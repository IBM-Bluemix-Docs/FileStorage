---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

keywords: File Storage, adjusting IOPS, increase IOPS, decrease IOPS, modify IOPS

subcollection: FileStorage

---
{:external: target="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 調整 IOPS
{: #adjustingIOPS}

使用這個新增特性，{{site.data.keyword.filestorage_full}} 儲存空間使用者可以立即調整其現有 {{site.data.keyword.filestorage_short}} 的 IOPS。他們不需要建立重複項目，或者手動將資料複製到新的儲存空間。進行調整時，使用者不會遇到任何類型的中斷，也不會無法存取儲存空間。

儲存空間的計費已更新成將新價格的按比例差額新增至現行計費週期。會在下一個計費週期收取新的完整金額。


## 可調式 IOPS 的優點

- 成本管理 - 有些客戶可能只有在用量尖峰期間才需要高 IOPS。例如，大型零售商店在假日期間會有用量尖峰，因此其儲存空間可能在當時比起盛夏而言會需要較高的 IOPS。此特性可讓它們管理其成本，並且只有在需要時才支付較高的 IOPS 費用。

## 限制
{: #limitsofadjustIOPS}

只有[精選資料中心](/docs/infrastructure/FileStorage?topic=FileStorage-news)內才提供此特性。

客戶在調整其 IOPS 時無法切換「耐久性」與「效能」。使用者可以根據下列準則和限制，為其儲存空間指定新的 IOPS 層級或 IOPS 層次。

- 如果原始磁區是「耐久性 0.25」層級，則無法更新 IOPS 層級。
- 如果原始磁區是具有小於或等於 0.30 IOPS/GB 的「效能」磁區，則可用的選項只包含結果會得到小於或等於 0.30 IOPS/GB 的大小及 IOPS 組合。
- 如果原始磁區是具有超過 0.30 IOPS/GB 的「效能」磁區，則可用的選項只包含結果會得到超過 0.30 IOPS/GB 的大小及 IOPS 組合。

## IOPS 調整對於抄寫的效果

如果磁區已有抄寫，則會自動更新抄本，以符合主要磁區的 IOPS 選取項目。

## 調整儲存空間上的 IOPS
{: #adjustingsteps}

1. 移至您的 {{site.data.keyword.filestorage_short}} 清單
    - 從客戶入口網站，按一下**儲存空間** > **{{site.data.keyword.filestorage_short}}**，或者
    - 從 {{site.data.keyword.cloud}} 主控台，按一下**基礎架構** > **儲存空間** > **{{site.data.keyword.filestorage_short}}**。
2. 從清單中選取磁區，然後按一下**動作** > **修改磁區**
3. 在**儲存空間 IOPS 選項**下，進行新的選取：
    - 針對「耐久性」（分層 IOPS），請為您的儲存空間選取大於 0.25 IOPS/GB 的「IOPS 層級」。您隨時可以增加 IOPS 層級。不過，一個月只能減少一次。
    - 針對「效能」（已配置的 IOPS），請為您的儲存空間指定新的 IOPS 選項，輸入範圍在 100 到 48,000 IOPS 的值。（請務必在訂單表格中查看大小所需的任何特定界限）。
4. 檢閱您的選取項目及新的定價。
5. 按一下**我已閱讀主要服務合約...** 勾選框，然後按一下**下訂單**。
6. 在幾分鐘之後，就可以使用您的新儲存空間配置。

或者，您可以透過 SLCLI 更新 IOPS。
```
# slcli file volume-modify --help
Usage: slcli file volume-modify [OPTIONS] VOLUME_ID

Options:
  -c, --new-size INTEGER        New Size of file volume in GB. ***If no size
                                is given, the original size of volume is
                                used.***
                                Potential Sizes: [20, 40, 80, 100,
                                250, 500, 1000, 2000, 4000, 8000, 12000]
                                Minimum: [the original size of the volume]
  -i, --new-iops INTEGER        Performance Storage IOPS, between 100 and 6000
                                in multiples of 100 [only for performance
                                volumes] ***If no IOPS value is specified, the
                                original IOPS value of the volume will be
                                used.***
                                Requirements: [If original IOPS/GB
                                for the volume is less than 0.3, new IOPS/GB
                                must also be less than 0.3. If original
                                IOPS/GB for the volume is greater than or
                                equal to 0.3, new IOPS/GB for the volume must
                                also be greater than or equal to 0.3.]
  -t, --new-tier [0.25|2|4|10]  Endurance Storage Tier (IOPS per GB) [only for
                                endurance volumes] ***If no tier is specified,
                                the original tier of the volume will be
                                used.***
                                Requirements: [If original IOPS/GB
                                for the volume is 0.25, new IOPS/GB for the
                                volume must also be 0.25. If original IOPS/GB
                                for the volume is greater than 0.25, new
                                IOPS/GB for the volume must also be greater
                                than 0.25.]
  -h, --help      Show this message and exit.
```
