---
sectionid: prereq
sectionclass: h2
title: Prerequisites
parent-id: intro
---



#### GitHub Account
You will need a personal GitHub account for today's workshop. If you don't already have one, you can sign up for free [here](https://github.com/join).

#### SSH Client
You will also need a client to SSH into a jumphost for command line access. Linux and Mac systems tend to have one included, and one of the more popular clients for Windows is PuTTY that you can download [here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html). More recently, Windows 10 offers OpenSSH that can be [installed as an optional feature](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse).

#### Lab Setup
Along with the web interface, we will be running commands directly against our cluster using a jump host. The SSH client mentioned above will be used to establish an SSH session to that jump host, and the diagram below provides a visual of how this hangs together.

![Diagram](media/diagram.png)