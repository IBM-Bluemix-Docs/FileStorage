---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-01"

---

{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}


# 複製抄本磁區供災難回復使用

萬一發生導致主要站台停電的災難性失效或災難，客戶可以執行下列動作，以便在次要站台快速存取其資料。 

## 在次要站台上利用抄本磁區的副本進行失效接手

1. 登入 [IBM Cloud 主控台](https://console.bluemix.net/catalog/){:new_window}，然後按一下左上方的**功能表**圖示。選取**典型基礎架構**。 

   或者，您可以登入 [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}。
2. 按一下**儲存空間** > **{{site.data.keyword.filestorage_short}}**。
3. 按一下清單中的檔案共用抄本，以檢視其**詳細資料**頁面。
4. 在**詳細資料**頁面上，向下捲動並選取現有的 Snapshot，然後按一下**動作** > **複製**。
5. 針對新磁區的容量（為了增加大小）或 IOP 進行任何必要的更新。
6. 必要的話，您可以更新新磁區的 Snapshot 空間。
7. 按一下**繼續**，以訂購重複項目。

建立磁區之後，您可以將它連接到主機，並在該磁區上執行讀寫作業。當資料從原始磁區複製到重複磁區時，您會在詳細資料頁面上看到一個顯示正在進行複製的狀態。複製處理程序完成之後，新的磁區即與原始磁區完全無關，您可以像平常一樣使用 Snapshot 及抄寫進行管理。

## 失效回復至原始主要站台

如果您想要使正式作業回到原始主要站台，您必須執行下列步驟。

1. 登入 [IBM Cloud 主控台](https://console.bluemix.net/catalog/){:new_window}，然後按一下左上方的**功能表**圖示。選取**典型基礎架構**。 

   或者，您可以登入 [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}。
2. 按一下**儲存空間** > **{{site.data.keyword.filestorage_short}}**。
3. 按一下 LUN 名稱，並建立 Snapshot 排程（如果尚無排程）。 

   如需 Snapshot 排程的相關資訊，請參閱[管理 Snapshot](working-with-snapshots.html#adding-a-snapshot-schedule)。
   {:tip}
4. 按一下**抄本**，然後按一下**購買抄寫**。
5. 選取您要抄寫遵循的現有 Snapshot 排程。此清單包含所有作用中 Snapshot 排程。 
6. 按一下**位置**，然後選取作為原始正式作業網站的資料中心。
7. 按一下**繼續**。
8. 按一下**我已閱讀主要服務合約...** 勾選框，然後按一下**下訂單**。

抄寫完成之後，您需要建立新抄本的複製磁區。
{:important}

1. 回到**儲存空間** > **{{site.data.keyword.filestorage_short}}**。
2. 按一下清單中的 LUN 抄本，以檢視其**詳細資料**頁面。
3. 在**詳細資料**頁面上，向下捲動並選取現有的 Snapshot，然後按一下**動作** > **複製**。
4. 針對新磁區的容量（為了增加大小）或 IOP 進行任何必要的更新。
5. 必要的話，請更新新磁區的 Snapshot 空間。
6. 按一下**繼續**，以訂購重複項目。

當複製處理程序完成時，您可以取消抄寫及所使用的磁區，使資料回到原始主要站台。此複製項目會變成主要儲存空間，而原始次要站台的抄寫可以重新建立。
