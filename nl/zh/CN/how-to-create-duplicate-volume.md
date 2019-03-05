---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 创建复制 {{site.data.keyword.filestorage_short}}
{: #duplicatevolume}

您可以创建现有 {{site.data.keyword.BluSoftlayer_full}} {{site.data.keyword.filestorage_full}} 的副本。缺省情况下，复制卷将继承原始卷的容量和性能选项，并且会包含截至快照时间点的数据的副本。   

因为复制项基于时间点快照中的数据，所以原始卷上需要有快照空间，然后您才能创建复制项。要了解有关快照以及如何订购快照空间的更多信息，请参阅[快照文档](/docs/infrastructure/FileStorage?topic=FileStorage-snapshots)。  

复制项可以基于**主卷**和**副本卷**创建。新复制项会在原始卷所在的数据中心内创建。如果基于副本卷创建复制项，那么新卷将在副本卷所在的数据中心内创建。

如果您是 {{site.data.keyword.containerlong}} 的 Dedicated 帐户用户，请参阅 [{{site.data.keyword.containerlong_notm}} 文档](/docs/containers?topic=containers-backup_restore#backup_restore)中有关复制卷的选项。
{:tip}

供应存储器后，主机即可以访问复制卷以进行读/写。但是，在完成从原始项到复制项的数据复制之后，才允许使用快照和复制。数据复制完成后，就可以将复制项作为独立卷进行管理和使用。

此功能在大多数位置中提供。单击[此处](/docs/infrastructure/FileStorage?topic=FileStorage-news)以获取可用数据中心的列表。

复制卷的一些常见用途包括以下示例。
- **灾难恢复测试**。创建副本卷的复制项，以验证数据是否完整并可以在发生灾难时使用，而不中断复制。
- **黄金副本**。使用存储卷作为黄金副本，基于此卷可以创建多个实例以用于各种用途。
- **数据刷新**。创建生产数据的副本，以安装到非生产环境进行测试。
- **从快照复原**。从快照复原原始卷上特定文件和日期的数据，而不使用快照复原功能来覆盖整个原始卷。
- **开发和测试（开发/测试）**。一次最多可同时创建卷的 4 个复制项，以创建复制数据用于开发和测试。
- **存储器大小调整**。创建具有新大小和/或 IOPS 速率的卷，而无需移动数据。  

您可以采用多种方式通过 [{{site.data.keyword.slportal}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){:new_window} 来创建复制卷。


## 基于存储器列表中的特定卷创建复制项

1. 转至 {{site.data.keyword.filestorage_short}} 的列表。
    - 在客户门户网站中，单击**存储** > **{{site.data.keyword.filestorage_short}}** 或
    - 在 {{site.data.keyword.BluSoftlayer_full}}“目录”中，单击**基础架构** > **存储** > **{{site.data.keyword.filestorage_short}}**。
2. 从列表中选择 LUN，然后单击**操作** > **复制 LUN（卷）**。
3. 选择快照选项。
    - 如果是从非副本卷订购，那么
      - 选择**基于新快照创建** - 此操作将创建要用于复制项的快照。如果卷当前没有快照，或者如果要创建该时间点的复制项，请使用此选项。</br>
      - 选择**基于最新快照创建** - 此操作将基于此卷存在的最近快照创建复制项。
    - 如果从副本卷订购，那么唯一的快照选项是使用最近的可用快照。
4. “存储类型”和“位置”会保持与原始卷相同。
5. 按小时或按月计费 - 您可以选择按小时或按月计费来供应复制 LUN。系统会自动选择原始卷的记帐类型。如果您希望为复制存储器选择其他计费类型，那么可以在此进行选择。
5. 如果需要，可以为新卷指定 IOPS 或 IOPS 层。缺省情况下设置了原始卷的 IOPS 指定值。这将显示可用性能和大小组合。
    - 如果原始卷为 0.25 IOPS 耐久性层，那么将无法进行新的选择。
    - 如果原始卷为 2、4 或 10 IOPS 耐久性层，那么可以使新卷移至这些层之间的任意位置。
6. 可以将新卷的大小更新为大于原始卷。缺省情况下设置了原始卷的大小。

   {{site.data.keyword.filestorage_short}} 的大小可以调整为卷原始大小的 10 倍。
   {:tip}
7. 可以更新新卷的快照空间，以添加更多或更少的快照空间，或者不添加快照空间。缺省情况下设置了原始卷的快照空间。
8. 单击**继续**以下订单。


## 基于特定快照创建复制项

1. 转至 {{site.data.keyword.filestorage_short}} 的列表。
2. 单击列表中的卷以查看详细信息页面。这可以是副本卷或非副本卷。
3. 在详细信息页面上向下滚动并从列表中选择现有快照，然后单击**操作** > **复制**。   
4. “存储类型”（耐久性或性能）和“位置”会保持与原始卷相同。
5. 这将显示可用性能和大小组合。缺省情况下设置了原始卷的 IOPS 指定值。可以为新卷指定 IOPS 或 IOPS 层。
    - 如果原始卷为 0.25 IOPS 耐久性层，那么将无法进行新的选择。
    - 如果原始卷为 2、4 或 10 IOPS 耐久性层，那么可以使新卷移至这些层之间的任意位置。
6. 可以将新卷的大小更新为大于原始卷。缺省情况下设置了原始卷的大小。

   {{site.data.keyword.filestorage_short}} 的大小可以调整为卷原始大小的 10 倍。
   {:tip}
7. 可以更新新卷的快照空间，以添加更多或更少的快照空间，或者不添加快照空间。缺省情况下设置了原始卷的快照空间。
8. 单击**继续**，以下订单购买复制卷。

## 通过 SLCLI 创建副本
```
# slcli file volume-duplicate --help
用法：slcli file volume-duplicate [OPTIONS] ORIGIN_VOLUME_ID

选项：
  -o, --origin-snapshot-id INTEGER
                                  用于复制的原始卷快照的标识。
-c, --duplicate-size INTEGER     复制文件卷的大小（以 GB 为单位）。***如果未指定大小，那么将使用原始卷的大小。***
                                  最小值为：[原始卷的大小]
  -i, --duplicate-iops INTEGER    性能存储器 IOPS，介于 100 到 6000 之间，且为 100 的倍数 [仅用于性能卷]
                                  ***如果未指定 IOPS 值，
                                  那么将使用原始卷的 IOPS 值。***
                                  要求：[如果原始卷的 IOPS/GB 小于
                                  0.3，那么复制卷的 IOPS/GB 也必须小于 0.3。
                                  如果原始卷的 IOPS/GB 大于或者等于 0.3，
                                  那么复制卷的 IOPS/GB 也必须大于或者等于 0.3。]
  -t, --duplicate-tier [0.25|2|4|10]
                                  耐久性存储器层 (IOPS/GB) [仅用于耐久性卷]
                                  ***如果未指定层，那么将使用原始卷的层。***
                                  要求：[如果原始卷的 IOPS/GB 为 0.25，那么复制卷的
                                  IOPS/GB 也必须为 0.25。如果原始卷的 IOPS/GB
                                  大于 0.25，那么复制卷的 IOPS/GB 也必须大于 0.25。]
  -s, --duplicate-snapshot-size INTEGER
                                  要为复制卷订购的快照空间的大小。
                                  ***如果未指定快照空间大小，那么将使用原始文件卷的
                                  快照空间大小。*** 为此参数输入“0”表示将订购没有快照空间的复制卷。
  --billing [hourly|monthly]      计费费率的可选参数（缺省为 monthly）
  -h, --help                      显示此消息并退出。
```

## 管理复制卷

将数据从原始卷复制到复制项时，在详细信息页面中会看到复制的状态为“进行中”。在此期间，您可以连接到主机，并对卷进行读/写，但无法创建快照安排。复制过程完成后，新卷将独立于原始项，并且可以如常通过快照和复制进行管理。
