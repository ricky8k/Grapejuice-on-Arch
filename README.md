# Grapejuice-on-Arch
(Work-in-Progress)

Guide to Grapejuice on Arch-based Linux distros

- Grapejuice: https://gitlab.com/brinkervii/grapejuice
- Documentation: https://brinkervii.gitlab.io/grapejuice/docs/

This guide serves as an easier reference (for myself mainly) to look back to, [as this guide is a bit sparse](https://brinkervii.gitlab.io/grapejuice/docs/Installing-from-package/Arch-Linux-and-similar.html).

## Table of Contents
- [Config](https://github.com/ricky8k/Grapejuice-on-Arch#Config)
- [Preperation](https://github.com/ricky8k/Grapejuice-on-Arch#Preperation)
  - [SteamOS](https://github.com/ricky8k/Grapejuice-on-Arch#SteamOS)
- [Installation](https://github.com/ricky8k/Grapejuice-on-Arch#Installation)

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

### Manjaro/Arch


