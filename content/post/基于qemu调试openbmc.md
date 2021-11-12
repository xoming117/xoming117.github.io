---
title: "基于qemu调试openbmc镜像"
date: 2021-11-10T16:00:05+08:00
draft: true
tags: ["bmc"]
---
1.切换到bmc镜像目录

```
cd openbmc/ff/build/tmp/deploy/images/evb-ast2500
```

2.qemu启动镜像

```
sudo qemu-system-arm -m 256 -machine romulus-bmc -nographic -drive file=./image-bmc,format=raw,if=mtd -net nic -net user,hostfwd=:127.0.0.1:22-:22,hostfwd=:127.0.0.1:443-:443,hostfwd=tcp:127.0.0.1:80-:80,hostfwd=tcp:127.0.0.1:2200-:2200,hostfwd=udp:127.0.0.1:623-:623,hostfwd=udp:127.0.0.1:664-:664,hostname=qemu
```

3.登录bmc系统
```
ipmitool power status
```

