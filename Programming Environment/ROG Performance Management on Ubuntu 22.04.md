# asusctl Installation Guide on Ubuntu 22.04

## Overview

This document covers the full process of installing **Rust** (system-wide), **asusctl** (built from source), and **rog-control-center** on Ubuntu 22.04, including all errors encountered and their resolutions.

**System:** ASUS ROG Strix G731GU  
**OS:** Ubuntu 22.04  [Ubuntu 2204](Programming%20Environment/Ubuntu%202204.md)
**Kernel:** 6.8.0-110-generic  
**asusctl version:** 6.3.7

---

## Background

asusctl is a daemon and CLI tool for controlling ASUS ROG/TUF laptop features on Linux (fan curves, thermal profiles, RGB, battery charge limits, etc.). It is the closest Linux equivalent to ASUS Armoury Crate.

There is no official PPA or apt package for Ubuntu. The recommended install method uses an Arch Linux repo (pacman), so on Ubuntu the only supported path is **building from source**.

**Project links:**
- asusctl source: https://gitlab.com/asus-linux/asusctl
- supergfxctl source: https://gitlab.com/asus-linux/supergfxctl
- Project website: https://asus-linux.org

---

## Prerequisites

### Kernel version

asusctl requires kernel **6.6 or newer**. Ubuntu 22.04 ships with 5.15 by default.

Check your kernel version:
```bash
uname -r
```

If below 6.6, upgrade via the HWE stack:
```bash
sudo apt install --install-recommends linux-generic-hwe-22.04
sudo reboot
```

---

## Part 1: Installing Rust System-Wide

asusctl is written in Rust and must be compiled from source. The default Rust installer installs to the current user's home directory (`~/.cargo`). To make Rust available to all users (including root, which is needed for `sudo make install`), install it to a system path instead.

### Step 1: Create the system Rust directory

```bash
sudo mkdir -p /usr/local/rust
```

### Step 2: Run the Rust installer with custom paths

```bash
sudo RUSTUP_HOME=/usr/local/rust/rustup CARGO_HOME=/usr/local/rust/cargo \
  sh -c 'curl --proto "=https" --tlsv1.2 -sSf https://sh.rustup.rs | sh'
```

### Step 3: Make the paths permanent for all users

```bash
sudo tee /etc/profile.d/rust.sh << 'EOF'
export RUSTUP_HOME=/usr/local/rust/rustup
export CARGO_HOME=/usr/local/rust/cargo
export PATH="$CARGO_HOME/bin:$PATH"
EOF
```

### Step 4: Source it in the current session

```bash
source /etc/profile.d/rust.sh
```

### Step 5: Verify

```bash
rustc --version
```

### Note on permissions

The `/usr/local/rust` directory is owned by root by default. Regular users cannot write to it, which causes build failures (see error below). Fix with:

```bash
sudo chown -R $USER:$USER /usr/local/rust
```

This does **not** break access for other users. It only changes the owner — read and execute permissions (`755`) remain intact for everyone. Other users can still run Rust tools; only the owner can write/update them.

---

## Part 2: Installing Build Dependencies

```bash
sudo apt update
sudo apt install make cmake libclang-dev libinput-dev libgbm-dev \
  libxkbcommon-dev libsystemd-dev libexpat1-dev libpcre2-dev \
  libzstd-dev libgtk-3-dev clang
```

If `make` fails with a missing library error, install the `-dev` package for that library and retry. The error message will name the library.

---

## Part 3: Building and Installing asusctl

### Step 1: Download the source

Download the zip from: https://gitlab.com/asus-linux/asusctl/-/releases

### Step 2: Extract and enter the directory

```bash
unzip asusctl-*.zip
cd asusctl-*
```

### Step 3: Build

```bash
make
```

### Step 4: Install

```bash
sudo make install
```

### Expected install output

The following files are installed:

