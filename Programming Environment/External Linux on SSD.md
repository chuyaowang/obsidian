# External Linux on SSD

## 1. SSD Partition

Leave out 130 GBs for the system in ext4

## 2. Create bootable USB flashdrive

Download Ubuntu 24.04 image
Use balenaEtcher to write it to a usb stick with 8GB storage

## 3. Boot from USB

Restart, enter BIOS by smashing F2 when the ROG logo shows, then change the boot sequence.
In other computers it's possible to disconnect the internal drives to avoid mistakenly overwriting them.
Restart to enter the Ubuntu menu

## 4. Install Ubuntu

Choose Ubuntu (Safe Graphics)
Follow the instructions
- Don
Choose `Manual Partition`
- In **most** cases, the internal HD will show up as `sda` and the external as `sdb`, but this is not guaranteed.
- `ESP Partition`: `VFAT`，500 MB
- `swap`: 8 GB, should not exceed computer RAM
- `/`: `ext4`, 60 GB, root partition
- `/boot/efi`: `VFAT`, 1 GB, created automatically
- `/home`: `ext4`, 40 GB, separate for easier system upgrade later
- The rest of space can be allocated for other use

> [!info] The /home directory
> With all credit to Ubuntu, the home directory is:
> 
> - Where your Desktop resides.
> - Where your documents, pictures, music, videos, audio, and pretty much everything else can be stored.
> - Where your application settings are stored, in hidden files and directories (their names start with a . ) that you should not touch unless you know what you are doing. Eg, /home/username/.thunderbird contains your Thunderbird emails and contacts, /home/username/.mozilla contains Firefox bookmarks, passwords, history, plugins…
> - The only place (with the exclusion of removable drives and the /tmp directory) within the Ubuntu file system where a user can freely create/modify/remove files and directories without needing root permissions or the sudo command.

> [!info] Bootloader
> The /boot/efi partition is for installing the bootloader to boot the system.
> 
> Make sure to choose bootloader installation to be on the external SSD.

## 5. Installing upgrades

### Recovery mode

Enter Recovery mode (Advanced options for Ubuntu) and boot in secure mode by choosing the 1st option. 



### White screen error

It may enter a white screen with 'Oh no .... contact system administrator' message. This is caused by gdm3 and gnome desktop.

Boot through recovery mode, then use the terminal:
Or press `Ctrl+Alt+F3`, and use the terminal:

working solution:
[source](https://askubuntu.com/questions/1050672/gdm3-does-not-start-in-ubuntu-18-04)
``` sh
sudo apt install ubuntu-gnome-desktop
sudo apt install gnome-shell gnome
sudo systemctl restart gdm3
sudo reboot
```

or try this:
``` sh
sudo apt purge gdm3
sudo reboot
```

When the computer boots again, only terminal is available. Enter

```
sudo apt install gdm3
sudo service gdm start
```

``` sh
sudo apt-get clean && sudo apt-get autoremove && sudo reboot
```

Or try lightdm, did not work for me

``` sh
sudo apt install lightdm
sudo dpkg-reconfigure lightdm
```

Or reinstall Nvidia driver
### Useful commands

Display system info

``` sh
inxi -G
```

Find package installed

```
dpkg -l | grep 'nvidia'
```

### Failed to start Nvidia persistence daemon

First check

``` sh
systemctl status nvidia-persistenced.service
```

If it runs don't worry about it

If it does not:
[Source](https://ubuntu.com/server/docs/nvidia-drivers-installation)
``` sh
sudo apt purge nvidia-*
sudo apt --purge remove '*nvidia*${DRIVER_BRANCH}*'
sudo apt autoremove
```
like `'*nvidia*535*'`

Then install the driver 

``` sh
sudo apt install nvidia-driver-535 nvidia-dkms-535
```

or

``` sh
sudo ubuntu-drivers install
```

Check installation

``` sh
nvidia-smi
```

Then install the Nvidia settings app

``` sh
sudo apt install nvidia-settings
```




