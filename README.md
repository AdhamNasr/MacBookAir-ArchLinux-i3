<h1 align="center">
Macbook Air 7,2 - Arch i3 Install Instructions
</h1>
<p align="right">
 Copyleft
 <br> Author: <a href="mailto:adham@geektweax.com">Adham Nasr</a>
 <br> <strong>
  Hire Me: <a href="https://www.upwork.com/freelancers/~01b5998dd4563fe640">Upwork</a> • <a href="https://www.freelancer.com/u/adhamnasr">Freelancer</a>
 </strong>
</p>

---

A simple, yet detailed instructions on building [Arch Linux][arch] on a MacBook Air 7,2. There are also plans on writing a shell script for future installs on the same system.

Please note that the install process is built for the system mentioned, and is tailored to work on that particular system only!

So please read through the README before installing it on a different machine.

[arch]: https://www.archlinux.org/

---

## Table of Contents

- [Device Specs](#Device-Specs)
- [What Works](#what-Works)
- [FAQ](#FAQ)
- Installation:
  - [Part 1](/Install-p1.md)
  - [Part 2](/Insatll-p2.md)
  - [Part 3](/Install-p3.md)
---

Make Your Life Easier
-------

 1. RTM!! [ARCH INSTALL DOCS][docs]. Just go through the 1st few pages on how to install to understand what's going on.

 2. Read the whole README before taking any action.

 3. Ask questions!

[docs]: https://wiki.archlinux.org/index.php/Official_Arch_Linux_Install_Guide

---

Device Specs & What Works (as of 2021.11.01-x86_64)
-------

### Device Specs

       - Host: MacBookAir7,2 1.0
       - CPU: Intel i5-5250U (4) @ 2.700GHz
       - GPU: Intel HD Graphics 6000
       - Max Resolution: 1440x900
       - Memory: 4GiB
       - Storage: 120GiB
       - Network controller: BCM4360 802.11ac Wireless Network Adapter
       - Multimedia controller: Broadcom Inc. 720p FaceTime HD Camera


### What Works

  - [x] initial boot
  - [x] audio
  - [x] bluetooth
  - [x] wlan
  - [x] trackpad
  - [x] keyboard
  - [x] webcam
  - [x] function buttons
  - [x] keyboard backlight
  - [x] backlight control
  - [x] brightness control
  - [x] keyboard and screen backlight adjust on the ambient light
  - [x] suspend/sleep+wake
---
---
FAQ
---

- How to solve the “unable to lock database” or “failed to synchronize any databases” errors?
              
      # sudo rm /var/lib/pacman/db.lck