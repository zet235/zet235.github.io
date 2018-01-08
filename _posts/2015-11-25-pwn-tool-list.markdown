---
layout: post
title:  "pwn tool list"
---

ub 14.04 x64

## i32 lib
```bash
apt-get install gcc-multilib
```

```bash
cd /etc/apt/sources.list.d
echo "deb http://old-releases.ubuntu.com/ubuntu/ raring main restricted universe multiverse" >ia32-libs-raring.list
apt-get update
apt-get install ia32-libs
```

```
dpkg --add-architecture i386
apt-get update
apt-get install libssl-dev:i386
```



## PEDA
```bash
apt-get install nasm micro-inetd
apt-get install libc6-dbg
https://github.com/longld/peda
```

## qira

https://github.com/BinaryAnalysisPlatform/qira


## pwntools
包含checksec, ROPgadget Tools

```bash
sudo pip install git+https://github.com/Gallopsled/pwntools#egg=pwntools
```

fix bug
```diff
cp /usr/local/lib/python2.7/dist-packages/usr/lib/python2.7/dist-packages/capstone/libcapstone.so /usr/local/lib/python2.7/dist-packages/capstone/.
```

## rp++
https://github.com/0vercl0k/rp/downloads

## ncat
```bash
sudo apt-get install netcat-traditional netcat-openbsd nmap
```
