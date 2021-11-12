---
title: "bmc常用命令"
date: 2021-11-10T14:23:44+08:00
draft: false
tags: ["bmc"]
---

BMC (Baseboard Management Controler)提供了多种通道来和主机通信，进而检测主机的温度、风扇转速、电压、电源和现场可替代器件。为了便于用户使用，它提供了非常丰富的命令，下面介绍一下主要的常用命令。

### 1. 远程电源控制类

ipmitool -I lanplus –H 10.32.228.111 –U username –P Passwordchassis power off

ipmitool -I lanplus –H 10.32.228.111 –U username –P Passwordchassis power on

ipmitool -I lanplus –H 10.32.228.111 –U username –P Passwordchassis power reset

ipmitool -I lanplus –H 10.32.228.111 –U username –P Passwordchassis power cycle

(注意power cycle 和power reset的区别在于前者从掉电到上电有１秒钟的间隔，而后者是很快上电)

### 2. 读取系统状态类

ipmitool sensor list 显示系统所有传感器列表

ipmitool fru list 显示系统所有现场可替代器件的列表

ipmitool sdr list 显示系统所有SDRRepository设备列表

ipmitool pef list 显示系统平台时间过滤的列表

### 3. 系统日志类

ipmitool sel elist 显示所有系统事件日志

ipmitool sel clear 删除所有系统时间日志

ipmitool sel delete ID 删除第ID条SEL

ipmitool sel time get 显示当前BMC的时间

ipmitool sel time set XXX 设置当前BMC的时间

### 4. 启动设置类

ipmitool chassis bootdev bios 重启后停在BIOS 菜单

ipmitool chassis bootdev pxe 重启后从PXE启动

### 5. 系统相关的命令

ipmitool mc info 显示BMC版本信息

ipmitool bmc reset cold BMC 热启动

ipmitool bmc reset warm BMC冷启动

### 6. 网络接口相关命令

ipmitool lan print 1 显示channel1的网络配置信息

ipmitool lan set 1 ipaddr 10.32.2.2 设置channel1的IP地址

ipmitool lan set 1 netmask 255.255.0.0 设置channel1的netmask

ipmitool lan set 4 defgw ipaddr255.255.0.254 设置channel4的网关

ipmitool lan set 2 defgw macaddr 设置channel2的网关mac address

ipmitool lan set 2 ipsrc dhcp 设置channel2的ip 源在DHCP

ipmitool lan set 3 ipsrc static 设置channel2的ip是静态获得的

### 7. 通道相关命令
ipmitool channel info 显示系统默认channel

ipmitool channel authcap channel-number privilege 修改通道的优先级别

ipmitool channel getaccess channel-number user-id 读取用户在通道上的权限

ipmitool channel setacccess channel-number user-id callin=on ipmi=on link=onprivilege=5 设置用户在通道上的权限

### 8. 看门狗相关命令

ipmitool mc watchdog get 读取当前看门狗的设置

ipmitool watchdog off 关掉看门狗

ipmitool watchdog reset 在最近设置的计数器的基础上重启看门狗

### 9. 用户管理相关命令

ipmitool user list chan-id 显示某通道上的所有用户

ipmitool set password [] 修改某用户的密码

ipmitool disable 禁止掉某用户

ipmitool enable 使能某用户

ipmitool priv [] 修改某用户在某通道上的权限

ipmitool test <16|20> 测试用户