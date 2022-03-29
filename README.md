# Grapejuice-on-Arch
(Work-in-Progress)

Guide to [Grapejuice](https://gitlab.com/brinkervii/grapejuice) on Arch-based Linux distros

- Grapejuice: https://gitlab.com/brinkervii/grapejuice
- Documentation: https://brinkervii.gitlab.io/grapejuice/docs/

This guide serves as an easier reference for inexperienced Linux users (like myself), [as this guide is a bit sparse](https://brinkervii.gitlab.io/grapejuice/docs/Installing-from-package/Arch-Linux-and-similar.html).

*I cannot guarantee this guide will work for everyone (especially with my limited Linux knowledge). If something doesn't work as intended, I won't be able to help.*

## Table of Contents
**Sections labeled under SteamOS are not tested yet.** They are based off of relevant documentation at the time of writing, so they may not work.

- [Config](https://github.com/ricky8k/Grapejuice-on-Arch#Config)
- [Preperation](https://github.com/ricky8k/Grapejuice-on-Arch#Preperation)
  - [SteamOS](https://github.com/ricky8k/Grapejuice-on-Arch#SteamOS)
  - [Manjaro/Arch](https://github.com/ricky8k/Grapejuice-on-Arch#ManjaroArch)
- [Installation](https://github.com/ricky8k/Grapejuice-on-Arch#Installation)
  - [SteamOS](https://github.com/ricky8k/Grapejuice-on-Arch#SteamOS-1)
  - [Manjaro/Arch](https://github.com/ricky8k/Grapejuice-on-Arch#ManjaroArch-1)
- [Patching](https://github.com/ricky8k/Grapejuice-on-Arch#Patching)
  - [SteamOS](https://github.com/ricky8k/Grapejuice-on-Arch#SteamOS-2)
  - [Manjaro/Arch](https://github.com/ricky8k/Grapejuice-on-Arch#ManjaroArch-2)
- [Troubleshooting](https://github.com/ricky8k/Grapejuice-on-Arch#Troubleshooting)

## Config
Working as of 3/28/22. Tested under a virtual machine, which shouldn't affect the guide (hopefully). *You'll have better performance using Grapejuice on bare metal instead.*

Using [Manjaro KDE Plasma 21.2.5](https://download.manjaro.org/kde/21.2.5/manjaro-kde-21.2.5-220314-linux515.iso) as SteamOS 3.0 [isn't available for general PC use](https://help.steampowered.com/en/faqs/view/1B71-EDF2-EB6D-2BB3) *yet*. Will likely redo under SteamOS when the time comes.

> For all the tinkerers out there, please note that this system image is not quite SteamOS 3 yet. Depending on what you try to install it on (desktop, another handheld, refrigerator, toaster), it may not work properly. SteamOS 3 proper will come out sometime after launch (and even then it may not work on your toaster).

<img src="https://user-images.githubusercontent.com/92121005/160516945-ec165b33-ffa8-4c5b-b639-4eccddde21f7.png" width="40">

![image](https://user-images.githubusercontent.com/92121005/160515637-5dfa61ec-399b-49ed-a6ab-e99ba479d773.png)

Ran under VMware Workstation Pro 16.2.1. Test machine used an AMD Ryzen 7 2700 (4c, 8t allocated) and 6GB of memory. Virtualized display adapter with 3D acceleration was enabled in VM settings.

## Preperation
### SteamOS
If you're on Steam Deck, you're running SteamOS 3.0. 

Before proceeding, you'll need to execute the following in terminal:
```
sudo steamos-readonly disable
```
__This command disables the write protection for the main operating system on SteamOS__, allowing us unrestricted access to the system files. __This is required for installation to continue.__ Without access, scripts and patches used to get Roblox and Grapejuice running cannot run properly.

*Remember to enable it again after you've completed this installation, or your Deck will be vulnerable to unauthorized modification.*

Once you've completed the following, head on over to the [Manjaro/Arch](https://github.com/ricky8k/Grapejuice-on-Arch#ManjaroArch) section to finish the [Preperation](https://github.com/ricky8k/Grapejuice-on-Arch#Preperation)

### Manjaro/Arch
If you're on Manjaro, [multilib](https://wiki.archlinux.org/title/official_repositories#multilib) *should* already be enabled by default. *However*, if you are unable to use the repo, or you're using a different Arch-based distro, we'll need to allow it in the `pacman.conf` file.

Access the text editor with the following:
```
sudo nano /etc/pacman.conf
```
- You may also access the text file under that directory and edit from there.

Then, we'll need to locate a certain area of text. Uncomment (remove the # at the beginning) or add this to your file if it isn't already:
```
[multilib]
Include = /etc/pacman.d/mirrorlist
```
Save and exit the text editor.

## Installation
Grapejuice requires an [AUR helper](https://wiki.archlinux.org/title/AUR_helpers) in order to install the package. For this guide, I will be using [yay](https://aur.archlinux.org/packages/yay).

First, we'll navigate to the `/opt` directory:
```
cd /opt
```
Clone https://aur.archlinux.org/yay.git, then enter the new directory:
```
sudo git clone https://aur.archlinux.org/yay.git
cd yay
```
Remove an unnecessary directory:
```
sudo rm -r /etc/pacman.d/gnupg/
```
Next, we'll need to initialize `pacman-key` to check signed packages. Input the following:
```
sudo pacman-key --init
sudo pacman-key --populate archlinux
sudo pacman -Sc
sudo pacman -Syyu
```

### SteamOS
> Note: These commands are not tested, so I cannot tell if they will work. Should these commands fail, head on over to [Manjaro/Arch](https://github.com/ricky8k/Grapejuice-on-Arch#ManjaroArch-1).

We'll need to install `base-devel` with our package manager:
```
sudo pacman -S base-devel
```
Once installed, we can navigate to the `yay` directory and install it on the system:
```
cd ~/yay
makepkg -si
```
After `yay` is installed, we can finish and start installing Grapejuice!
```
yay -S grapejuice-git
```

Then you're all set! Now, head on over to [Patching](https://github.com/ricky8k/Grapejuice-on-Arch#Patching) to patch Wine and allow Roblox to run properly.

### Manjaro/Arch
(WIP)

## Patching
(WIP)

## Troubleshooting
(WIP)
