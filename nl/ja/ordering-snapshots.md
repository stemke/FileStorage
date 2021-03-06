---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

keywords: File Storage, file storage, NFS, snapshot, ordering snapshot, snapshot space

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}


# スナップショットの注文
{: #ordering-snapshots}

ストレージ・ボリュームのスナップショットを自動または手動で作成するには、それらを保持するためのスペースを購入する必要があります。 最大でストレージ・ボリューム量までの容量を、(ボリュームを最初に購入するとき、または購入後に下記の手順を使用して) 購入できます。

## 注文するスナップショット・スペースの量の決定

一般的に、スナップショット・スペースの使用量は、以下の 2 つの主要な要因によって決まります。
- 時間の経過とともにアクティブなファイル・システムがどれだけ変更するか
- スナップショットの保存期間  

必要なスペース量は、**(変更率)** x **(データを保存する時間数/日数/週数/月数)** として計算します。  

最初のスナップショットは、アクティブなファイル・システム・ブロックを示すメタデータ (ポインター) のコピーに過ぎないので、使用するスペースはごくわずかです。
{:note}

多数の変更が加えられ、保存期間も長いボリュームには、変更率がそれほど高くなく、保存期間もそれほど長くないボリュームに比べて、多くのスペースが必要になります。 前者のタイプの例には、変更率の高いデータベースがあります。 後者のタイプの例には、VMware データ・ストアがあります。

500 GB の実際のデータの毎時スナップショットを 12 個保持し、各スナップショット間の変更率が 1% である場合、スナップショットは 60 GB になります。

*(5-GB の変更率) x (1 時間ごとのスナップショット 12 個) = (60 GB の使用スペース)*

一方、実際のデータが 500 GB で、毎時スナップショットを 12 個作成し、1 時間ごとの変更率が 10% である場合は、スナップショット・スペースの使用量は 600 GB になります。

*(50-GB の変更率) x (1 時間ごとのスナップショット 12 個) = (600 GB の使用スペース)*

したがって、必要なスナップショット・スペースの量を決定するときには、変更率を慎重に検討してください。 変更率によって、必要なスナップショット・スペースの量は大きく左右されます。 ボリュームのサイズが大きいと、変更の頻度も多くなりそうに思えます。 しかし、変更量が 5 GB のボリューム 500-GB と、変更量が 5 GB のボリューム 10-TB は、同じ量のスナップショット・スペースを使用します。

また、ほとんどのワークロードは、ボリュームが大きいほど、最初に確保しなければならないスペース量は少なくなります。 これは主に、データ効率が高くなるためと、環境のスナップショットの仕組みの特性によるものです。

## {{site.data.keyword.cloud_notm}} コンソールによるスナップショット・スペースの注文

1. [IBM Cloud コンソール](https://{DomainName}/){:new_window}にログインして、左上にあるメニュー・アイコンをクリックします。 **「クラシック・インフラストラクチャー」**を選択します。

   または、[{{site.data.keyword.slportal}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/){:new_window} にログインできます。
2. **「ストレージ」**>**「{{site.data.keyword.filestorage_short}}」**の手順でストレージにアクセスします。
3. 「スナップショット」フレームで**「スナップショット・スペースの変更」**をクリックします。
4. 必要なスペース量と支払方法を選択します。
5. **「次へ進む (Continue)」**をクリックします。
6. プロモーション・コードがある場合は入力し、**「再計算」**をクリックします。 **「この注文の課金」**と**「注文の検討」**には、デフォルト値が表示されます。

   注文の処理時に割引が適用されます。
   {:note}
7. **「マスター・サービス契約を読み、その契約条件に同意します」**ボックスにチェック・マークをつけ、**「注文する」**をクリックします。 スナップショット・スペースは数分後にプロビジョンされます。

## SLCLI によるスナップショット・スペースの注文

```
# slcli file snapshot-order --help
Usage: slcli file snapshot-order [OPTIONS] VOLUME_ID

Options:
  --capacity INTEGER    Size of snapshot space to create in GB  [required]
  --tier [0.25|2|4|10]  Endurance Storage Tier (IOPS per GB) of the file
                        volume for which space is ordered [optional, and only
                        valid for endurance storage volumes]
  --upgrade             Flag to indicate that the order is an upgrade
  -h, --help            Show this message and exit.
```
