---

copyright:
  years: 2014, 2019
lastupdated: "2019-03-08"

keywords: File Storage, file storage, NFS, mounting volume in Container Linux, CoreOS

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:codeblock: .codeblock}


# Container Linux への {{site.data.keyword.filestorage_short}} のマウント
{: #mountingCoreOS}

Container Linux by CoreOS は、Linux カーネルに基づく、オープン・ソースの軽量オペレーティング・システムです。 これはクラスター化されたデプロイメントにインフラストラクチャーを提供するように設計されています。 Container Linux は、オペレーティング・システムとして、ソフトウェア・コンテナー内にアプリケーションをデプロイするために必要な最小限の機能と、サービス・ディスカバリーと構成共有用の組み込みメカニズムを備えています。 詳しくは、[Mounting storage ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://coreos.com/os/docs/latest/mounting-storage.html) を参照してください

システム・レベルのマウントは読み取り専用のディレクトリーに入っているため、2 次マウント・ファイルはすべて `/etc/systemd/system` ディレクトリーに入れます。 まず、`MOUNTPOINT.mount` ファイルを作成する必要があります。 この `.mount` ファイルの **Where** セクションはファイル名と一致しなければなりません。 マウント・ポイントが `/` の直下にない場合は、`path-to-mount.mount` という構文を使用してファイルに名前を付ける必要があります。 例えば、ポータブル・ストレージ・ドライブを `/mnt/www` にマウントする場合は、`mnt-www.mount` という名前をファイルに付けます。

パーティションを作成するときには、`fdisk` または `parted` を使用できます。 作成するファイル・システムは、`.mount` ファイルにリストされているものと一致するようにしてください。そうしないと、サービスは開始に失敗します。マウントが NFS なので、マウント・ファイルで `Options=` 行を使用して追加のオプションを指定できます。

次の例では、`/data/www` にマウントするように NFS を設定します。{{site.data.keyword.filestorage_short}}・インスタンスの NFS マウント・ポイントは、{{site.data.keyword.filestorage_short}}のリスト・ページから取得できます。また、API 呼び出し `SoftLayer_Network_Storage::getNetworkMountAddress()` を使用して取得することもできます。
{:tip}

```
$ cat data-www.mount
[Unit]
Description = Mount for Container Storage

[Mount]
What=<nfs_mount_point>
Where=/data/www
Type=nfs
Options=vers=3,sec=sys,noauto

[Install]
WantedBy = multi-user.target
```
{:codeblock}

次に、マウントを有効にして、適切にマウントされたことを確認します。

```
systemctl enable --now /etc/systemd/system/data-www.mount

cluster1 ~ # mount |grep data
<nfs_mount_point> on /data/www type nfs3 (rw,relatime,vers=3.0,rsize=65536,wsize=65536,namlen=255,hard,proto=tcp,port=0,timeo=600,retrans=2,sec=sys,clientaddr=10.81.x.x,local_lock=none,addr=10.1.x.x)
```
{:codeblock}

詳しくは、[`systemd mount` の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.freedesktop.org/software/systemd/man/systemd.mount.html) を参照してください
