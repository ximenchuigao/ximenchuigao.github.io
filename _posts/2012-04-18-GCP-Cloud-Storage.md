---
layout: post
title:  GCP Storage
subtitle:   谷歌云平台存储服务分类以及应用场景
date:       2020-04-18	
author:     ChuiGao 
catalog: true 	
tags:							
    - GCP Architect
---

## 简介
谷歌云平台的存储服务有：
- Cloud Storage 
支持全球边缘缓存的对象存储服务
- Cloud Filestore
高性能文件存储服务
- Persistent Disk
用于虚拟机实例的块存储服务
- Drive Enterprise
- Cloud Storage for Firebase
- Local SSD

下面就来介绍一下他们的特点以及相应的使用场景

## Cloud Storage 
  Cloud Storage 是支持全球边缘缓存的对象存储服务。首先从[资源的管理](http://example.com/)角度来说，Cloud Storage 中的数据是属于project的。在Cloud Storage里，Buckets是数据基本的存储单位，其中Buckets名字必须是唯一标识的。而object是bucket中的数据对象，object由data和metadata组成。一个object可以存在多个版本，版本号存在metadata中。

### 分类

|    分类    | 最少存储时间 |    有效性/每月
| -- | -- |--
| Standard Storage |  None |>99.99%  multi-regions and dual-regions <br> 99.99% in regions
| Nearline Storage       |  30天 |99.95% in multi-regions and dual-regions<br>99.9% in regions
| Coldline Storage      |  90天 |99.95% in multi-regions and dual-regions<br>99.9% in regions
| Archive Storage       |  365天 |99.95% in multi-regions and dual-regions<br>99.9% in regions

### 特点
#### Pub/Sub集成
Cloud Storage可以与Pub/Sub集成，换而言之，当Cloud Storage中的object发生改变时，可以配置Pub/Sub将消息发布出来。具体支持的消息类型可参见[官网相关文档](https://cloud.google.com/storage/docs/pubsub-notifications)。

#### 数据对象版本设置
#### 生命周期管理
#### 请求者付费
#### 转码