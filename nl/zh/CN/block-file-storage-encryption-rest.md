---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

keywords: File Storage, file storage, NFS, security, encryption

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 提供者管理的静态加密
{: #encryption}

{{site.data.keyword.BluSoftlayer_full}} 认真对待安全性需求，并深知能够加密数据以保证数据安全的重要性。借助提供者管理的加密，缺省情况下，会加密通过“耐久性”或“性能”选项供应的 {{site.data.keyword.filestorage_full}}，这无需任何额外费用，对性能也没有任何影响。

提供者管理的静态加密功能使用以下业界标准协议：

* 业界标准 AES-256 加密
* 使用业界标准密钥管理互操作性协议 (KMIP) 对密钥进行内部管理
* 存储器根据以下标准进行验证：
    - 美国联邦信息处理标准 (FIPS) 出版物 140-2，
    - 《联邦信息安全管理法案》(FISMA)，
    - 《健康保险可移植性和责任法案》(HIPAA)，
    - 支付卡行业 (PCI) 标准，
    - 新巴塞尔协议，
    - 《加利福尼亚州违反安全信息法》(SB 1386)，以及
    - 《欧盟数据保护指令 (95/46/EC)》合规要求。

## 确保快照或已复制存储器的安全  

缺省情况下，加密文件存储器的所有快照和副本也都已加密。此功能无法逐个卷加以禁用。

## 为存储器供应加密

提供者管理的静态加密功能在精选数据中心内提供。对于在这些数据中心内订购的所有存储器，都自动供应了静态数据加密。单击[此处](/docs/infrastructure/FileStorage?topic=FileStorage-news)以查看可使用 {{site.data.keyword.filestorage_short}} 加密的数据中心的当前列表。

订购 {{site.data.keyword.filestorage_short}} 时，请选择标有星号 (`*`) 的数据中心。您可以在“LUN/卷名”字段右侧看到“锁定”图标，指示已对该卷进行加密。请参阅图 1。

![“锁定”图标指示 LUN 已加密](/images/encryptedstorage.png)
<caption>图 1. 用于指示卷已加密的“锁定”图标的示例。</caption>

在升级数据中心之前供应的任何非加密存储器**不会**自动加密。如果在已升级的数据中心内拥有非加密存储器，并且希望对其进行加密，那么需要创建新卷，然后移动数据。有关更多信息，请参阅[在已升级的数据中心内进行文件存储器迁移](/docs/infrastructure/FileStorage?topic=FileStorage-migratestorage)
{:important}
