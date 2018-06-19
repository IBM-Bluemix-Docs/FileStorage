---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-14"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Snapshot

Snapshot 是一種 {{site.data.keyword.filestorage_full}} 特性。Snapshot 代表磁區在特定時間點的內容。Snapshot 可讓您保護資料而不影響效能、耗用最小空間，而且視為資料保護的第一線防禦。如果使用者意外修改或刪除具有 Snapshot 特性之磁區中的重要資料，則可以輕鬆且快速地從 Snapshot 副本中還原資料。

{{site.data.keyword.filestorage_short}} 提供兩種方式來擷取 Snapshot - 透過自動建立及刪除每一個儲存空間磁區之 Snapshot 副本的可配置 Snapshot 排程。您也可以根據需求，建立額外 Snapshot 排程、手動刪除副本，以及管理排程。第二種方法是擷取手動 Snapshot。

Snapshot 副本是 {{site.data.keyword.filestorage_short}} 磁區的唯讀映像檔，可擷取磁區某個時間點的狀態。在建立 Snapshot 副本所需的時間以及儲存空間這兩方面，Snapshot 副本都極具效率。不論儲存空間上的磁區大小或活動層次為何，只需要幾秒鐘就可以建立 {{site.data.keyword.filestorage_short}} Snapshot 副本（通常不到 1 秒）。建立 Snapshot 副本之後，對資料物件的變更即會反映在物件現行版本的更新中，就像 Snapshot 副本不存在一樣。同時，資料的副本仍會完全穩定。 

Snapshot 副本不會造成任何效能額外負擔；使用者可以輕鬆地針對每個 {{site.data.keyword.blockstorageshort}} 磁區儲存最多 50 個已排定的 Snapshot 及 50 個手動 Snapshot，這全部都可以作為資料的唯讀及線上版本進行存取

您可以使用 Snapshot 來執行下列動作：

- 不中斷地建立時間點回復點
- 將磁區回復到前一個時間點
- 您必須購買磁區所需的部分 Snapshot 空間量，才能擷取其 Snapshot。在起始磁區訂購期間或起始佈建之後可以新增 Snapshot 空間，方法是透過**磁區詳細資料**頁面。請注意，已排定及手動 Snapshot 會共用 Snapshot 空間，因此請相應地訂購您的空間。如需詳細資料及指引，請參閱[訂購 Snapshot](ordering-snapshots.html) 一文。

## Snapshot 最佳作法
Snapshot 設計取決於客戶環境。下列設計考量可協助您計劃及實作 Snapshot 副本： 
- 在每個磁區或 LUN 上透過排程最多可以建立 50 個 Snapshot，透過手動方式最多可建立 50 個 Snapshot。 
- 不要過度擷取快照。請確定已排定的 Snapshot 頻率符合 RTO 及 RPO 需求，以及應用程式商業需求，方法是排定每小時、每日或每週 Snapshot。 
- Snapshot AutoDelete 應該用來控制儲存空間耗用的成長。<br/>
    **附註**：AutoDelete 臨界值固定為百分之 95。
    
## Snapshot 副本如何使用磁碟空間？

Snapshot 副本可使磁碟耗用量降到最低，方法是保留個別區塊，而非整個檔案。只有在變更或刪除作用中檔案系統中的檔案時，Snapshot 副本才會開始使用額外空間。發生此情況時，仍會保留原始檔案區塊作為一個以上 Snapshot 副本的一部分。

在作用中檔案系統中，會將已變更的區塊重新寫入至磁碟上的不同位置，或當成作用中檔案區塊完全移除。因此，除了已修改的作用中檔案系統中的區塊所使用的磁碟空間之外，仍會保留原始區塊所使用的磁碟空間，以反映作用中檔案系統在變更之前的狀態。

<table>
    <colgroup>
      <col style="width: 33.3%;"/>
      <col style="width: 33.3%;"/>
      <col style="width: 33.3%;"/>
    </colgroup>
    <tbody>
      <tr>
        <th colspan="3" style="border: 0.0px;text-align: center;">Snapshot 副本前後的磁碟空間使用情形</th>
     </tr><tr>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle1.png" alt="Snapshot 副本之前"></td>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle3.png" alt="Snapshot 副本之後"></td>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle2.png" alt="Snapshot 副本之後的變更"></td>
     </tr><tr>
        <td style="border: 0.0px;">建立任何 Snapshot 副本之前，只有作用中檔案系統才會使用磁碟空間。</td>
        <td style="border: 0.0px;">建立 Snapshot 副本之後，作用中檔案系統及 Snapshot 副本會指向相同的磁碟區塊。Snapshot 副本不會使用額外的磁碟空間。</td>
        <td style="border: 0.0px;">即使是從作用中檔案系統刪除 <i>myfile.txt</i> 之後，Snapshot 副本仍然會包括該檔案，並參照其磁碟區塊。因此，刪除作用中檔案系統資料不一定會釋放磁碟空間。</td>
      </tr>
    </tbody>
</table>

若要檢視使用的 Snapshot 空間量，請遵循[管理 Snapshot](working-with-snapshots.html) 文件中的指示。
