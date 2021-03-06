---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-22"

keywords: File Storage, mounting file storage, Linux, CentOS, NFS

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:codeblock: .codeblock}


# Mounting {{site.data.keyword.filestorage_short}} in CentOS
{: #mountingCentOS}

To mount {{site.data.keyword.filestorage_full}} in CentOS 7, you must authorize the host first through the [{{site.data.keyword.slportal}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){:new_window} or through the SLCLI. Then, install the NFS utilities as described in [Mounting {{site.data.keyword.filestorage_short}} on Linux](/docs/infrastructure/FileStorage?topic=FileStorage-mountingLinux).

For CentOS, you can specify some additional options by using the `Options=` line in the mount file. In the following example, the NFS is set to mount at `/data/www`.

The NFS mount point of the {{site.data.keyword.filestorage_short}} instance can be obtained from the {{site.data.keyword.filestorage_short}} listing page or through an API call -`SoftLayer_Network_Storage::getNetworkMountAddress()`.
{:tip}

```
$ cat data-www.mount
[Unit]
Description = Mount for Container Storage

[Mount]
What=<nfs_mount_point>
Where=/data/www
Type=nfs
Options=vers=4,sec=sys,noauto

[Install]
WantedBy = multi-user.target
```
{:codeblock}

Next, enable the mount and check that it is mounted properly.

```
systemctl enable --now /etc/systemd/system/data-www.mount

cluster1 ~ # mount |grep data
<nfs_mount_point> on /data/www type nfs4 (rw,relatime,vers=4.0,rsize=65536,wsize=65536,namlen=255,hard,proto=tcp,port=0,timeo=600,retrans=2,sec=sys,clientaddr=10.81.x.x,local_lock=none,addr=10.1.x.x)
```
{:codeblock}
