# RESCUE Partition Installation on SSD

This guide outlines the process of creating a "Self-Rescue" environment on your internal SSD. This setup allows you to boot into a Live Ubuntu environment (stored on your SSD) to perform maintenance, resize partitions, or reinstall the OS without needing a physical USB or SD card.

---

## 1. Partition Preparation & Permissions

Before you can store the rescue image, you need a dedicated "landing zone" on your drive.

### Step A: Create the Partition

1. Open **GParted**.
2. Create a small partition (Recommended: **8GB - 10GB**) at the end of your drive.
3. Format it as **ext4**.
4. Set the label to `RESCUE`.

### Step B: Claim Ownership

By default, new ext4 partitions are owned by the `root` user. You must change ownership to your own user account to move files into it.

```bash
# 1. Find where the partition is mounted
lsblk -f

# 2. Claim ownership (replace 'RESCUE_MOUNT_PATH' with the path from lsblk)
# Example path: /media/username/RESCUE
sudo chown $USER:$USER /media/$USER/RESCUE
```

If the new partition is not named correctly, use this command to rename it:

```bash
sudo e2label /dev/sdb6 RESCUE
```

Change `/dev/sdb6` to your actual drive mount point.

To change the name of an `exfat` partition, run:

```bash
sudo exfatlabel /dev/sdb5 Portable
```

---

## 2. Deploying the ISO Image

The bootloader needs a static file to "loopback" into.

1. Download the **Ubuntu Desktop ISO** (e.g., Ubuntu 22.04 or 24.04).
2. Move the file to the **root** of your new `RESCUE` partition.
3. **Crucial:** Rename the file to exactly `ubuntu.iso`.

> **Note:** Do not put the file inside a folder. It must sit directly on the partition (e.g., `/media/username/RESCUE/ubuntu.iso`).

---

## 3. GRUB Configuration

You must manually tell the GRUB bootloader how to find and "mount" this ISO file during the boot process.

### Step A: Get the Partition UUID

GRUB works best with UUIDs because they don't change if you plug in other drives.

```bash
# Identify your RESCUE partition and copy the long UUID string
lsblk -f
```

### Step B: Edit the Custom Boot Script

```bash
# Open the custom configuration file
sudo nano /etc/grub.d/40_custom
```

Paste the following at the bottom of the file (below the existing headers). Replace `YOUR_UUID_HERE` with the string you just copied:

```text
menuentry "Ubuntu Live (Emergency Rescue)" {
    # Locate the partition by its UUID
    search --no-floppy --fs-uuid --set=root YOUR_UUID_HERE
    
    # Define the ISO path and map it to a loop device
    set isofile="/ubuntu.iso"
    loopback loop ($root)$isofile
    
    # Load the kernel. 'toram' copies the OS to RAM so you can unmount the SSD later.
    linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=$isofile toram --
    
    # Load the initial RAM disk
    initrd (loop)/casper/initrd
}
```

### Step C: Update the Master Bootloader

For the changes to take effect, you must regenerate the main GRUB configuration.

```bash
sudo update-grub
```

---

## 4. Usage & Maintenance

### How to use the Rescue Partition

1. **Reboot** your computer.
2. Select **"Ubuntu Live (Emergency Rescue)"** from the boot menu.
3. Once the desktop loads, open **GParted**.
4. **Unmount the Rescue Partition:** Because you used the `toram` flag, you can now right-click the `RESCUE` partition in GParted and select **Unmount**.
5. You now have full access to resize or move your main `/` and `/home` partitions.

### Important Commands Reference

| Task | Command |
| :--- | :--- |
| **Check Mounts** | `lsblk` |
| **Change Label** | `sudo e2label /dev/sdXX RESCUE` |
| **Reset Ownership** | `sudo chown $USER:$USER /path/to/mount` |
| **Update Bootloader** | `sudo update-grub` |

---

> **Peer Advice:** If you ever decide to change the ISO (e.g., upgrading to a newer version of Ubuntu), just swap the file in the `RESCUE` partition and name it `ubuntu.iso`. As long as the partition UUID stays the same, you don't even need to touch the GRUB config again.
