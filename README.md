<h1 align="center">
Macbook Air 7,2 - Arch Linux i3 Manual Install Instructions
</h1>
<p align="right">
 Copyleft
 <br> Author: <a href="mailto:adham@geektweax.com">Adham Nasr</a>
 <br> <strong>
  Hire Me: <a href="https://www.fiverr.com/adhamnasr?public_mode=true">Fiverr</a> • <a href="https://thegeektweax.com">The Geek Tweax</a>
 </strong>
</p>

---

This document provides simple yet detailed instructions on how to install [Arch Linux][arch] on a [MacBook Air 7,2][MBA].

Please note that the install instructions are tailored to work on that particular system only!

So please read through the README before installing it on a different machine.

[arch]: https://www.archlinux.org/
[MBA]: https://support.apple.com/kb/SP714?locale=en_US
---

## Table of Contents

- [Device Specs](#Device-Specs)
- [What Works](#What-Works)
- [FAQ](#FAQ)
- Installation:
  - [Part 1](/Install-p1.md)
  - [Part 2](/Install-p2.md)
  - [Part 3](/Install-p3.md)
---

Make Your Life Easier
-------

 1. Read the official manual ---> [ARCH INSTALL DOCS][docs]. Just go through the 1st few pages on how to install to have a better understanding of what's going on.

 2. Read the whole README before taking any action.

 3. Ask questions!

[docs]: https://wiki.archlinux.org/index.php/Official_Arch_Linux_Install_Guide

---

Device Specs & What Works
-------

### Device Specs

       - Host: MacBookAir7,2 1.0
       - CPU: Intel i5-5250U (4) @ 2.700GHz
       - GPU: Intel HD Graphics 6000
       - Max Resolution: 1440x900
       - Memory: 4GiB
       - Storage: 120GiB
       - Bluetooth 4.0
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
  - [ ] suspend/sleep+wake (used to work, will troubleshoot)
---
---
FAQ
---

- How to solve the “unable to lock database” or “failed to synchronize any databases” errors?
              
      # sudo rm /var/lib/pacman/db.lck