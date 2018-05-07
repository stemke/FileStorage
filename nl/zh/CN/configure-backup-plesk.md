---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
 
# 使用 Plesk 配置 {{site.data.keyword.filestorage_short}} 进行备份

在本文中，我们的目的是提供有关在 Plesk 中配置 {{site.data.keyword.blockstoragefull}} 进行备份的指示信息。假定以 root 用户或 sudo 用户身份通过 SSH 登录到系统，并且有完整的管理级别 Plesk 访问权。此示例基于 CentOS7 主机。

**注**：您可以在[此处](https://docs.plesk.com/en-US/12.5/administrator-guide/backing-up-and-restoration.59256/){:new_window}找到 Plesk 文档中有关备份和复原的内容。

1. 通过 SSH 连接主机。

2. 确保安装点目标已存在。<br />
   **注**：Plesk 有两个备份存储选项，一个是内部 Plesk 存储器（位于 Plesk 服务器上的备份存储器），另一个是外部 FTP 存储器（位于 Web 或本地网络中某个外部服务器上的备份存储器）。通常在 Plesk 框中，内部备份存储在 `/var/lib/psa/dumps` 中，并使用
`/tmp` 作为临时目录。在示例中，我们使临时目录保持为本地目录，但将转储目录移至 STaaS 目标 (`/backup/psa/dumps`)。不需要 FTP 用户凭证。
   
3. 如[在 Red Hat Enterprise Linux 上访问 {{site.data.keyword.filestorage_short}}](accessing-file-storage-linux.html) 和[在 CentOS 中安装 NFS/{{site.data.keyword.filestorage_short}}](mounting-nsf-file-storage.html) 中所述，配置 {{site.data.keyword.filestorage_short}}。确保将其安装到 `/backup` 并且在
`/etc/fstab` 中对其进行配置，以启用引导时安装。<br />
   **注**：缺省情况下，NFS 会将使用 root 用户许可权创建的任何文件自动降级为供 nobody 用户访问。要允许 root 用户客户机保留对 NFS 共享的 root 用户许可权，应该将 `no_root_squash` 添加到 `/etc/exports`。<br />
   **注**：我们还提供了[在 CoreOS 上安装 NFS/{{site.data.keyword.filestorage_short}}](mounting-storage-coreos.html) 的指示信息。<br />

4. **可选**：将现有备份复制到新存储器。例如，使用 `rsync`：
   ```
   rsync -avz /var/lib/psa/dumps /backup/psa/dumps
   ```
   {: pre}
    
    **注**：此命令传输压缩的数据以尽可能保留最多的数据（硬链接除外），同时提供有关所传输文件的信息并在结束时提供简短摘要。
    
5. 编辑 `/etc/psa/psa.conf` 以指向新目标上的 `DUMP_D` 值。 
    -  应该显示为：`DUMP_D /backup/psa/dumps`。 

6. **可选**：根据特定用例和业务需求的指示，从服务器中除去旧存储器并从帐户中取消该存储器。