```
/usr/bin/asusd                          # main daemon
/usr/bin/asusctl                        # CLI tool
/usr/bin/asusd-user                     # user-space daemon
/usr/bin/asus-shutdown                  # shutdown helper
/usr/bin/rog-control-center             # GUI application
/usr/lib/udev/rules.d/99-asusd.rules    # udev rule for auto-start
/usr/share/asusd/aura_support.ron       # LED support data
/usr/share/dbus-1/system.d/asusd.conf   # DBus config
/usr/lib/systemd/system/asusd.service   # systemd service
/usr/lib/systemd/system/asus-shutdown.service
/usr/share/applications/rog-control-center.desktop
/usr/share/icons/hicolor/...            # notification icons
```

Two `realpath: missing operand` warnings may appear during install. These are harmless — they relate to optional AniMe matrix display support which is not present on most ROG laptops.

---

## Part 4: Starting the asusd Daemon

### Enable and start via systemd

```bash
sudo systemctl daemon-reload
sudo systemctl enable asusd
sudo systemctl start asusd
```

**Note on `systemctl enable`:** asusd will print a warning saying it has no `[Install]` section. This is intentional — the service is designed to be activated automatically via its udev rule (`99-asusd.rules`) when the keyboard driver is ready at boot. The `enable` command is not required. Simply starting it is sufficient:

```bash
sudo systemctl start asusd
```

### Verify it is running

```bash
systemctl status asusd
asusctl --version
asusctl profile -l       # list available thermal profiles
```

---

## Errors Encountered and Resolutions

### Error 1: Permission denied building Rust dependencies

**Symptom:**
```
error: failed to create directory `/usr/local/rust/cargo/git/db/sg-rs-b76dcf934df278cd`
Caused by: Permission denied (os error 13)
```

**Cause:** `CARGO_HOME` points to `/usr/local/rust/cargo` which is owned by root, but `make` runs as the regular user.

**Resolution:**
```bash
sudo chown -R $USER:$USER /usr/local/rust
```
Then re-run `make` as normal. Only `make install` needs sudo.

---

### Error 2: asusd fails to start via systemd — `226/NAMESPACE`

**Symptom:**
```
asusd.service: Failed with result 'exit-code'
Process: ExecStartPre=/bin/sleep 1 (code=exited, status=226/NAMESPACE)
```

**Cause (discovered via `journalctl -u asusd.service -b --no-pager`):**
```
asusd.service: Failed to set up mount namespacing:
/run/systemd/unit-root/etc/asusd: No such file or directory
```

The service file has `ReadWritePaths=/etc/asusd/` but that directory did not exist yet. Systemd tries to set up the mount namespace for it before starting the process, finds the directory missing, and aborts.

**Additional context from the journal:**
```
/lib/systemd/system/asusd.service:32: Unknown key name 'PrivateBPF' in section 'Service', ignoring.
/lib/systemd/system/asusd.service:45: Failed to parse boolean value, ignoring: strict
/lib/systemd/system/asusd.service:52: Unknown key name 'RestrictNetworkInterfaces' in section 'Service', ignoring.
```

These warnings indicate that Ubuntu 22.04's systemd (version 249) does not recognise some newer service file options (`PrivateBPF`, `RestrictNetworkInterfaces`, `ProtectControlGroups=strict`) that were introduced in systemd 254. These are **ignored harmlessly** and are not the cause of the failure.

**Resolution:**
```bash
sudo mkdir -p /etc/asusd
sudo systemctl daemon-reload
sudo systemctl start asusd
```

---

### Confirming asusd works: running directly

To see the raw daemon output and confirm it starts correctly, bypass systemd entirely:

```bash
sudo /usr/bin/asusd
```

Key lines confirming successful startup:
```
[INFO  asusd] Product family: ROG Strix
[INFO  asusd] Board name: G731GU
[INFO  asusd] Startup success on dbus name xyz.ljones.Asusd: begining dbus server loop
```

**Non-critical warnings in the output:**

