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


# Montagem  {{site.data.keyword.filestorage_short}}  no CentOS
{: #mountingCentOS}

Para montar o {{site.data.keyword.filestorage_full}} no CentOS 7, deve-se autorizar o host primeiro por meio do [{{site.data.keyword.slportal}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){:new_window} ou por meio do SLCLI. Em seguida, instale os utilitários do NFS conforme descrito em [Montando o {{site.data.keyword.filestorage_short}} no Linux](/docs/infrastructure/FileStorage?topic=FileStorage-mountingLinux).

Para o CentOS, é possível especificar algumas opções adicionais usando a linha `Options=` no arquivo de montagem. No exemplo a seguir, o NFS está configurado para montagem em `/data/www`.

O ponto de montagem do NFS da instância do {{site.data.keyword.filestorage_short}} pode ser obtido por meio da página de listagem do {{site.data.keyword.filestorage_short}} ou por meio de uma chamada API - `SoftLayer_Network_Storage::getNetworkMountAddress()`.
{:tip}

```
$ cat data-www.mount [Unidade] Descrição = Montar para o armazenamento de contêiner

[Mount] What=<nfs_mount_point> Where=/data/www Type=nfs Options=vers=4,sec=sys,noauto

[Install] WantedBy = multi-user.target
```
{:codeblock}

Em seguida, ative a montagem e verifique se ela está montada de forma adequada.

```
systemctl enable --now /etc/systemd/system/data-www.mount

cluster1 ~ # mount |grep data <nfs_mount_point> on /data/www type nfs4 (rw,relatime,vers=4.0,rsize=65536,wsize=65536,namlen=255,hard,proto=tcp,port=0,timeo=600,retrans=2,sec=sys,clientaddr=10.81.x.x,local_lock=none,addr=10.1.x.x)
```
{:codeblock}
