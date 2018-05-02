---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 管理 {{site.data.keyword.filestorage_short}}

您可以透過 {{site.data.keyword.slportal}} 管理 {{site.data.keyword.filestorage_full}} 磁區。本文章提供大部分一般作業的指示。

## 如何授權主機存取 {{site.data.keyword.filestorage_short}}

「授權」主機是已獲得特定磁區存取權的主機。如果沒有主機授權，就無法從系統中存取或使用儲存空間。授權主機存取您的磁區，會產生「使用者名稱」及「密碼」。 

**附註**：您只能授權及連接與儲存空間位於相同資料中心的主機。如果您有多個帳戶，您無法授權某個帳戶的主機存取您在另一個帳戶上的儲存空間。 

1. 按一下**儲存空間** > **{{site.data.keyword.filestorage_short}}**，然後按一下**磁區名稱**。
2. 捲動至頁面的**授權主機**區段。
3. 按一下頁面右側的**授權主機**鏈結。選取可存取該特定磁區的主機。

 

## 如何檢視授權存取 {{site.data.keyword.filestorage_short}} 磁區的主機清單

使用下列步驟，以檢視授權存取磁區的主機清單。

1. 按一下**儲存空間 > {{site.data.keyword.filestorage_short}}**，然後按一下**磁區名稱**。
2. 向下捲動至頁面底端的**授權主機**區段。

在這裡，您會看到目前已獲授權存取磁區的主機清單。


## 如何檢視已授權主機存取的 {{site.data.keyword.filestorage_short}} 磁區

您可以檢視主機可存取的磁區，包括建立連線所需的資訊 - 「磁區名稱」、「儲存空間類型」、「目標位址」、容量及位置：

1. 從 [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window} 中按一下**裝置** > **裝置清單**，然後按一下適當的裝置。
2. 選取「儲存空間」標籤。

然後，會出現此特定主機可存取的儲存空間磁區清單，這些儲存空間磁區全部是依儲存空間類型（區塊、檔案、其他）分組。從個別的**動作**功能表中，您可以授權其他儲存空間，或移除存取權。

 

## 如何裝載及卸載 {{site.data.keyword.filestorage_short}}

您可以使用**磁區詳細資料**視圖中所提供的裝載點資訊，從主機裝載 {{site.data.keyword.filestorage_short}}。

請參閱下列文章，其中包含從主機裝載及卸載 {{site.data.keyword.filestorage_short}} 的詳細資料：[存取 Linux 上的 {{site.data.keyword.filestorage_short}}](accessing-file-storage-linux.html)

 

## 如何撤銷主機對 {{site.data.keyword.filestorage_short}} 的存取權

如果您要停止主機對特定儲存空間磁區的存取權，則可以撤銷存取權。撤銷存取權時，將會中斷與磁區的主機連線，而且作業系統及應用程式都將無法與磁區通訊。 

**附註：**若要避免主機端問題，請先卸載您作業系統的儲存空間磁區，然後再撤銷存取權，以避免遺漏磁碟機或資料毀損。

您可以從「裝置清單」中的「儲存空間」或從「儲存空間」視圖中，撤銷存取權。

### 如何從「裝置清單」撤銷存取權：

1. 從 [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window} 中按一下**裝置** > **裝置清單**，然後按兩下適當的裝置。
2. 選取**儲存空間**標籤。
3. 然後，會出現此特定主機可存取的儲存空間磁區清單，這些儲存空間磁區全部是依儲存空間類型（區塊、檔案、其他）分組。選取您要撤銷其存取權之磁區旁的個別**動作**功能表，然後按一下**撤銷存取權**。
4. 系統將會詢問您是否要撤銷磁區的存取權，因為此動作無法復原。按一下**是**來撤銷磁區存取權，或按一下**否**來取消動作。

**附註：**如果您要中斷多個磁區與特定主機的連線，則需要對每一個磁區重複「撤銷存取權」動作。

 

### 如何從「儲存空間」視圖撤銷存取權：
1. 按一下**儲存空間、{{site.data.keyword.filestorage_short}}**，然後選取您要從中撤銷存取權的**磁區**。
2. 向下捲動至頁面的**授權主機**區段。
3. 按一下要撤銷其存取權之主機旁邊的**動作**下拉箭頭，然後選取**撤銷存取權**。
4. 系統將會詢問您是否要撤銷磁區的存取權，因為此動作無法復原。按一下**是**來撤銷磁區存取權，或按一下**否**來取消動作。

**附註：**如果您要中斷多台主機與特定磁區的連線，則需要對每一台主機重複「撤銷存取權」動作。

 

## 如何取消儲存空間磁區

如果您不再需要特定磁區，則可以取消它。為了取消儲存空間磁區，您需要先撤銷任何主機的存取權。

1. 按一下**儲存空間** > **{{site.data.keyword.filestorage_short}}**。
2. 按一下要取消之磁區的**動作**下拉箭頭，然後選取**取消 {{site.data.keyword.filestorage_short}}**。
3. 系統將要求您確認要立即取消磁區，還是在佈建磁區的週年日取消磁區。按一下**繼續**或**關閉**。**附註**：如果您選取在其週年日取消磁區的選項，則可以在其週年日之前使取消要求失效。
4. 按一下確認通知勾選框，然後按一下**確認**。

 

## 如何查看已佈建的 {{site.data.keyword.filestorage_short}} 磁區詳細資料

您可以檢視所選取儲存空間磁區的重要資訊摘要（包括已新增至儲存空間的其他 Snapshot 及抄寫功能）。

1. 按一下**儲存空間** > **{{site.data.keyword.filestorage_short}}**。
2. 從清單中，按一下適當的**磁區名稱**。