| Warning | Explanation |
|---|---|
| `Config "/etc/asusd/asusd.ron" does not exist` | Normal on first run; config is created automatically |
| `FanCurves: Profile error: Not supported` | G731GU hardware does not expose full fan curve control via this interface |
| `No serial for SCSI device: /devices/virtual/block/loopN` | Debug noise from snap mount points; harmless |
| `No Anime Matrix capable laptop found` | G731GU does not have an AniMe matrix display |

---

## Part 5: rog-control-center

rog-control-center is the GUI frontend for asusctl. It was installed as part of the asusctl build (the source repo includes it). It requires:
- asusd to be running
- A **Wayland** display session (X11 is not supported)

### Launching

```bash
rog-control-center
```

Or from the application menu after login.

### Error: Wayland not found

**Symptom:**
```
thread 'main' panicked at rog-control-center/src/main.rs:310:40:
called `Result::unwrap()` on an `Err` value: Could not initialize backend.
Error from Winit backend: neither WAYLAND_DISPLAY nor WAYLAND_SOCKET is set;
note: enable the `winit/x11` feature to support X11
```

**Cause:** The binary was compiled with Wayland support only. X11 is explicitly not supported by the developers. Either the session is X11, or the Wayland socket variables are not set (e.g. when running from a root terminal).

**Check your session type:**
```bash
echo $XDG_SESSION_TYPE
```

**Resolution:**
- If `x11`: Switch to a Wayland session at the login screen (click the gear icon, select "Ubuntu on Wayland"), then re-launch rog-control-center.
- If `wayland` but running via sudo: Run as your normal user without sudo.
- If Wayland is unavailable: Use the `asusctl` CLI instead — it works on any display server.

---

## Part 6: Notes on Related Tools

### supergfxctl

supergfxctl is a **separate project** not included in asusctl. It manages GPU switching between integrated (Intel) and discrete (NVIDIA) graphics. Source: https://gitlab.com/asus-linux/supergfxctl

It is only needed if you want to switch GPU modes. Without it, the system defaults to hybrid mode: the Intel iGPU drives the display while the NVIDIA dGPU is available for applications via PRIME render offload:

```bash
__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia <application>
```

### Conflict with TLP (battery charge limit)

[tlp](Programming%20Environment/Ubuntu%202204.md#tlp)
Both TLP and asusd can manage the battery charge limit via `/sys/class/power_supply/BAT0/charge_control_end_threshold`. Running both will cause conflicts as they overwrite each other.

**Resolution:** Pick one. To use asusctl for charge management and disable TLP's charge control, comment out `START_CHARGE_THRESH_BAT0` and `STOP_CHARGE_THRESH_BAT0` in `/etc/tlp.conf`, then set the limit via asusctl:

```bash
asusctl -c 80   # set charge limit to 80%
```

### Energy Performance Preference (EPP)

asusctl links thermal profiles to CPU Energy Performance Preference automatically. When you switch profiles, the EPP is updated for all CPU cores:

| asusctl Profile | EPP |
|---|---|
| Performance | Performance |
| Balanced | BalancePerformance |
| Silent | BalancePower or Power |

Switch profiles with:
```bash
asusctl profile -P Performance
asusctl profile -P Balanced
asusctl profile -P Silent
```

---

## Quick Reference

```bash
# Check kernel version
uname -r

# Check Rust version
rustc --version

# Start asusd
sudo systemctl start asusd

# Check asusd status
systemctl status asusd

# List thermal profiles
asusctl profile -l

# Switch thermal profile
asusctl profile -P Performance

# Set battery charge limit
asusctl -c 80

# Fan curve help
asusctl fan-curve -h

# Check asusd logs
journalctl -u asusd.service -b --no-pager

# Launch GUI (requires Wayland + asusd running)
rog-control-center
```

## Change profile on start-up

```bash
sudo vim /etc/asusd/asusd.ron
```

Change platform_profile_on_ac to Quiet, Balanced, or Performance.

Then restart.