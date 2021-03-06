---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

keywords: File Storage, file storage, NFS, snapshots, snapshot schedule, manual snapshot, snapshot space, snapshot quota

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}


# スナップショットの管理
{: #managingSnapshots}

## スナップショット・スケジュールの作成

スナップショット・スケジュールを使用して、ストレージ・ボリュームのポイント・イン・タイム・リファレンスを作成する頻度と時間を決定します。 ストレージ・ボリュームごとに最大 50 個のスナップショットを作成できます。 スケジュールは、[{{site.data.keyword.slportal}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/){:new_window}の**「ストレージ」**>**「{{site.data.keyword.filestorage_short}}」**タブで管理します。

ストレージ・ボリュームの初期プロビジョニング時にスナップショット・スペースを購入していなかった場合は、初期スケジュールをセットアップする前に、まず購入する必要があります。
{:important}

### スナップショット・スケジュールの追加
{: #addschedule}

スナップショット・スケジュールは、時間単位、日単位、週単位の間隔で、それぞれに異なる保持サイクルを指定してセットアップできます。 スナップショットの最大限度はストレージ・ボリュームごとに 50 個で、時間単位、日単位、週単位のスケジュールや手動スナップショットを混在させることができます。

1. ストレージ・ボリュームをクリックして、**「アクション」**をクリックし、**「スナップショットのスケジュール」**をクリックします。
2. 「新規スナップショット・スケジュール」ウィンドウでは、3 つの異なるスナップショットの頻度から選択できます。 3 つの頻度を任意に組み合わせて使用し、包括的なスナップショット・スケジュールを作成します。
   - 時間単位
      - スナップショットを毎時何分に取得するかを指定します。 デフォルトは現在の分です。
      - 最も古いスナップショットが破棄されるまで保持する毎時スナップショットの数を指定します。
   - 日単位
      - スナップショットを何時何分に取得するかを指定します。 デフォルトは現在の時間と分です。
      - 最も古いスナップショットが破棄されるまで保持する毎時スナップショットの数を選択します。
   - 週単位
      - スナップショットを何曜日の何時何分に取得するかを指定します。 デフォルトは現在の曜日、時間、分です。
      - 最も古いスナップショットが破棄されるまで保持する週次スナップショットの数を選択します。
3. **「保存」**をクリックして、異なる頻度の別のスケジュールを作成します。 スケジュールされたスナップショットの総数が 50 を超えると、警告メッセージが表示され、保存できません。

スナップショットが**「詳細」**ページの**「スナップショット」**セクションに取り込まれると、それらのリストが表示されます。

SLCLI で以下のコマンドを使用してスナップショット・スケジュールのリストを表示することもできます。
```
# slcli file snapshot-schedule-list --help
Usage: slcli file snapshot-schedule-list [OPTIONS] VOLUME_ID

  Lists snapshot schedules for a given volume

Options:
  -h, --help  Show this message and exit.
```

## 手動スナップショットの取得

手動スナップショットは、アプリケーションのアップグレードまたは保守の際に、さまざまな時点で取得できます。 また、アプリケーション・レベルで一時的に非アクティブ化した複数のサーバーにわたってスナップショットを取得できます。

ストレージ・ボリュームごとの手動スナップショットの最大限度は 50 個です。

1. ストレージ・ボリュームをクリックします。
2. **「アクション」**をクリックします。
3. **「手動スナップショットの取得」**をクリックします。
スナップショットが取得され、**「詳細」**ページの**「スナップショット」**セクションに表示されます。 そのスケジュールは手動として表示されます。

代わりの方法として、SLCLI で以下のコマンドを使用してスナップショットを作成することができます。
```
# slcli file snapshot-create --help
Usage: slcli file snapshot-create [OPTIONS] VOLUME_ID

Options:
  -n, --notes TEXT  Notes to set on the new snapshot
  -h, --help        Show this message and exit.
```

## すべてのスナップショットとそのスペース使用情報のリスト表示および管理機能

保存されているスナップショットのスペース使用量のリストは、**「詳細」**ページ (**「ストレージ」**、**「{{site.data.keyword.filestorage_short}}」**) で参照できます。 管理機能 (スケジュールの編集とスペースの追加) は、この「詳細」ページのさまざまなセクションにある**「アクション」**メニューまたはリンクを使用して実行します。

代わりの方法として、SLCLI でこのタスクを実行できます。
```
# slcli file snapshot-list --help
Usage: slcli file snapshot-list [OPTIONS] VOLUME_ID

Options:
  --sortby TEXT   Column to sort by
  --columns TEXT  Columns to display. Options: id, name, created, size_bytes
  -h, --help      Show this message and exit.
```

## 保存されているスナップショットのリスト表示

保存されているスナップショットは、スケジュールのセットアップ時に**「保持する最新の件数」**フィールドに入力した数に基づいています。 **「スナップショット」**セクションで、取得されたスナップショットを表示できます。 スナップショットは、スケジュール別にリストされます。

## 使用されているスナップショット・スペースの量の表示

**「詳細」**ページ上部の円グラフに、使用済みのスペースの量と残りのスペースの量が表示されます。 スペースしきい値 (75%、90%、95%) に達すると、通知を受け取ります。

## ボリューム用のスナップショット・スペースの量の変更

スナップショット・スペースがこれまでなかったボリュームや、追加のスナップショット・スペースが必要なボリュームに、スナップショット・スペースを追加する必要がある場合があります。 必要に応じて、5 GB から 4,000 GB を追加できます。

スナップショット・スペースは増やすことだけができます。 減らすことはできません。 必要なスペース量を判断できるまで、少量のスペースを選択することができます。 自動スナップショットと手動スナップショットはスペースを共有することに注意してください。
{:important}

スナップショット・スペースは、**「ストレージ」** > **「{{site.data.keyword.filestorage_short}}」**で変更できます。

1. ストレージ・ボリュームをクリックして、**「アクション」**をクリックし、**「スナップショット・スペースの追加」**をクリックします。
2. プロンプトで、サイズの範囲から選択します。 サイズの範囲は通常、0 からボリュームのサイズまでです。
3. **「次へ進む (Continue)」**をクリックします。
4. プロモーション・コードがある場合は入力し、**「再計算」**をクリックします。 「この注文の課金」フィールドと「注文の検討」フィールドは、デフォルトで入力されています。
5. **「マスター・サービス契約を読み…」**チェック・ボックスをクリックし、**「注文する」**をクリックします。 追加されたスナップショット・スペースが数分後にプロビジョンされます。

## スナップショット・スペースの限界に達してスナップショットが削除されるときに通知を受け取る

3 つの異なるスペースしきい値 (75%、90%、および 95%) に達すると、アカウントのマスター・ユーザーにサポート・チケットから通知が送信されます。

- **容量の 75%** では、スナップショット・スペースの使用率が 75% を超えたことを示す警告が送信されます。 警告に従い、手動でスペースを追加するか、保存されている不要なスナップショットを削除すると、そのアクションが認識されて、チケットはクローズされます。 何も行わない場合は、チケットに手動で応答してからクローズする必要があります。
- **容量の 90%** では、スナップショット・スペースの使用率が 90% を超えると、2 番目の警告が送信されます。 75% の容量に達したときと同様に、使用スペースを減らすために必要なアクションを実行すると、そのアクションが認識されて、チケットはクローズされます。 何も行わない場合は、チケットに手動で応答してからクローズする必要があります。
- **容量の 95%** では、最終警告が送信されます。 スペース使用率がしきい値を下回るようなアクションを実行しなかった場合は、通知が生成され、今後もスナップショットを作成できるよう、自動削除が実行されます。 スケジュールで取得されたスナップショットが削除されます。最も古いものから始まり、使用率が 95% を下回るまで続けられます。 スナップショットは、使用率が 95% を超えるたび、使用率がしきい値を下回るまで削除が続行されます。 スペースが手動で増やされるか、スナップショットが削除されると、警告はリセットされ、再びしきい値を超えた場合に再び発行されます。 アクションが実行されない場合は、この通知が、受信する唯一の警告になります。

## スナップショット・スケジュールの削除

スナップショット・スケジュールは、**「ストレージ」**>**「{{site.data.keyword.filestorage_short}}」**でキャンセルできます。

1. **「詳細」**ページの**「スナップショットのスケジュール」**フレームで、削除するスケジュールをクリックします。
2. 削除するスケジュールの横にあるチェック・ボックスをクリックして、**「保存」**をクリックします。<br />

レプリケーション機能を使用している場合は、削除するスケジュールがレプリケーションで使用されるスケジュールでないことを確認してください。 レプリケーション・スケジュールの削除について詳しくは、[ここ](/docs/infrastructure/FileStorage?topic=FileStorage-replication)を参照してください。
{:important}

## スナップショットの削除

不要になったスナップショットを手動で削除して、今後のスナップショット用にスペースを解放することができます。 削除は、**「ストレージ」**>**「{{site.data.keyword.filestorage_short}}」**で行います。

1. ストレージ・ボリュームをクリックし、**「スナップショット」**セクションまでスクロールして既存のスナップショットのリストを確認します。
2. 特定のスナップショットの隣にある**「アクション」**をクリックし、**「削除」**をクリックしてスナップショットを削除します。 スナップショット間に依存関係はないため、この削除によって同じスケジュールによる将来または過去のスナップショットが影響を受けることはありません。

代わりの方法として、SLCLI でスナップショットを削除できます。
```
# slcli file snapshot-delete --help
Usage: slcli file snapshot-delete [OPTIONS] SNAPSHOT_ID

Options:
  -h, --help  Show this message and exit.
```

ポータル内の手動で削除されなかった手動スナップショットは、スペースの制限に達すると自動的に (古いものから順に) 削除されます。
{:note}

## スナップショットを使用してストレージ・ボリュームを特定時点にリストアする

ユーザー・エラーやデータ破損が原因で、ストレージ・ボリュームを特定時点に戻す必要がある場合があります。

1. ストレージ・ボリュームをホストからアンマウントして切り離します。
   - [ここ](/docs/infrastructure/FileStorage?topic=FileStorage-mountingLinux)をクリックすると説明が表示されます。
2. [{{site.data.keyword.slportal}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/){:new_window}で、**「ストレージ」**、**「{{site.data.keyword.filestorage_short}}」**をクリックします。
3. スクロールダウンして、リストアするボリュームをクリックします。 **「詳細」**ページの**「スナップショット」**セクションに、保存されているすべてのスナップショットのサイズと作成日のリストが表示されます。
4. 使用するスナップショットの横の**「アクション」**をクリックし、**「リストア」**をクリックします。 <br/>

   復元を完了すると、スナップショットが作成された後に作成または変更されたデータは失われます。 このデータ損失は、ストレージ・ボリュームがスナップショット取得時と同じ状態に戻るために発生します。
   {:note}
5. リストアを開始するには、**「はい」**をクリックします。

   選択したスナップショットを使用してボリュームがリストアされることを示すメッセージが、ページに表示されます。 また、{{site.data.keyword.filestorage_short}} のボリュームの横に、アクティブ・トランザクションが進行中であることを示すアイコンが表示されます。 アイコン上にカーソルを移動すると、トランザクションを示すウィンドウが表示されます。 トランザクションが完了すると、アイコンは消えます。
   {:note}
6. ストレージ・ボリュームをホストにマウントして再接続します。
  - [ここ](/docs/infrastructure/FileStorage?topic=FileStorage-mountingLinux)をクリックすると説明が表示されます。

代わりの方法として、SLCLI でスナップショットを使用してボリュームを復元することができます。
```
# slcli file snapshot-restore --help
Usage: slcli file snapshot-restore [OPTIONS] VOLUME_ID

Options:
  -s, --snapshot-id TEXT  The id of the snapshot which will be used to restore
                          the block volume
  -h, --help              Show this message and exit.
```  

ボリュームを復元すると、復元に使用されたスナップショットの後に実行されたすべてのスナップショットが削除されます。
{:important}
