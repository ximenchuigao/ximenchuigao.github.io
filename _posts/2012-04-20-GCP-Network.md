---
layout: post
title:  GCP Network
subtitle:   谷歌云平台网络 （一）
date:       2020-04-20	
author:     吹糕
catalog: true 	
tags:							
    - GCP Architect
---

由于篇幅原因，本文重要介绍GCP网络中 VPC/Shared VPC, Load Balancing 和 Router相关内容，而在下一章节谷歌云台网络（二）中介绍 CDN, NAT,VPN 以及相关安全性的服务。
## 谷歌云平台网络简介

## Visual Private Cloud (VPC)
VPC为GCE,CKE以及GAE提供了网络功能。所有GCE，GKE以及GAE都是通过VPC网络进行通信。VPC将各种资源连接起来，并将其同互联网相连接。

### VPC 网络
首先，VPC网络在资源管理层级上是属于全球性（global）资源，它不从属于特定的区域（regional）或者地区（zonal）。但是subnet是regional资源，每个subnet会定义一个IP地址范围。VPC内的资源可以通过IPv4地址相互通信。通过对等连接，可以实现不同organization或者是Project间VPC连接。
GCP提供两种创建VPC网络的方式，自动创建和自定义创建。不同方式创建的VPC网络，他们的subnet创建方式也不一样
- 在自动模式下创建的VPC，它同时也创建了一个具有预定义范围的IP subnet (10.128.0.0/9)
- 自定义创建的VPC他不会创建subnet。这里要注意的是自动模式的VPC可以转换成自定义VPC，但自定义VPC不能转换成自动模式的VPC。

自动模式适用于对于预定义的IP范围同特定使用的IP范围没有冲突。而自定义模式下的network更为复杂灵活，同时可以更好的在生产环境下使用。

### Shared VPC
Shared VPC 允许在一个组织内的资源通过一个common的VPC相互连接。他们之间的通信采用内部的IP。在设计Shared VPC时，将一个project作为Host project,而其他的project则称为service projects。service project里的资源可以使用shared VPC network里的subnet。

一个Project不能既为Host project又是service project。你可以创建多个Host project,但一个service project只能有一个Host project。

Shared network可以是自动模式创建的VPC,也可以是自定义模式创建的VPC。但是shared network不支持legacy networks。










