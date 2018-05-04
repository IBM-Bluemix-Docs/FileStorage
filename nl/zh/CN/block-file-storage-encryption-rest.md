---

copyright:
  years: 2014, 2018
lastupdated: "2018-04-23"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 确保数据安全 - 提供者管理的静态加密 

{{site.data.keyword.BluSoftlayer_full}} 认真对待安全性需求，并深知能够加密数据以保证数据安全的重要性。借助提供者管理的加密，缺省情况下，会加密所供应的类型为“耐久性”或“性能”的 {{site.data.keyword.filestorage_full}}，这无需任何额外费用，对性能也没有任何影响。

提供者管理的静态加密功能使用以下业界标准协议：

* 业界标准 AES-256 加密
* 使用业界标准密钥管理互操作性协议 (KMIP) 对密钥进行内部管理
* 存储器已通过美国联邦信息处理标准 (FIPS) 出版物 140-2 的验证，符合《联邦信息安全管理法案》(FISMA)、《健康保险可移植性和责任法案》(HIPAA)、支付卡行业 (PCI) 标准、《巴塞尔协议 II》、《加利福尼亚州违反安全信息法》(SB 1386) 和《欧盟数据保护指令 (95/46/EC)》

## 针对快照或已复制存储器的静态加密  

缺省情况下，加密文件存储器的所有快照和副本也都已加密。此功能无法逐个卷加以禁用。

## 为存储器供应加密

提供者管理的静态加密功能仅可用于在精选数据中心（会定期添加更多新的数据中心）内供应的 {{site.data.keyword.filestorage_short}}。对于在这些数据中心内供应的所有存储器，都自动供应了静态数据加密。单击[此处](new-ibm-block-and-file-storage-location-and-features.html)以查看可使用 {{site.data.keyword.filestorage_short}} 静态数据加密的数据中心的当前列表。


订购 {{site.data.keyword.filestorage_short}} 时，请选择标有星号 (`*`) 以及声明加密可用的消息的数据中心。您将在“LUN/卷名”字段右侧看到“锁定”图标，指示已对其进行加密。请参阅图 1。

![“锁定”图标指示 LUN 已加密](/images/encryptedstorage.png)
<caption>图 1. 用于指示卷已加密的“锁定”图标的示例。</caption>



**注**：在数据中心升级之前供应的非加密存储器**不会**自动进行加密。如果在已升级的数据中心内有非加密存储器，那么需要创建新卷，然后执行数据迁移。以下文章可以提供相关指导。

* [在已升级的数据中心内进行文件存储器迁移](migrate-file-storage-encrypted-file-storage.html)
