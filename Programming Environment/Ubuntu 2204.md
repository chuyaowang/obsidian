# Ubuntu 22.04

## Install with Manual Partition

https://www.youtube.com/watch?v=Wc4GjV_Ahb8

Installing 3rd party drivers (Nvidia) require a password. Make it and remember it: 12345678
On reboot after installation. Choose enroll MOK. Then follow the instructions to enter your password. [Watch this](https://www.youtube.com/watch?v=A0gxy3xaJlE)

Manual partition
- EFI partition: 200 MB sdb1
- Root: 60 GB sdb2
- Home: 40 GB sdb3
- Swap: 17 GB (depend on RAM) sdb4

Separating home partition makes upgrading system or using multiple systems easier.
Why the size of EFI partition? [here](https://askubuntu.com/questions/670778/why-must-an-efi-partition-be-at-least-100mb)

## Fix Grub Location

> my fix is simply to use gparted to remove the boot flag before starting the  
> installer, and the setting it back when the install is finished. It always  
> works for me.

How to remove wrong grub and install correct one [here](https://www.reddit.com/r/Ubuntu/comments/nd2qzw/grub_installed_to_wrong_drive_bug/)
Install boot repair tool https://pimylifeup.com/ubuntu-boot-repair-tool/

## Change GRUB settings

Allows you to see more detailed logs during boot

Edit `/etc/default/grub` 

Change

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

to 

```
GRUB_CMDLINE_LINUX_DEFAULT=""
```

and set 

```
GRUB_TIMEOUT=10
```

Finally

```
sudo update-grub
```

## Samba

For smb file sharing, install samba

``` sh
sudo apt update
sudo install samba
```

``` sh
whereis samba
```

[Set up sharing](https://ubuntu.com/tutorials/install-and-configure-samba#3-setting-up-samba)

## V2ray

Core:

First download the core file at `https://github.com/v2fly/v2ray-core/releases/download/v5.16.1/v2ray-linux-64.zip`

Send it to the system via smb

Then in the smbshare directory
``` sh
curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh > go.sh
```

``` sh
sudo bash ./go.sh --local ./v2ray-linux-64.zip
```

``` sh
systemctl start v2ray
systemctl enable v2ray
```

v2rayA:

[Install and set auto-start](https://v2raya.org/en/docs/prologue/installation/debian/)

``` sh
sudo apt install /installer_path
```

``` sh
sudo systemctl start v2raya.service
sudo systemctl enable v2raya.service
```

### V2rayA usage

1. Choose up to 4 proxy servers
2. Set On: Proxt except CN Sites
3. Turn on at the top left
4. No need to configure bash again

### Disable

``` sh
sudo systemctl disable v2raya.service
sudo systemctl disable v2ray
sudo systemctl status v2ray
```

## Update and Upgrade


``` sh
sudo apt update && sudo apt upgrade
```

``` sh
sudo apt clean && sudo apt autoremove && sudo reboot
```

## rustdesk

Desktop sharing app

## Git

``` sh
sudo apt install git
```

## tlp

Power management

``` sh
sudo apt install tlp
sudo tlp start
tlp-stat -s
tlp-stat -b
sudo systemctl enable tlp
```

Edit charge level:

``` sh
sudo vim /etc/tlp.conf
```

Change

``` 
START_CHARGE_THRESH_BAT0=50
STOP_CHARGE_THRESH_BAT0=60
```

## Time discrepancy

https://www.howtogeek.com/323390/how-to-fix-windows-and-linux-showing-different-times-when-dual-booting/#:~:text=By%20default%2C%20Windows%20assumes%20the,make%20Windows%20use%20UTC%20time.
## CUDA

[Source](https://qiyuan-z.github.io/2022/01/04/Ubuntu%E5%A4%9A%E7%89%88%E6%9C%ACcuda%E5%AE%89%E8%A3%85%E4%B8%8E%E5%88%87%E6%8D%A2/)

## Zero Tier One

https://www.zerotier.com/download/#entry-4
Simulate LAN network for devices in different networks

MacOS: package installer
Linux: command line install

### Set-up

Go to my.zerotier.com
Make account
Create a network
Add members and authorize: [how](https://docs.zerotier.com/cli)
Turn off auto-assign IP
Add IPs within the managed routes

## ssh server

To ssh to Linux, Linux should be set up as a server. The computer that starts the ssh should have the ssh client. 
https://ubuntu.com/server/docs/openssh-server

Use `ssh-keygen -t rsa` to generate a pair of public and private keys. The public key should be stored on the server you're trying to access.

Use `ssh-copy-id username@ip` to add your public key to the host's authorized_keys

## SFTP server

Don't need to do anything extra. But for creating a user and assign to a group specifically for sftp, read below:
https://www.cybrosys.com/blog/how-to-setup-sftp-server-on-ubuntu-20-04

## conda

Install [conda](conda.md) on Ubuntu [here](https://docs.anaconda.com/miniconda/)

Install for multiple users [here](https://askubuntu.com/questions/1457726/how-and-where-to-install-conda-to-be-accessible-to-all-users). I used the group name `miniconda`

## jupyter lab

Install [jupyter](jupyter.md) lab on Ubuntu in [conda](conda.md).

Also installed jupyverse and set autostart. See [jupyter](jupyter.md) note.

## Turn off stupid sound

https://ubuntuhandbook.org/index.php/2023/01/disable-event-sound-ubuntu/

## Filling up EFI System Partition

https://askubuntu.com/questions/1410236/how-can-i-expand-the-boot-efi-partition-on-ubuntu-20-04

## The initramfs will attempt to resume from /dev/sdb4

https://askubuntu.com/questions/1189835/the-initramfs-will-attempt-to-resume-from-dev-dm-1

## Change Ubuntu mirror

Go into Software & Updates, choose new server location.

## Install fonts (like Times New Roman)

https://itsfoss.com/install-microsoft-fonts-ubuntu/

## Tailscale

- Trying this as a [Zero Tier One](#Zero%20Tier%20One) replacement
- Starts automatically

## Whisper

- Installed to pytorch251 [conda](Programming%20Environment/conda.md) env

## opencl

`sudo apt install ocl-icd-opencl-dev clinfo`