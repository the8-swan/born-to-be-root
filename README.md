This project has been created as part of the 42 curriculum by : Obakri
# Born to be root 
## Overview

This project introduces you to the world of system administration through virtualization. You will create and configure a virtual machine using VirtualBox (or UTM if VirtualBox is unavailable), following strict security and configuration guidelines.

## Project Goals

By the end of this project, you will be able to:
- Set up your own operating system from scratch in a virtualized environment
- Implement strict security rules and system policies
- Understand the fundamentals of system administration
- Configure and manage a secure server environment

## Description
Born2beRoot is a system administration project that focuses on virtualization and server security. You'll learn to build a functional virtual machine while adhering to specific technical requirements, including user management, security policies, partitioning schemes, and service configuration. This hands-on experience provides essential knowledge for managing and securing Linux-based systems.

### Debian vs Rocky Linux Comparison

| Feature | Debian | Rocky Linux |
|---------|--------|-------------|
| Base | Independent, community-developed. | Red Hat Enterprise Linux (RHEL) source code. |
| Package Manager | APT with .deb packages | DNF/YUM with .rpm packages  |
| Target Audience | General-purpose users, developers, servers | Enterprises needing a stable, RHEL-compatible platform |

### why is choosed this OS:

I chose Debian over Rocky because it is way more easy for beginners - it has simpler syntax and commands, and it is also better documented for newcomers. Debian uses AppArmor which is simpler and easier to configure compared to SELinux . Without forgetting the package management simplicity using apt, it is also easier to install and manage packages like sudo and ssh.debian is indepent distro but rockyy is built in top another distro .

**Debian Advantages :**

1- ***It is maintained by its users:*** If something needs to be fixed or improved, we can just do it.

2-***Easy updates:***  Upgrading to a new version of Debian is very easy thanks to our packaging system. You just have to run apt update; apt full-upgrade and can be upgraded .

3-***It is one of the most stable Operating Systems today.***

**Debian disadvantages :**

1- ***A prior knowledge:*** You need to already know some Linux basics to use the operating system comfortably.example : Terminal Basics, Package Management etc...

2-***Windows users may find Debian harder*** : because it relies more on the terminal.


s
