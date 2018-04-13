---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 訂購及管理 {{site.data.keyword.filestorage_full_notm}}

根據需求及喜好設定，您可以佈建兩種不同類型的儲存空間。{{site.data.keyword.filestorage_short}} 磁區的兩個選項如下：

- **耐久性**：佈建「耐久性」層級，其特色是預先定義的效能層次，以及例如 Snapshot 及抄寫等特性。
- **效能**：建置您可以配置所需每秒輸入/輸出作業 (IOPS) 的高功率「效能」環境。

## 佈建 {{site.data.keyword.filestorage_short}}

### 如何訂購 {{site.data.keyword.filestorage_short}} 的耐久性

1. 從 [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window} 中，按一下**儲存空間** > **{{site.data.keyword.filestorage_short}}**，或者，從「{{site.data.keyword.BluSoftlayer_full}} 型錄」中，按一下**基礎架構** > **儲存空間** > **{{site.data.keyword.filestorage_short}}**。
2. 按一下畫面右上角的**訂購 {{site.data.keyword.filestorage_short}}**。 
3. 從**選取儲存空間類型**下拉清單中，選取**耐久性**。
4. 按一下**位置**下拉清單，然後選取資料中心。
   - 確定將新的「儲存空間」新增至與先前訂購的主機相同的位置。
   - 如果您已選取具有改良功能的資料中心（在下拉清單中會以 * 表示），則可以選擇「每月計費」或「每小時計費」。 
     1. 使用**每小時**計費，計算檔案磁區在刪除磁區或計費週期結束時（看何者為先）該檔案磁區存在於帳戶上的小時數。如果儲存空間使用期間為幾天或不到一整個月，則每小時計費是一個良好的選擇。每小時計費只適用於這些[精選資料中心](new-ibm-block-and-file-storage-location-and-features.html)內所佈建的儲存空間。 
     2. 使用**每月**計費，價格是從建立日期到計費週期結束按比例計算，並立即計費。如果在計費週期結束之前刪除檔案磁區，並不會退款。如果儲存空間用於正式作業工作負載，而正式作業工作負載使用需要長期（一個月或更久）儲存及存取的資料，則每月計費是一個良好的選擇。**附註**：依預設，如果儲存空間佈建在未使用改良功能更新的資料中心內，則會使用每月計費類型。
5. 選取應用程式的儲存空間層次：
    - **每 GB 0.25 IOPS** 是為了低 I/O 強度的工作負載而設計。這些工作負載的特點通常是在給定時間會有大百分比的非作用中資料。應用程式範例包括儲存信箱或部門層次檔案共用。
    - **每 GB 2 IOPS** 是為了最通用用途而設計。應用程式範例包括管理支持小型資料庫的 Web 應用程式或 Hypervisor 的虛擬機器磁碟映像檔。
    - **每 GB 4 IOPS** 是為了較高強度工作負載而設計。這些工作負載的特點通常是在給定時間會有高百分比的作用中資料。應用程式範例包括交易式資料庫及其他效能相關的資料庫。
    - **每 GB 10 IOPS** 是為了最嚴苛的工作負載（例如 NoSQL Database 所建立的工作負載）以及進行分析的資料處理而設計。此層級適用於[精選資料中心](new-ibm-block-and-file-storage-location-and-features.html)內大小最多佈建 4TB 的儲存空間。
6. 從下拉清單中，選取**可用的儲存空間大小**。
7. 從下拉清單中，選擇 **Snapshot 空間大小**（除了可用的空間之外）。
8. 按一下**繼續**。您會看到每月及按比例分配的費用，並且會有最後一次機會檢閱訂單詳細資料。
9. 按一下**我已閱讀主要服務合約**勾選框，然後按一下**下訂單**。
10. 在幾分鐘之後，應該就可以使用您的新儲存空間配置。

**附註**：依預設，您可以佈建總計 250 個 {{site.data.keyword.blockstorageshort}} 磁區。若要增加磁區數目，請與業務代表聯絡。請在[這裡](managing-storage-limits.html)閱讀增加限制的相關資訊。

如需同時授權的限制，請參閱[常見問題](File-Storage-FAQ.html)

### 如何訂購 {{site.data.keyword.filestorage_short}} 的效能

