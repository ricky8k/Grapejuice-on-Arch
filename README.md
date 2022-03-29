# Grapejuice-on-Arch <img src="https://user-images.githubusercontent.com/92121005/160626622-e66b02a8-b287-4760-8340-b31fd22b0519.png" width="30">

*Also known as Roblox on Steam Deck and Arch*

Guide to [Grapejuice](https://gitlab.com/brinkervii/grapejuice) on Arch-based Linux distros
> Grapejuice is a Wine wrapper application that is tailored to Roblox. The aim is to make running Roblox on Linux as painless as possible.

- Grapejuice: https://gitlab.com/brinkervii/grapejuice
- Documentation: https://brinkervii.gitlab.io/grapejuice/docs/

This guide serves as an easier reference for inexperienced Linux users (like myself), [as this guide is a bit sparse](https://brinkervii.gitlab.io/grapejuice/docs/Installing-from-package/Arch-Linux-and-similar.html).

*I cannot guarantee this guide will work for everyone (especially with my limited Linux knowledge). If something doesn't work as intended, [you may find a fix here](https://github.com/ricky8k/Grapejuice-on-Arch#Troubleshooting).*

**I recommend you read the guide completely first before proceeding.**

## Table of Contents
**Sections labeled under SteamOS are not tested yet.** They are based off of relevant documentation I can find at the time of writing, so they *may* not work.

- [Config](https://github.com/ricky8k/Grapejuice-on-Arch#Config)
  - [Supported Distros](https://github.com/ricky8k/Grapejuice-on-Arch#Supported-Distros)
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
- [Credits](https://github.com/ricky8k/Grapejuice-on-Arch#Credits)

## Config
Working as of 3/28/22. Tested under a virtual machine, which shouldn't affect the guide (hopefully). *You'll have better performance using Grapejuice on bare metal instead.*

Using [Manjaro KDE Plasma 21.2.5](https://download.manjaro.org/kde/21.2.5/manjaro-kde-21.2.5-220314-linux515.iso) as SteamOS 3.0 [isn't available for general PC use](https://help.steampowered.com/en/faqs/view/1B71-EDF2-EB6D-2BB3) *yet*. I will likely redo under SteamOS when the time comes.

> For all the tinkerers out there, please note that this system image is not quite SteamOS 3 yet. Depending on what you try to install it on (desktop, another handheld, refrigerator, toaster), it may not work properly. SteamOS 3 proper will come out sometime after launch (and even then it may not work on your toaster).

<img src="https://user-images.githubusercontent.com/92121005/160516945-ec165b33-ffa8-4c5b-b639-4eccddde21f7.png" width="40">

![image](https://user-images.githubusercontent.com/92121005/160515637-5dfa61ec-399b-49ed-a6ab-e99ba479d773.png)

Ran under VMware Workstation Pro 16.2.1. Test machine used an AMD Ryzen 7 2700 (4c, 8t allocated) and 6GB of memory. Virtualized display adapter with 3D acceleration was enabled in VM settings.

This copy of Manjaro uses KDE Plasma, which is the same desktop interface on the Steam Deck.

### Supported Distros
From [Grapejuice](https://brinkervii.gitlab.io/grapejuice/docs/Installing-from-package/Arch-Linux-and-similar.html):
> - Arch Linux
> - Manjaro Linux
> - SteamOS 3.0

## Preperation
### SteamOS
If you're on Steam Deck, you're running SteamOS 3.0. 

Before proceeding, go to desktop mode and execute the following in Konsole:
```
sudo steamos-readonly disable
```
__This command disables the write protection for the main operating system on SteamOS__, allowing us unrestricted access to the system files. __This is required for installation to continue.__ Without access, scripts and patches used to get Roblox and Grapejuice running cannot run properly.

*Remember to enable it again after you've completed this installation, or your Deck will be vulnerable to unauthorized modification.*

Once you've completed the following, head on over to the [Manjaro/Arch](https://github.com/ricky8k/Grapejuice-on-Arch#ManjaroArch) section to finish the Preparation.

### Manjaro/Arch
If you're on Manjaro, [multilib](https://wiki.archlinux.org/title/official_repositories#multilib) *should* already be enabled by default. If not, or you're using a different Arch-based distro, we'll need to allow it in the `pacman.conf` file.

Access the text editor in Konsole with the following:
```
sudo nano /etc/pacman.conf
```
- You may also access the text file under that directory and edit from there.

Then, we'll need to locate a certain area of text. Uncomment (remove the # at the beginning) or add this to your file if it isn't already:
```
[multilib]
Include = /etc/pacman.d/mirrorlist
```
Once complete, save and exit the text editor.

Now, head on over to [Installation](https://github.com/ricky8k/Grapejuice-on-Arch#Installation) to install the AUR helper and Grapejuice.

## Installation
**Grapejuice requires an [AUR helper](https://wiki.archlinux.org/title/AUR_helpers) in order to install the package.** For this guide, I will be using [yay](https://aur.archlinux.org/packages/yay).

First, we'll navigate to the `/opt` directory:
```
cd /opt
```
Clone the `yay` repo under https://aur.archlinux.org/yay.git, then enter the new directory:
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
> ⚠️ Note: **These commands are not tested**, so I cannot tell if they will work. Should these commands fail, head on over to [Manjaro/Arch](https://github.com/ricky8k/Grapejuice-on-Arch#ManjaroArch-1).

We'll need to install `base-devel` with our package manager:
```
sudo pacman -S base-devel
```
Once installed, we can navigate to the `yay` directory and install it on the system:
```
cd ~/yay
makepkg -si
```
After `yay` is installed, we can finish and start installing [Grapejuice](https://aur.archlinux.org/packages/grapejuice-git)! Use:
```
yay -S grapejuice-git
```

Then you're all set! Now, head on over to [Patching](https://github.com/ricky8k/Grapejuice-on-Arch#Patching) to patch the Wine compatibility layer in order for Roblox to run properly.

### Manjaro/Arch
If you're on Manjaro or other Arch distribution, we'll need to perform some additional steps in order to get `makepkg -si` to work as intended.

You should be under the `/opt/yay` directory currently. We'll exit that directory, then change ownership to the user (you):
```
cd ..
sudo chown -R user:user ./yay               # Remember to remove "user" and replace it with your user.
cd yay
```
Make sure you have [make](https://archlinux.org/packages/core/x86_64/make/) installed. Get `make` with the following:
```
sudo pacman -S make
```
Once done, we can now use `makepkg -si`!
```
makepkg -si
```
Now you should be able to install the [Grapejuice](https://aur.archlinux.org/packages/grapejuice-git) package. Input the following:
```
yay -S grapejuice-git
```

Then you're all set! Now, head on over to [Patching](https://github.com/ricky8k/Grapejuice-on-Arch#Patching) to patch the Wine compatibility layer in order for Roblox to run properly.

## Patching
**In order for Roblox to be playable under Linux, we'll have to patch the Wine compatibility layer.** *Doing so will fix UI issues, unexpected crashes, and mouse locking with the program.*

### SteamOS
> ⚠️ Note: **These commands are not tested**, so I cannot tell if they will work. Should these commands fail, head on over to [Manjaro/Arch](https://github.com/ricky8k/Grapejuice-on-Arch#ManjaroArch-2).

First, we'll navigate to the `/tmp` directory with the following:
```
cd /tmp
```
We'll be applying a patch using [wget](https://wiki.archlinux.org/title/wget). Install if you haven't already, then we can get our `install.py`.
```
sudo pacman -S wget
wget https://pastebin.com/raw/5SeVb005 -O install.py
```
- Mirror: https://github.com/ricky8k/Grapejuice-on-Arch/blob/main/WinePatch/install.py

Now run `install.py` with Python:
```
python3 install.py
```

**Once the script finishes, you should be complete!** If you run into any issues running Grapejuice, head on over to [Troubleshooting](https://github.com/ricky8k/Grapejuice-on-Arch#Troubleshooting) for a possible fix.

### Manjaro/Arch
If you use Manjaro, other Arch distribution, or if the SteamOS method does not work, we'll be applying a different script to get Wine patched and running.

We'll navigate to the `/opt` directory and clone the [wine-tkg-git](https://github.com/frogging-family/wine-tkg-git) repository to it:
```
cd /opt
sudo git clone --depth=1 https://github.com/frogging-family/wine-tkg-git.git
cd wine-tkg-git
```
Now that we have `wine-tkg-git`, [we can apply the custom patch](https://github.com/e666666/robloxWineBuildGuide/):
```
sudo curl https://raw.githubusercontent.com/e666666/robloxWineBuildGuide/main/roblox-wine-staging-v2.2.patch --output roblox-wine-staging-v2.2.patch
sudo git apply roblox-wine-staging-v2.2.patch
```
- Mirror: https://raw.githubusercontent.com/ricky8k/Grapejuice-on-Arch/main/WinePatch/v2.2/roblox-wine-staging-v2.2.patch

Once the patch is applied, we'll need ownership of the new folder in order to use `makepkg -si`:
```
sudo chown -R user:user ./wine-tkg-git               # Remember to remove "user" and replace it with your user.
cd wine-tkg-git
makepkg -si
```
- Press "Enter" when prompted, press "Y", use default "1," then "Y" again.

**Roblox should be patched now!** If you run into any issues running Grapejuice, head on over to [Troubleshooting](https://github.com/ricky8k/Grapejuice-on-Arch#Troubleshooting) for a possible fix.

## Troubleshooting
- Grapejuice Wiki: https://brinkervii.gitlab.io/grapejuice/docs/Troubleshooting.html

## Credits
- [BrinkerVII](https://gitlab.com/brinkervii) for [Grapejuice](https://gitlab.com/brinkervii/grapejuice)
- [e666666](https://github.com/e666666) for [robloxWineBuildGuide](https://github.com/e666666/robloxWineBuildGuide/)
- [Frogging-Family](https://github.com/frogging-family) for [wine-tkg-git](https://github.com/frogging-family/wine-tkg-git)

## 
*ricky8k*
- https://github.com/ricky8k
