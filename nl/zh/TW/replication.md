---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

keywords:

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}


# 抄寫資料
{: #replication}

抄寫使用您的其中一個 Snapshot 排程，自動將 Snapshot 複製到遠端資料中心內的目的地磁區。如果發生災難性事件，或者您的資料毀損，則可以在遠端網站中回復副本。

抄寫是將資料同步保留在兩個不同位置。如果您想要複製您的磁區，並與原始磁區分開使用，請參閱[建立重複的檔案磁區](/docs/infrastructure/FileStorage?topic=FileStorage-duplicatevolume)。
{:tip}

您必須先建立 Snapshot 排程，才能進行抄寫。{:important}


## 判斷已抄寫儲存空間磁區的遠端資料中心

{{site.data.keyword.BluSoftlayer_full}} 的資料中心已配對成全球主要與遠端組合。如需完整的資料中心可用性及抄寫目標清單，請參閱「表 1」。

<table>
  <caption style="text-align: left;"><p>表 1 - 此表格顯示每一個地區中具有加強功能的資料中心完整清單。每個地區都是一個個別的直欄。有些城市（例如「達拉斯」、「聖荷西」、「華盛頓特區」、「阿姆斯特丹」、「法蘭克福」、「倫敦」及「雪梨」）會有多個資料中心。</p>
  <p>&#42; 美國 1 地區中的「資料中心」沒有加強型儲存空間。具有加強型儲存空間功能之資料中心中的主機<strong>無法</strong>啟動在美國 1 資料中心有抄本目標的抄寫。</p>
  </caption>
  <thead>
    <tr>
      <th>美國 1 &#42;</th>
      <th>美國 2</th>
      <th>拉丁美洲</th>
      <th>加拿大</th>
      <th>歐洲</th>
      <th>亞太地區</th>
      <th>澳洲</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>DAL01<br />
DAL05<br />
	  DAL06<br />
	  HOU02<br />
	  SJC01<br />
	  WDC01<br />
	  <br /><br /><br /><br /><br /><br />
      </td>
      <td>SJC03<br />
	  SJC04<br />
	  WDC04<br />
	  WDC06<br />
	  WDC07<br />
	  DAL09<br />
	  DAL10<br />
	  DAL12<br />
	  DAL13<br />
	  <br /><br /><br />
      </td>
      <td>MEX01<br />
	  SAO01<br />
	  <br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
      </td>
      <td>TOR01<br />
MON01<br />
	  <br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
      </td>
      <td>AMS01<br />
	  AMS03<br />
	  FRA02<br />
	  FRA04<br />
	  FRA05<br />
	  LON02<br />
	  LON04<br />
	  LON05<br />
	  LON06<br />
	  OSL01<br />
	  PAR01<br />
	  MIL01<br />
      </td>
      <td>HKG02<br />
TOK02<br />
	  TOK04<br />
	  TOK05<br />
	  SNG01<br />
	  SEO01<br />
                                CHE01<br />
	  <br /><br /><br /><br /><br />
      </td>
      <td>SYD01<br />
SYD04<br />
          SYD05<br />
MEL01<br />
          <br /><br /><br /><br /><br /><br /><br /><br />
      </td>
    </tr>
  </tbody>
</table>

## 建立起始抄本

抄寫是根據 Snapshot 排程運作。您必須先有來源磁區的 Snapshot 空間及 Snapshot 排程，才能進行抄寫。如果您嘗試設定抄寫，但沒有適當的空間或排程，則系統會提示您購買更多空間，或設定排程。抄寫是在 [{{site.data.keyword.slportal}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){:new_window} 中的**儲存空間** > **{{site.data.keyword.filestorage_short}}** 下進行管理。

1. 按一下儲存空間磁區。
2. 按一下**抄本**，然後按一下**購買抄寫**。
3. 選取您要抄寫遵循的現有 Snapshot 排程。清單包含所有作用中的 Snapshot 排程。<br />

   您只能選取一個排程，即使是混合使用每小時、每日及每週。會抄寫自前次抄寫週期以來擷取到的所有 Snapshot，不論原始的排程為何。<br />如果您未設定 Snapshot，則會在訂購抄寫之前提示您這樣做。如需相關資訊，請參閱[使用 Snapshot](/docs/infrastructure/FileStorage?topic=FileStorage-snapshots)。
   {:tip}
3. 按一下**位置**，然後選取將成為您 DR 網站的資料中心。
4. 按一下**繼續**。
5. 如果您有**促銷代碼**，請輸入促銷代碼，然後按一下**重新計算**。依預設，會完成視窗中的其他欄位。

   折扣會在處理訂單時套用。
   {:note}
6. 按一下**我已閱讀主要服務合約...** 勾選框，然後按一下**下訂單**。


## 編輯現有抄寫

您可以從 [{{site.data.keyword.slportal}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){:new_window} 中，**儲存空間** > **{{site.data.keyword.filestorage_short}}** 下的**主要**或**抄本**標籤編輯抄寫排程，以及變更抄寫空間。


## 編輯抄寫排程

抄寫排程是以現有 Snapshot 排程為基礎。例如，若要將抄本排程從「每小時」變更為「每週」，您必須取消抄寫排程並設定新的排程。

變更排程可以在「主要」或「抄本」標籤上進行。

1. 在**主要**或**抄本**標籤上，按一下**動作**。
2. 選取**編輯 Snapshot 排程**。
3. 查看**排程**下的 **Snapshot** 頁框，以判定您要用於抄寫的排程。變更您要的排程。例如，如果您的抄寫排程是**每日**，則您可以變更進行抄寫的時間。
4. 按一下**儲存**。


## 變更抄寫空間

您的主要 Snapshot 空間與抄本空間必須相同。如果您在**主要**或**抄本**標籤上變更空間，則會自動將空間新增至來源及目的地資料中心。增加 Snapshot 空間也會觸發立即抄寫更新。

1. 在**主要**或**抄本**標籤上，按一下**動作**。
2. 選取**新增其他 Snapshot 空間**。
3. 從清單中選取儲存空間大小，然後按一下**繼續**。
4. 如果您有**促銷代碼**，請輸入促銷代碼，然後按一下**重新計算**。依預設，會完成對話框中的其他欄位。
5. 按一下**我已閱讀主要服務合約...** 勾選框，然後按一下**下訂單**。


## 在主要資料中心增加 Snapshot 空間時，會在抄本資料中心增加 Snapshot 空間

主要及抄本儲存空間磁區的磁區大小必須相同。其中一個不能大於另一個。當您增加主要磁區的 Snapshot 空間時，即會自動增加抄本空間。增加 Snapshot 空間會觸發立即抄寫更新。兩個磁區的增加量會在您的發票中顯示為明細行項目，並且視需要按比例分配。

如需增加 Snapshot 空間的相關資訊，請參閱 [Snapshot](/docs/infrastructure/FileStorage?topic=FileStorage-snapshots)。
## 檢視磁區清單中的抄本磁區

您可以在**儲存空間** > **{{site.data.keyword.filestorage_short}}** 的 {{site.data.keyword.filestorage_short}} 頁面上，檢視抄寫磁區。磁區名稱顯示主要磁區名稱，後面接著 REP。**類型**為「耐久性或效能 - 抄本」。**目標位址**為 N/A，因為抄本磁區未裝載在抄本資料中心，且**狀態**顯示「非作用中」。


## 在抄本資料中心檢視已抄寫磁區的詳細資料

您可以在**儲存空間** > **{{site.data.keyword.filestorage_short}}** 下的**抄本**標籤上，檢視抄本磁區詳細資料。另一個選項是從 **{{site.data.keyword.filestorage_short}}** 頁面中選取抄本磁區，然後按一下**抄本**標籤。


## 檢視抄寫歷程

在**管理**下的**帳戶**標籤上，在**審核日誌**上檢視抄寫歷程。主要及抄本磁區都會顯示相同的抄寫歷程，包括

- 抄寫的類型（失效接手或失效回復）、
- 起始時間
- 用於抄寫的 Snapshot、
- 抄寫的大小、
- 完成時間。


## 建立抄本的重複磁區

您可以建立現有 {{site.data.keyword.BluSoftlayer_full}} {{site.data.keyword.filestorage_full}} 的重複磁區。依預設，重複磁區會繼承原始儲存空間磁區的容量及效能選項，而且會有到達 Snapshot 中該時間點之前的資料副本。

您可以建立主要及抄本磁區的重複磁區。新的重複磁區會建立在與原始磁區相同的資料中心內。如果您建立抄本磁區的重複磁區，則新的磁區會建立在與抄本磁區相同的資料中心內。

佈建儲存空間之後，主機就可以存取重複磁區來進行讀寫。不過，除非從原始磁區到重複磁區的資料複製已完成，否則不容許進行 Snapshot 及抄寫。

如需相關資訊，請參閱[建立重複的檔案磁區](/docs/infrastructure/FileStorage?topic=FileStorage-duplicatevolume)

## 災難來襲時，使用抄本進行失效接手

當您失效接手時，您會將「開關」從主要資料中心的儲存空間磁區快速切換到遠端資料中心的目的地磁區。例如，您的主要資料中心是「倫敦」，而次要資料中心是「阿姆斯特丹」。如果發生故障事件，您會失效接手至「阿姆斯特丹」- 從「阿姆斯特丹」的運算實例連接至現行主要磁區。修復「倫敦」中的磁區之後，會擷取「阿姆斯特丹」磁區的 Snapshot，以從「倫敦」的運算實例失效回復至「倫敦」及那個再度成為主要磁區的磁區。

* 如果主要位置發生問題，但儲存空間和主機仍在線上，請參閱[使用可存取的主要磁區進行失效接手](/docs/infrastructure/FileStorage?topic=FileStorage-dr-accessible)。
* 如果主要位置已停機，請參閱[使用無法存取的主要磁區進行失效接手](/docs/infrastructure/FileStorage?topic=FileStorage-dr-inaccessible)。

## 取消現有抄寫

您可以立即或在週年日取消抄寫，這會導致計費結束。您可以從**主要**或**抄本**標籤中取消抄寫。

1. 從 **{{site.data.keyword.filestorage_short}}** 頁面，按一下磁區。
2. 在**主要**或**抄本**標籤上，按一下**動作**。
3. 選取**取消抄本**。
4. 選取要在何時取消。選擇**立即**或**週年日**，然後按一下**繼續**。
5. 按一下**我確認因為取消而可能發生資料流失**，然後按一下**取消抄本**。


## 取消主要磁區時取消抄寫

取消主要磁區時，即會刪除抄寫排程及抄本資料中心內的磁區。抄本是從 **{{site.data.keyword.filestorage_short}}** 頁面進行取消。

 1. 在 **{{site.data.keyword.filestorage_short}}** 頁面上，強調顯示磁區。
 2. 按一下**動作**，然後選取**取消 {{site.data.keyword.filestorage_short}}**。
 3. 選取要在何時取消磁區。選擇**立即**或**週年日**，然後按一下**繼續**。
 4. 按一下**我確認因為取消而可能發生資料流失**，然後按一下**取消**。

## SLCLI 中的抄寫相關指令
{: #clicommands}

* 列出適合於特定磁區的抄寫資料中心。
  ```
  # slcli file replica-locations --help
  Usage: slcli file replica-locations [OPTIONS] VOLUME_ID

  Options:
  --sortby TEXT   Column to sort by
  --columns TEXT  Columns to display. Options: ID, Long Name, Short Name
  -h, --help      Show this message and exit.
  ```

* 訂購檔案儲存空間抄本磁區。
  ```
  # slcli file replica-order --help
  Usage: slcli file replica-order [OPTIONS] VOLUME_ID

  Options:
  -s, --snapshot-schedule [INTERVAL|HOURLY|DAILY|WEEKLY]
                                  Snapshot schedule to use for replication,
                                  (INTERVAL | HOURLY | DAILY | WEEKLY)
                                  [required]
  -l, --location TEXT             Short name of the data center for the
                                  replicant (e.g.: dal09)  [required]
  --tier [0.25|2|4|10]            Endurance Storage Tier (IOPS per GB) of the
                                  primary volume for which a replicant is
                                  ordered [optional]
  -h, --help                      Show this message and exit.
  ```

* 列出檔案磁區的現有抄本磁區。
  ```
  # slcli file replica-partners --help
  Usage: slcli file replica-partners [OPTIONS] VOLUME_ID

  Options:
  --sortby TEXT   Column to sort by
  --columns TEXT  Columns to display. Options: ID, Username, Account ID,
                  Capacity (GB), Hardware ID, Guest ID, Host ID
  -h, --help      Show this message and exit.
  ```

* 將檔案磁區失效接手至特定的抄本磁區。
  ```
  # slcli file replica-failover --help
  Usage: slcli file replica-failover [OPTIONS] VOLUME_ID

  Options:
  --replicant-id TEXT  ID of the replicant volume
  --immediate          Failover to replicant immediately.
  -h, --help      Show this message and exit.
```

* 從特定的抄本磁區失效回復檔案磁區。
  ```
  # slcli file replica-failback --help
  Usage: slcli file replica-failback [OPTIONS] VOLUME_ID

  Options:
  --replicant-id TEXT  ID of the replicant volume
  -h, --help           Show this message and exit.
  ```
