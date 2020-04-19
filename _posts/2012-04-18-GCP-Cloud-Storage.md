---
layout: post
title:  GCP Storage
subtitle:   谷歌云平台存储服务分类以及应用场景 （一）
date:       2020-04-18	
author:     吹糕
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
独立于G Suite 的存储协作服务
- Cloud Storage for Firebase
为Firebase设计的Cloud Storage,可供快速存储/读取用户数据，例如照片，视频等。
- Local SSD
从物理上直接attached到虚拟机实例上，因此，其具有非常快的读写速度。


下面就来介绍一下它们的特点以及相应的使用场景

## Cloud Storage 
  Cloud Storage 是支持全球边缘缓存的对象存储服务。首先从[资源的管理](http://example.com/)角度来说，Cloud Storage 中的数据是属于project层级的。在Cloud Storage里，Buckets是数据基本的存储单位，其中Buckets名字必须是唯一标识的。而object是bucket中的数据对象，object由data和metadata组成。一个object可以存在多个版本，版本号存在metadata中。

### 分类

|    分类    | 最少存储时间 |    有效性/每月
| -- | -- |--
| Standard Storage |  None |>99.99%  multi-regions and dual-regions <br> 99.99% in regions
| Nearline Storage       |  30天 |99.95% in multi-regions and dual-regions<br>99.9% in regions
| Coldline Storage      |  90天 |99.95% in multi-regions and dual-regions<br>99.9% in regions
| Archive Storage       |  365天 |99.95% in multi-regions and dual-regions<br>99.9% in regions

另外，根据数据存储的物理空间，又可分为单区域存储以及多区域存储。（单区域存储考虑速度和价格，多区域存储考虑容灾及有效性）
### 特点
#### Pub/Sub集成
Cloud Storage可以与Pub/Sub集成，换而言之，当Cloud Storage中的object发生改变时，可以配置Pub/Sub将消息发布出来。具体支持的消息类型可参见[官网相关文档](https://cloud.google.com/storage/docs/pubsub-notifications)。

#### 数据对象版本设置
Cloud Storage 可以对 data object设置版本，其版本信息存在Metadata中。
#### 生命周期管理
通过对data object 生命周期管理可以降低成本。例如，可以配置将存储在standard storage 里超过30天的 data object 自动转移到Nearline Storage中，从而达到降低成本的目的。
#### 请求者付费
在以下几种情况下，可以设置数据请求者来支付查询费用。数据请求者在请求数据时需要关联一个projectId用以付费。
- 对Cloud Storage里的数据进行操作产生的费用
- 网络传输产生的费用
- 查询存储在Nearline Storage, Coldline Storage, Archive Storage中的数据而产生额外的费用
#### 数据加密
Cloud Storage中的数据支持加密，密钥可以托管在GCP key management service 上，也可以由客户自己保存。（具体见GCP Security）
#### 审计日志
Cloud Storage可以与Cloud Audit Logs服务集成。
#### CORS 支持
Cloud Storage可以用于host静态网站，其提供了CORS支持。

### gsutil 支持
gsutil是GCP提供的与Cloud Storage交互的命令行工具，例如：
- 创建一个bucket:  
  `` gsutil mb -b on -l us-east1 gs://my-awesome-bucket/ ``
- 下载数据  
  `` gsutil cp gs://my-awesome-bucket/image.png``
- 列出一个bucket 里的data object  
  `` gsutil ls gs://my-awesome-bucket ``

等等，更多命令可参考相关官方文档
### 权限设置
详见Cloud IAM, 在这不做赘述。
### 典型应用

#### 在数据分析中的应用

![在数据分析中的应用](/assets/cloud-storage-integrated-repository.png)

#### Media 数据存储
![在数据分析中的应用](/assets/cloud-storage-media-content-storage-and-delivery.png)

#### 备份和归档
![在数据分析中的应用](/assets/cloud-storage-backups-and-archives.png)