1. 從 [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window} 中，按一下**儲存空間**、**{{site.data.keyword.filestorage_short}}**，或者，從「{{site.data.keyword.BluSoftlayer_full}} 型錄」中，按一下**基礎架構** > **儲存空間** > **{{site.data.keyword.filestorage_short}}**。
2. 按一下畫面右上角的**訂購 {{site.data.keyword.filestorage_short}}**。 
3. 從「選取儲存空間類型」下拉清單中，選取**效能**。
4. 按一下**位置**下拉清單，然後選取資料中心。
    -  確定將新的「儲存空間」新增至與先前訂購的主機相同的位置。
    -  如果您已選取具有改良功能的資料中心（在下拉清單中會以 * 表示），則可以選擇「每月計費」或「每小時計費」。 
       1.  使用**每小時**計費，計算檔案磁區在刪除磁區或計費週期結束時（看何者為先）該檔案磁區存在於帳戶上的小時數。如果儲存空間使用期間為幾天或不到一整個月，則每小時計費是一個良好的選擇。每小時計費只適用於這些精選資料中心內所佈建的儲存空間。 
       2. 使用**每月**計費，價格是從建立日期到計費週期結束按比例計算，並立即計費。如果在計費週期結束之前刪除檔案磁區，並不會退款。如果儲存空間用於正式作業工作負載，而正式作業工作負載使用需要長期（一個月或更久）儲存及存取的資料，則每月計費是一個良好的選擇。**附註**：依預設，如果儲存空間佈建在未使用改良功能更新的資料中心內，則會使用每月計費類型。  
5. 選取適當**儲存空間大小**旁的圓鈕。
6. 在**指定 IOPS** 欄位中，輸入 IOPS。
7. 按一下**繼續**。您會看到每月及按比例分配的費用，並且會有最後一次機會可檢閱訂單詳細資料。如果您要變更訂單，請按**上一步**。
8. 按一下**我已閱讀主要服務合約**勾選框，然後按一下**下訂單**。
9. 在幾分鐘之後，應該就可以使用您的新儲存空間配置。

**附註**：依預設，您可以佈建總計 250 個 {{site.data.keyword.blockstorageshort}} 磁區。若要增加磁區數目，請與業務代表聯絡。請在[這裡](managing-storage-limits.html)閱讀增加限制的相關資訊。

如需同時授權的限制，請參閱[常見問題](File-Storage-FAQ.html)

## 管理 {{site.data.keyword.filestorage_short}}

### 如何授權主機存取 {{site.data.keyword.filestorage_short}}

「授權」主機是已獲得特定磁區存取權的主機。如果沒有主機授權，就無法從系統中存取或使用儲存空間。授權主機存取您的磁區，會產生「使用者名稱」及「密碼」。 

**附註**：您只能授權及連接與儲存空間位於相同資料中心的主機。如果您有多個帳戶，則無法授權某個帳戶的主機存取您在另一個帳戶上的儲存空間。 

1. 按一下**儲存空間** > **{{site.data.keyword.filestorage_short}}**，然後按一下**磁區名稱**。
2. 捲動至頁面的**授權主機**區段。
3. 按一下頁面右側的**授權主機**鏈結。選取可存取該特定磁區的主機。

 

### 如何檢視授權存取 {{site.data.keyword.filestorage_short}} 磁區的主機清單

使用下列步驟，以檢視授權存取磁區的主機清單。

1. 按一下**儲存空間 > {{site.data.keyword.filestorage_short}}**，然後按一下**磁區名稱**。
2. 向下捲動至頁面底端的**授權主機**區段。

在這裡，您會看到目前已獲授權存取磁區的主機清單。


### 如何檢視已授權主機存取的 {{site.data.keyword.filestorage_short}} 磁區

您可以檢視主機可存取的磁區，包括建立連線所需的資訊 - 「磁區名稱」、「儲存空間類型」、「目標位址」、容量及位置：

1. 從 [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window} 中按一下**裝置** > **裝置清單**，然後按一下適當的裝置。
2. 選取「儲存空間」標籤。

