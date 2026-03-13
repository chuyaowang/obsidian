# Incident Report: Tailscale Connectivity Loss & System Freeze (ASUS ROG Strix)

**Date:** January 7, 2026
**Affected System:** ASUS ROG Strix G731GU ([Ubuntu 2204](Programming%20Environment/Ubuntu%202204.md))
**Services Impacted:** SSH, Ping, RustDesk, Tailscale Tunnel, Jupyter Notebook
**Primary Trigger:** Python Segfault interacting with NVIDIA Drivers

## 1. Problem Description

The remote Linux machine became unreachable via Tailscale after a period of partial instability.

* **Initial State:** The user was running a Jupyter Notebook remotely. The connection appeared stable for hours after the initial internal error.
* **Symptoms:**
* **Admin Panel:** Device showed "Connected" (false positive).
* **Network:** `tailscale netcheck` was healthy, but no traffic (`rx 0`) was received from the peer.
* **Physical:** Screen frozen, total OS lockup requiring hard reset.

## 2. Timeline of Failure (The "Zombie" State)

The system did not crash instantly; it experienced a "cascading failure" where the graphical interface died long before the network stack.

* **11:02:23 (The Trigger):** `python3.10 segfault`
* **Event:** A Python process (likely a heavy C/C++ library within Jupyter like NumPy or TensorFlow) attempted a memory or GPU operation that conflicted with the display driver.
* **Impact:** The "Gui/Display" component crashed, but the system kernel and background services (HTTP server for Jupyter) remained alive.

* **12:13:08 (Network Instability):** `magicsock: derp-14 does not know about peer`
* **Event:** Tailscale began losing connectivity to the coordination server (Control Plane), but the established direct tunnel for the Jupyter session remained open.

* **13:55:44 (Display Death):** `RustDesk Error: Can't open display`
* **Event:** The user attempted to connect via Remote Desktop. The service failed because the X11/Wayland display server was already dead from the 11:02 event.

* **14:35:00 (Total System Freeze):**
* **Event:** The instability finally spread to the Kernel (Kernel Panic or Deadlock).
* **Result:** The network stack collapsed, cutting off the Jupyter connection and causing the "Timed Out" errors.

## 3. Root Cause Analysis (RCA)

### Primary Cause: Wayland vs. NVIDIA Incompatibility

The ASUS ROG Strix (Hybrid Graphics) was running the **Wayland** display server with proprietary **NVIDIA** drivers. This combination is known to cause deadlocks when heavy computational tasks (Python/Data Science) interact with the GPU.

Checking display server: `echo $XDG_SESSION_TYPE`
Checking Nvidia driver: `nvidia-smi`. Proprietary driver installed would return information.

### The "Trigger": Jupyter Notebook Execution

The Python segfault was not a random error but a resource conflict.

* **Mechanism:** When the Jupyter kernel executed a computationally intensive task, it invoked the GPU driver.
* **Conflict:** Because the driver was unstable under Wayland, the operation caused a segmentation fault in the process, triggering the slow system collapse.

### Post-Reboot Complication: DNS Deadlock

After the forced hard reset, the machine remained offline because `systemd-resolved` was corrupted. Tailscale could not resolve its control server to re-login, creating a dependency loop.

## 4. Resolution Strategy

### Immediate Recovery

1. **Hard Reset:** Forced power cycle (10-second power button hold).
2. **DNS Repair:**
```bash
sudo systemctl restart systemd-resolved
sudo systemctl restart tailscaled

```

### Permanent Fixes

1. **Switch to X11 (Critical):**
* Log out and select **"Ubuntu on Xorg"** at the login screen. This removes the Wayland instability that caused the Python segfault.


2. **Disable Sleep:**
* Prevent the laptop from suspending during heavy workloads:
```bash
sudo systemctl mask sleep.target suspend.target

```
- Alternatively, disable Screen Blank and Automatic Suspend in settings

3. **Disable Livepatch:**
* Reduced log noise and overhead: `sudo snap disable canonical-livepatch`

## 5. Early Warning Signs & Best Practices

If this situation repeats, observe the "Canary" services:

* **The "Canary" Rule:** If secondary services (RustDesk, SSH, or generic Internet browsing) fail while your Jupyter Notebook is still working, **SAVE YOUR WORK IMMEDIATELY.**
* **Interpretation:** This indicates the OS is in a "Headless Survival Mode." The display server has died, and a total kernel freeze is imminent (usually within 1-2 hours). Do not attempt to fix it remotely; save data and issue a `sudo reboot` command immediately if the shell is still responsive.