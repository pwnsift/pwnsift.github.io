---
layout: blog-read
title: "What's Wrong With NetHydra Contrib? Contrib is missing?"
date: 2026-11-18 20:54:00 +0700
author: Joe
categories: NetHydra
thumbnail: /assets/graphics/thumbnails/nethydra-contrib.jpg
permalink: /blog/:title
description: "Today, we facing an issue about driver especially nvidia for NetHydra, why you couldn't install it?"
---

Hi, I'm joe, And today, on [Pwn Sift Blog](/blog), we would to announcing a problem facing By [NetHydra 1.1.0](https://pwnsift.github.io/blog/nethydra-1.1.0-release).

you might wondering when you trying to install some driver, especialy `nvidia-driver` you will facing an issue like `E: Package nvidia-driver has no installation candidate` even if you already updating the `APT database`.

## But why we didn't fix it ASAP?

this issue appear while we trying to installing `nvidia-driver` to our NetHydra System a few weeks ago, before we didn't have any `nvidia device` so we couldn't test it

## And How to fix it?

to fix this issue, very easy you can just add `contrib` component to your `debian.sources`
 `NetHydra` system, you can follow the command below

```
root@nh:~# cat <<EOF> /etc/apt/sources.list.d/debian.sources
Types: deb deb-src
URIs: http://deb.debian.org/debian/
Suites: trixie
Components: main contrib non-free non-free-firmware
Enabled: yes
Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg
EOF

root@nh:~# apt update && apt full-upgrade -y
# Then try to install the driver
root@nh:~# apt install -y nvidia-driver
```

This issue will be fixed for Next Release