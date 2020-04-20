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

由于篇幅原因，本文重要介绍GCP网络中 VPC/Share VPC, Load Balancing 和 Router相关内容，而在下一章节谷歌云台网络（二）中介绍 CDN, NAT,VPN 以及相关安全性的服务。
## 谷歌云平台网络简介

## Visual Private Cloud (VPC)
VPC为GCE,CKE以及GAE提供了网络功能。所有GCE，GKE以及GAE都是通过VPC网络进行通信。VPC将各种资源连接起来，并将其同互联网相连接。

### VPC 网络
首先，VPC网络在资源管理层级上是属于全球性（global）资源，它不从属于特定的区域（regional）或者地区（zonal）。但是subnet是regional 资源，每个subnet会定义一个IP地址范围。VPC内的资源可以通过IPv4地址相互通信。通过对等连接，可以实现不同organization或者是Project间VPC连接。






