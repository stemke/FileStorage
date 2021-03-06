---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

keywords: File Storage, file storage, NFS, disaster recovery, duplicate volume, replica volume, failover, failback,

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}

# 灾难恢复 - 通过可访问的主卷进行故障转移
{: #dr-accessible}

如果主站点上发生灾难性故障或状况，但主存储器仍可访问，客户可以执行以下操作，以快速访问辅助站点上的数据。

在启动故障转移之前，确保所有主机授权已就位。

已授权的主机和卷必须位于同一数据中心内。例如，您不能使副本卷位于伦敦，而使主机位于阿姆斯特丹。副本卷和主机必须都位于伦敦，或者都位于阿姆斯特丹。
{:note}

1. 登录到 [{{site.data.keyword.cloud}} 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/catalog){:new_window}，然后单击左上角的**菜单**图标。选择**经典基础架构**。


   或者，您可以登录到 [{{site.data.keyword.slportal}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){:new_window}。
1. 在 **{{site.data.keyword.filestorage_short}}** 页面中，单击源卷或目标卷。
2. 单击**副本**。
3. 向下滚动到**授权主机**框架，然后单击右侧的**授权主机**。
4. 突出显示要授权执行复制的主机。要选择多个主机，请按住 CTRL 键的同时单击适用的主机。
5. 单击**提交**。如果您没有主机，那么系统将提示您购买同一数据中心内的计算资源。

## 启动从卷到其副本的故障转移

如果发生故障事件，可以启动到目标卷的**故障转移**。目标卷会变为活动状态。最后一个成功复制的快照会激活，并且该卷会变为可用于安装。自上一个复制周期以来写入源卷的所有数据都会丢失。启动故障转移后，复制关系会翻转。目标卷成为源卷，原先的源卷会变成目标卷，以 **LUN 名称**后跟 **REP** 来指示。

故障转移在 [[{{site.data.keyword.slportal}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){:new_window} 中的**存储**、**{{site.data.keyword.filestorage_short}}** 下启动。

继续执行这些步骤之前，请先断开该卷的连接。否则会导致数据损坏和丢失。
{:important}

1. 单击活动卷（“源”）。
2. 单击右上角的**副本**，然后单击**操作**。
3. 选择**故障转移**。


   应该会收到一条消息，声明正在进行故障转移。此外，**{{site.data.keyword.filestorage_short}}** 上的相应卷旁边会显示一个图标，指示正在执行活动事务。将鼠标悬停在该图标上将生成一个用于显示事务的窗口。事务完成后，该图标会消失。在故障转移过程中，与配置相关的操作为只读。无法编辑任何快照安排，也无法更改快照空间。该事件将记录在复制历史记录中。
   <br/> 目标卷处于活动状态时，您将收到另一条消息。原始源卷的“LUN 名称”更新为以“REP”结尾，并且其状态将变为“不活动”。
   {:note}
4. 单击**查看所有 ({{site.data.keyword.filestorage_short}})**。
5. 单击活动卷（原先的目标卷）。现在，此卷的状态为**活动**。
6. 安装存储卷并将其连接到主机。单击[此处](/docs/infrastructure/FileStorage?topic=FileStorage-orderingConsole)以获取指示信息。


## 启动从卷到其副本的故障恢复

修复原始源卷后，可以启动到原始源卷的受控故障恢复。在受控故障恢复中，

- 执行操作的源卷变为脱机状态，
- 生成快照，
- 完成复制周期，
- 激活刚才生成的数据快照，
- 并使源卷变为活动状态以供安装。

启动故障恢复后，复制关系会再次翻转。原来的源卷会复原为源卷，原来的目标卷将再次成为目标卷，以 **LUN 名称**后跟 **REP** 来指示。

故障恢复在 [{{site.data.keyword.slportal}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){:new_window} 中的**存储**、**{{site.data.keyword.filestorage_short}}** 下启动。

1. 单击活动卷（“目标”）。
2. 单击右上角的**副本**，然后单击**操作**。
3. 选择**故障恢复**。

   应该会收到一条消息，说明正在进行故障恢复。此外，**{{site.data.keyword.filestorage_short}}** 上的相应卷旁边会显示一个图标，指示正在执行活动事务。将鼠标悬停在该图标上将生成一个用于显示事务的窗口。事务完成后，该图标会消失。在故障恢复过程中，与配置相关的操作为只读。无法编辑任何快照安排，也无法更改快照空间。该事件将记录在复制历史记录中。
   {:note}
4. 单击右上角的**查看所有 {{site.data.keyword.filestorage_short}}** 链接。
5. 单击活动卷（“源”）。
6. 安装存储卷并将其连接到主机。单击[此处](/docs/infrastructure/FileStorage?topic=FileStorage-orderingConsole)以获取指示信息。
