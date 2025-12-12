This project has been created as part of the 42 curriculum by : **obakri**
# born2beroot 
## Overview

This project aims to introduce you to the world of virtualization through creating a debian/rocky machine in VirtualBox (or UTM if you can’t use VirtualBox) using specific instructions.By the end of this project , you'll know how to se up your own OS while implementing strict rules like : user management, SSH configuration, firewall rules and password policies .

## What is virtualization ? 
Virtualization is a technology that allows the creation of virtual hardware from a single physical machine, enabling it to be shared across multiple instances of virtual machines using **Hypervisor**

**What is a Hypervisor ?**

A hypervisor (or Virtual Machine Monitor, VMM) is software that lets multiple operating systems run on a single physical machine. It manages hardware resources (CPU, memory, storage) and allocates them to virtual machines (VMs) without interference. 

**Types of Hypervisor :**

There are two main types of hypervisors:
- **Type 1** (Bare metal) :it runs directly on the host's hardware ,without depending on a host OS . example (KVM,VMware ESXi)

- **Type2** (Software hypervisor) : this type runs on top of another OS . it's a software application within the host OS .

![Hypervisor types](https://gigacloud.eu/wp-content/webpc-passthru.php?src=https://gigacloud.eu/wp-content/uploads/2024/10/65fd76b3c43ad-1-1024x538.png&nocache=1)

## VirtualBox vs UTM 

VirtualBox and UTM are both Type-2 hypervisors (run on top of a host OS) .the main difference is that virtualbox is free, open-source and cross-platform which means it works on windows, linux and macOS .UTM also is open-source , but it is mainly designed for MacOS solution . 

**My choice and why:**

For this project, I chose VirtualBox for two reasons: I've used it before and since I'm running Linux as my host OS, VirtualBox is the optimal solution.

## What is OS ?
An operating system acts as an intermediary between the computer hardware and the user. In short, it is an interface between computer hardware and the user.it is a collection of software that manages a computer’s hardware and applications by allocating resources, including memory, CPU, input/output devices and file storage.

**OS components :**

An Operating System (OS) comprises core components like the Kernel (managing hardware interaction), Process Management (handling programs), Memory Management (allocating RAM), File System (organizing storage), I/O Device Management (controlling peripherals), Security, and the User Interface (shell/CLI) for user interaction, all working to manage hardware/software resources and provide a platform for applications. 

**What is linux :**
![Hypervisor types](https://www.opensourceforu.com/wp-content/uploads/2017/02/Tux-with-tablet.jpg)
 Linux is a family of open-source operating systems based on the Linux kernel, originally created by Linus Torvalds in 1991. It’s one of the most widely used OS families in the world.

 **What is a Linux distribution?**

A Linux distribution (or "distro") is a complete, ready-to-use operating system built around the Linux kernel, bundling it with essential software, libraries, tools, and a package manager, packaged for specific uses like desktops, servers, or embedded devices, offering flexibility and customization. Think of the Linux kernel as the engine, and a distro as the entire car, including the body, seats, dashboard (desktop environment), and wheels (package manager). 

## Debian VS Rocky 

Both Debian and Rocky are popular Linux distributions , but they serve different focuses: 


| Feature | Debian | Rocky Linux |
|---------|--------|-------------|
| **Base** | Independent distribution | RHEL (Red Hat Enterprise Linux) clone |
| **Package Manager** | APT (`apt`, `apt-get`) | DNF/YUM (`dnf`, `yum`) |
| **Package Format** | `.deb` | `.rpm` |
| **Community** | Huge, one of the oldest distros | Growing refugees |
| **Documentation** | Extensive, been around since 1993 | Good, benefits from RHEL/CentOS docs been around since 2021|
| **Learning Curve** | Beginner-friendly |more enterprise-focused |
| **Use Case** | Servers, desktops, everything | Enterprise servers, production environments |

**why i choose this OS:**

I chose Debian over Rocky because it is way more easy for beginners - it has simpler syntax and commands, and it is also better documented for newcomers. Debian uses AppArmor which is simpler and easier to configure compared to SELinux . Without forgetting the package management simplicity using apt, it is also easier to install and manage packages like sudo and ssh.debian is independent distro but Rocky is built in top another distro .

**Debian Advantages :**

1- **It is maintained by its users:** If something needs to be fixed or improved, we can just do it.

2- **Easy updates:**  Upgrading to a new version of Debian is very easy thanks to our packaging system. You just have to run apt update; apt full-upgrade and can be upgraded .

3- **Stability:** One of the most stable operating systems available today.

**Debian disadvantages :**

1- **A prior knowledge:** You need to already know some Linux basics to use the operating system comfortably.example : Terminal Basics, Package Management etc...

2-**Steeper learning curve for Windows users:** because it relies more on the terminal.


## Sitting up my system 

### hostname 

As a hostname for my machine i choosed user+42 . The hostname is the human-readable name assigned to a device (computer, server, phone, router, etc.) on a network.

**To change the hostname permanently**

open the following file and change the old hostname by the new one .

``` 
sudo nano /etc/hostname
``` 

### System users 

I configured my root password and created a user with my login 

### System Design Choices 

#### Partitioning Scheme

partitions schemes are methods for dividing storages (disks …) into logical sections , the most common schemes are : MBR and GPT .


I have created two main partitions: the boot partition and sda5. The boot partition holds essential files to launch the operating system. It's where the BIOS loads the kernel when you start your system.
The second partition (sda5) is encrypted. It uses LVM to divide it into logical volumes.

**Why i choose this structure:**

Sda5 is an encrypted partition, so I needed a separate unencrypted partition (/boot) to store OS files. The BIOS and bootloader cannot decrypt encrypted partitions, so they need direct access to the files required to load the kernel into memory.

#### My logical volumes : 
I have devided sda5 into 7 logical partition 

1- root : contains the core of the operating system (kernel files , libraries , os binaries etc...)

2- swap : acts as an extra RAM when physical memory is full . it helps to prevent crashes when memory is full .

3-home : it contains users files and personal data , it is separated so even you reinstall the OS your personal files stay safe .