然後，會出現此特定主機可存取的儲存空間磁區清單，這些儲存空間磁區全部是依儲存空間類型（區塊、檔案、其他）分組。從個別的**動作**功能表中，您可以授權其他儲存空間，或移除存取權。

 

### 如何裝載及卸載 {{site.data.keyword.filestorage_short}}

您可以使用**磁區詳細資料**視圖中所提供的裝載點資訊，從主機裝載 {{site.data.keyword.filestorage_short}}。

請參閱下列文章，其中包含從主機裝載及卸載 {{site.data.keyword.filestorage_short}} 的詳細資料：[存取 Linux 上的 {{site.data.keyword.filestorage_short}}](accessing-file-storage-linux.html)

 

### 如何撤銷主機對 {{site.data.keyword.filestorage_short}} 的存取權

如果您要停止主機對特定儲存空間磁區的存取權，則可以撤銷存取權。撤銷存取權時，將會捨棄與磁區的主機連線，而且作業系統及應用程式都將無法與磁區通訊。 

**附註：**若要避免主機端問題，請先卸載您作業系統的儲存空間磁區，然後再撤銷存取權，以避免遺漏磁碟機或資料毀損。

您可以從「裝置清單」或「儲存空間」視圖中，撤銷「儲存空間」的存取權。

#### 如何從「裝置清單」撤銷存取權：

1. 從 [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window} 中按一下**裝置** > **裝置清單**，然後按兩下適當的裝置。
2. 選取**儲存空間**標籤。
3. 然後，會出現此特定主機可存取的儲存空間磁區清單，這些儲存空間磁區全部是依儲存空間類型（區塊、檔案、其他）分組。選取您要撤銷其存取權之磁區旁的個別**動作**功能表，然後按一下**撤銷存取權**。
4. 系統將會詢問您是否要撤銷磁區的存取權，因為此動作無法復原。按一下**是**來撤銷磁區存取權，或按一下**否**來取消動作。

**附註：**如果您要中斷多個磁區與特定主機的連線，則需要對每一個磁區重複「撤銷存取權」動作。

 

#### 如何從「儲存空間視圖」撤銷存取權：
1. 按一下**儲存空間、{{site.data.keyword.filestorage_short}}**，然後選取您要從中撤銷存取權的**磁區**。
2. 向下捲動至頁面的**授權主機**區段。
3. 按一下要撤銷其存取權之主機旁邊的**動作**下拉箭頭，然後選取**撤銷存取權**。
4. 系統將會詢問您是否要撤銷磁區的存取權，因為此動作無法復原。按一下**是**來撤銷磁區存取權，或按一下**否**來取消動作。

**附註：**如果您要中斷多台主機與特定磁區的連線，則需要對每一台主機重複「撤銷存取權」動作。

 

### 如何取消儲存空間磁區

如果您不再需要特定磁區，則可以取消它。為了取消儲存空間磁區，您需要先撤銷任何主機的存取權。

1. 按一下**儲存空間** > **{{site.data.keyword.filestorage_short}}**。
2. 按一下要取消之磁區的**動作**下拉箭頭，然後選取**取消 {{site.data.keyword.filestorage_short}}**。
3. 系統將詢問您是要立即取消磁區，還是在佈建磁區的週年日取消磁區。按一下**繼續**或**關閉**。**附註**：如果您選取在其週年日取消磁區的選項，則可以在其週年日之前使取消要求失效。
4. 按一下確認通知勾選框，然後按一下**確認**。

 

### 如何查看已佈建的 {{site.data.keyword.filestorage_short}} 磁區詳細資料

您可以檢視所選取儲存空間磁區的重要資訊摘要（包括已新增至儲存空間的其他 Snapshot 及抄寫功能）。

1. 按一下**儲存空間** > **{{site.data.keyword.filestorage_short}}**。
2. 從清單中，按一下適當的**磁區名稱**。

### 如何在發票上識別 {{site.data.keyword.filestorage_short}} 磁區

所有磁區在發票上都會顯示為一個行項目；「耐久性」將顯示為「耐久性儲存空間服務」，而「效能」將顯示為「效能儲存空間服務」。根據您的儲存空間層次，速率會不同。您可以展開「耐久性」或「效能」，即可看到它是 {{site.data.keyword.filestorage_short}} 磁區。