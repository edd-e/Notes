# How to set up a Raspberry Pi with Raspberry Pi OS<!-- omit in toc -->

This guide contains helpful details and configuration options for a headless Raspberry Pi with Raspberry Pi OS. At the end of this guide the Pi should be in a good state for a Pi-hole installation.

## Table of contents<!-- omit in toc -->

- [Introduction](#introduction)
- [Installing Raspberry Pi OS](#installing-raspberry-pi-os)
  - [Getting started](#getting-started)
  - [Setting up the microSD card](#setting-up-the-microsd-card)
- [Preparing the connection](#preparing-the-connection)
  - [Enabling SSH](#enabling-ssh)
  - [Connecting to the LAN](#connecting-to-the-lan)
  - [Logging in to the Raspberry Pi](#logging-in-to-the-raspberry-pi)
- [Raspberry Pi OS configuration](#raspberry-pi-os-configuration)
  - [Initial system setup](#initial-system-setup)
  - [Raspberry Pi OS updates](#raspberry-pi-os-updates)
    - [Finding and installing upgrades](#finding-and-installing-upgrades)
    - [Housekeeping](#housekeeping)
    - [Combining commands](#combining-commands)
  - [Static IP address](#static-ip-address)
- [SSH key-based authentication](#ssh-key-based-authentication)
  - [SSH keys](#ssh-keys)
  - [How to generate SSH keys](#how-to-generate-ssh-keys)
  - [Copying the public key to the Raspberry Pi](#copying-the-public-key-to-the-raspberry-pi)
  - [How to disable SSH password authentication](#how-to-disable-ssh-password-authentication)
  - [SSH config](#ssh-config)
- [Conclusion](#conclusion)

## Introduction

Raspberry Pi OS is a free GNU/Linux operating system based on Debian and optimized for Raspberry Pi.

## Installing Raspberry Pi OS

There are two Raspberry Pi OS installations to choose from. The desktop edition is optimized with a user interface and pre-loaded applications. The lite edition is streamlined for the command prompt, usually ideal for a headless setup.

### Getting started

Required resources;

- Raspberry Pi Model 2, 3, Zero W, or 4
- power supply
- micro SD card (16gb or more is recommended)
- computer
- LAN network
- Raspberry Pi OS `.img` download

Raspberry Pi OS lite can be downloaded directly from the Raspberry Pi Foundation [website](https://www.raspberrypi.org/downloads). Extract the Raspberry Pi OS `.img` file from the zip folder.

### Setting up the microSD card

To install Raspberry Pi OS, write the `.img` file to the micro SD card:

1. Connect the microSD card to the computer.

2. Format the card to `FAT32`.

3. In the terminal, run this command to find the SD card (example: /dev/disk2):

   ```sh
   diskutil list
   ```

4. Un-mount the disk (SD card)

   ```sh
   diskutil unmountDisk /dev/disk2
   ```

5. Copy the Raspberry Pi OS `.img` to the card (note the use of raw disk "`rdisk`")

   ```sh
   sudo dd bs=1m if=/path/to/RPiOS.img of=/dev/rdisk2; sync
   ```

6. Wait for the process to finish (`ctrl` + `T` to see progress), then eject the card

   ```sh
   sudo diskutil eject /dev/rdisk2
   ```

The Pi is now ready to run Raspberry Pi OS from the micro SD card.

## Preparing the connection

This section covers how to connect to the Raspberry Pi by SSH.

### Enabling SSH

An empty file named `ssh` is all that is required to enable SSH.

1. Reconnect the microSD card.

2. Navigate to the card (shows up as a drive with a `boot` partition).

3. On the root directory run:

   ```sh
   touch ssh
   ```

### Connecting to the LAN

A Pi wired directly to the LAN by ethernet is ready to go, skip to step 4 below.

To connect to a WLAN specify the Wi-Fi credentials needed to join the network. With the microSD card still connected:

1. Navigate to the card (shows up as a drive with a `boot` partition).

2. Create a file named `wpa_supplicant.conf`. Copy/paste these contents with the correct country and network details:

   ```sh
   country=US
   update_config=1
   ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev

   network={
     ssid="wifi"
     psk="password"
   }
   ```

3. Save and close the file.

4. Eject the microSD card from the computer and insert it into the Pi.

5. Connect the Pi to the power supply.

### Logging in to the Raspberry Pi

To connect to the Pi by SSH, open the terminal and use this command:

```sh
ssh pi@raspberrypi.local
```

On a new Raspberry Pi OS installation, `pi` is the default username. The Pi's default hostname is `raspberrypi`, the Pi's IP address can be used instead of its hostname.

To execute the command by IP address:

```sh
ssh pi@IP
```

Enter the password to authenticate the session, the default password is `raspberry`.

Note: Security addressed in SSH section below.

## Raspberry Pi OS configuration

This section of the guide will cover initial system configuration and Raspberry Pi OS updates.

### Initial system setup

After logging in use this command to access the configuration options:

```sh
sudo raspi-config
```

This command launches a tool with a simple user interface. Use the arrow keys to move between selections, the space key to check/un-check settings, and the tab key to switch between the selection area and command area.

Some of the more noteworthy things to configure are:

- Change the user password.

  - Change the default password. Every Raspberry Pi OS installation has the same default login.

- Network Options

  - Change the hostname to something else, useful when you have more than one Pi.

- Localization Options

  - Adjust the locale, time zone, keyboard settings, and wi-fi region.

- Advanced Options

  - Expand the file system to make full use of the memory card.

- Update

  - Updates the raspi-config tool.

A reboot may be required.

### Raspberry Pi OS updates

Raspberry Pi OS uses the Advanced Packaging Tool (APT) to update the package list and check for updates.

#### Finding and installing upgrades

To update the package list, run the command:

```sh
sudo apt-get update
```

To check the updated package list, and install the available package upgrades run:

```sh
sudo apt-get upgrade
```

Some packages may have dependencies that need upgrading. To upgrade them, use:

```sh
sudo apt-get dist-upgrade
```

#### Housekeeping

To remove packages that are no longer needed use:

```sh
sudo apt-get autoclean
```

To remove packages that were automatically installed to satisfy dependencies for other packages, and that are no longer needed, use:

```sh
sudo apt-get autoremove
```

To manually reboot the Pi use:

```sh
sudo reboot
```

To manually shutdown the Pi use:

```sh
sudo halt
```

#### Combining commands

You can combine most commands using the `&&` operator:

```sh
sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get autoclean
```

The commands will execute automatically in that order.

### Static IP address

Pi-hole requires that the Raspberry Pi have a static IP address so that the gateway can use it as the default DNS.

To see the current network information use `ifcongig`.

To set a static IP address open `/etc/dhcpcd.conf`. Enter the desired information for interface, IP address, subnet mask, gateway, and DNS:

```sh
# Custom static IP configuration:
interface eth0
static_ipaddress=192.168.0.2/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1 1.1.1.1
```

Save the file and reboot the Pi to implement the settings. An optional step is to reserve the desired static IP directly on the LAN router.

## SSH key-based authentication

How to configure SSH keys to securely log in to the Raspberry Pi.

### SSH keys

When using SSH key authentication, a pair of two secure keys are cryptographically generated and used to authenticate an SSH session. The private key is kept on the client and the public key is stored on the host.

### How to generate SSH keys

The command to create SSH keys is `ssh keygen`. To get started, open the terminal on the computer. To generate Ed25519 keys, the command is:

```sh
ssh-keygen -t ed25519
```

The system will prompt for a name to assign to the generated keys. Then, for added security, select a passphrase or continue.

A key pair will be generated and saved to `~/.ssh/`. For example; a private key named `id_ed25519` would have a corresponding public key named `id_ed25519.pub`.

### Copying the public key to the Raspberry Pi

Before adding the public key to the authorized keys list in the Raspberry Pi create this folder:

```sh
mkdir ~/.ssh
```

The list should be located here. Create a file named `authorized_keys` then copy and add the contents of `id_ed25519.pub`. Save and close the file.

The last step is to modify the permissions. Run this to set the `~/.ssh/` directory permissions:

```sh
chmod 700 ~/.ssh/
```

Run this to set the authorized list permissions:

```sh
chmod 600 ~/.ssh/authorized_keys
```

You can now log out of the Raspberry Pi and begin a new SSH session. Upon logging in, you will not be prompted for the password.

### How to disable SSH password authentication

After verifying that ssh key authentication is working properly, disable password authentication on the Raspberry Pi to increase security.

To disable password authentication open the `/etc/ssh/sshd_config` file. Uncomment this option and set it to `no`:

```sh
PasswordAuthentication no
```

Reboot the Pi for the setting to take effect.

It is important to note that we have effectively limited access to only one device: the computer where the private key is stored. It's advisable to secure a backup copy, or enable another machine to log in with its own key.

### SSH config

On the computer, open the `~/.ssh/config` file and add the following information:

```sh
Host pi
    Hostname raspberrypi.local
    User pi
    IdentityFile ~/.ssh/id_ed25519
```

This makes logging in to the Raspberry Pi as simply as entering this command:

```sh
ssh pi
```

## Conclusion

Thats is all! This configuration guide should leave the Raspberry Pi in a good state to install Pi-hole.
