---

copyright:
  years: 2014, 2019
lastupdated: "2019-06-10"

keywords: File Storage, file storage, NFS, replication, duplication, synchronous, replica schedule, replica space, disaster recovery

subcollection: FileStorage

---
{:external: target="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}


# 复制数据
{: #replication}

复制使用其中一个快照安排自动将快照复制到远程数据中心内的目标卷。如果发生灾难性事件，或者数据变得损坏，那么可以在远程站点中恢复副本。

复制可以使两个不同位置的数据保持同步。如果要克隆卷并独立于原始卷来使用该卷，请参阅[创建复制文件卷](/docs/infrastructure/FileStorage?topic=FileStorage-duplicatevolume)。
{:tip}

必须创建快照安排后，才能进行复制。
{:important}


## 确定复制的存储卷的远程数据中心

在世界各地的 {{site.data.keyword.cloud}} 数据中心组成了多个主数据中心和远程数据中心组合。请参阅表 1，以获取数据中心可用性和复制目标的完整列表。

|美国 1|美国 2|拉丁美洲|加拿大|欧洲|亚太地区|澳大利亚|
|-----|-----|-----|-----|-----|-----|-----|
|DAL01<br />DAL05<br />DAL06<br />HOU02<br />SJC01<br />WDC01|SJC03<br />SJC04<br />WDC04<br />WDC06<br />WDC07<br />DAL09<br />DAL10<br />DAL12<br />DAL13|MEX01<br />SAO01|TOR01<br />MON01|AMS01<br />AMS03<br />FRA02<br />FRA04<br />FRA05<br />LON02<br />LON04<br />LON05<br />LON06<br />OSL01<br />PAR01<br />MIL01|HKG02<br />TOK02<br />TOK04<br />TOK05<br />SNG01<br />SEO01<br />                                CHE01|SYD01<br />SYD04<br />          SYD05<br />MEL01|
{: caption="表 1 - 下表显示每个区域中具有增强功能的数据中心的完整列表。每个区域单独一列。某些城市（例如，达拉斯、圣何塞、华盛顿特区、阿姆斯特丹、法兰克福、伦敦和悉尼）有多个数据中心。“美国 1”区域中的数据中心没有增强型存储器。具有增强存储功能的数据中心内的主机无法启动与“美国 1”数据中心内副本目标的复制。" caption-side="top"}


## 创建初始副本

复制将根据快照安排来执行。必须先有可用于源卷的快照空间和快照安排，然后才能进行复制。如果尝试设置复制，但未设置源卷的快照空间或快照安排，那么系统将提示您购买更多空间或设置安排。在 [{{site.data.keyword.cloud}} 控制台](https://{DomainName}/classic){: external}中的**存储** > **{{site.data.keyword.filestorage_short}}** 下管理复制。

1. 单击存储卷。
2. 单击**副本**，然后单击**购买复制**。
3. 选择希望复制遵循的现有快照安排。此列表包含所有有效的快照安排。<br />

   只能选择一个安排，即便有每小时、每天和每周的混合安排也是如此。将复制自上一个复制周期以来捕获到的所有快照，而不管这些快照源自哪个安排。<br />如果没有设置快照，那么系统会提示您进行设置，然后才能订购复制。有关更多信息，请参阅[使用快照](/docs/infrastructure/FileStorage?topic=FileStorage-snapshots)。
   {:tip}
3. 单击**位置**，然后选择将作为 DR 站点的数据中心。
4. 单击**继续**。
5. 如果您有促销码，请在**促销码**中进行输入，然后单击**重新计算**。缺省情况下，已填写窗口中的其他字段。

   处理订单时会应用折扣。
   {:note}
6. 单击**我已阅读主服务协议...** 复选框，然后单击**下订单**。


## 编辑现有复制

在 [{{site.data.keyword.cloud}} 控制台](https://{DomainName}/classic){: external}中**存储** > **{{site.data.keyword.filestorage_short}}** 下的**主**或**副本**选项卡中，可以编辑复制安排和更改复制空间。


## 编辑复制安排

复制安排基于现有快照安排。要将复制安排从每小时更改为每天或每周，或者反之，必须取消该副本卷并设置一个新的副本卷。

但是，如果要更改**每天**复制发生的时间，可以对“主”或“副本”选项卡上的现有安排进行调整。

1. 单击**主**或**副本**选项卡上的**操作**。
2. 选择**编辑快照安排**。
3. 查看**安排**下的**快照**框架，以确定要用于复制的安排。更改所需的安排。
4. 单击**保存**。


## 更改复制空间

主快照空间和副本空间必须相同。如果在**主**或**副本**选项卡上更改空间，那么会自动将该空间添加到源和目标数据中心。增大快照空间还会触发立即复制更新。

1. 单击**主**或**副本**选项卡上的**操作**。
2. 选择**添加更多快照空间**。

3. 从列表中选择存储器大小，然后单击**继续**。

4. 如果您有促销码，请在**促销码**中进行输入，然后单击**重新计算**。缺省情况下，已填写对话框中的其他字段。
5. 单击**我已阅读主服务协议...** 复选框，然后单击**下订单**。


## 在主数据中心内增大快照空间时，也增大副本数据中心内的快照空间

主存储卷和副本存储卷的卷大小必须相同。不能其中一个卷大于另一个卷。增大主卷的快照空间时，副本空间也会自动增加。增大快照空间会触发立即复制更新。这两个卷的增大将在发票上显示为行项，并且将根据需要分派。

有关增加快照空间的更多信息，请参阅[快照](/docs/infrastructure/FileStorage?topic=FileStorage-snapshots)。
## 在卷列表中查看副本卷

您可以在**存储** > **{{site.data.keyword.filestorage_short}}** 下的 {{site.data.keyword.filestorage_short}} 页面中查看复制卷。卷名将显示为主卷名称后跟 REP。**类型**为“耐久性 - 副本”或“性能 - 副本”。**目标地址**为“不适用”（因为副本卷未安装在副本数据中心上），**状态**显示为“不活动”。


## 在副本数据中心查看复制卷的详细信息

您可以在**存储** > **{{site.data.keyword.filestorage_short}}** 下的**副本**选项卡中查看副本卷详细信息。另一个选择是在 **{{site.data.keyword.filestorage_short}}** 页面中选择副本卷，然后单击**副本**选项卡。


## 查看复制历史记录

复制历史记录可在**管理**下**帐户**选项卡上的**审计日志**中进行查看。
主卷和副本卷将显示完全相同的复制历史记录，包括：

- 复制的类型（故障转移或故障恢复），
- 启动时间，
- 用于复制的快照，
- 复制的大小，
- 完成时间。


## 创建副本的复制项

您可以创建现有 {{site.data.keyword.cloud}} {{site.data.keyword.filestorage_full}} 的复制项。缺省情况下，复制卷将继承原始存储卷的容量和性能选项，并且会包含截至快照时间点的数据的副本。

复制项可以基于主卷和副本卷创建。新复制项会在原始卷所在的数据中心内创建。如果基于副本卷创建复制项，那么新卷将在副本卷所在的数据中心内创建。

供应存储器后，主机即可以访问复制卷以进行读/写。但是，在完成从原始项到复制项的数据复制之后，才允许使用快照和复制。

有关更多信息，请参阅[创建复制文件卷](/docs/infrastructure/FileStorage?topic=FileStorage-duplicatevolume)。

## 在灾难发生时使用副本进行故障转移

进行故障转移时，将“翻转开关”从主数据中心的存储卷切换到远程数据中心的目标卷。例如，主数据中心是伦敦，辅助数据中心是阿姆斯特丹。如果发生故障事件，将故障转移到阿姆斯特丹 - 从阿姆斯特丹的计算实例连接到现在的主卷。修复伦敦的卷之后，会生成阿姆斯特丹卷的快照，以便故障恢复到伦敦，并从伦敦的计算实例连接到原先的主卷。

* 如果主位置遇到问题，而存储器和主机仍然联机，请参阅[通过可访问的主卷进行故障转移](/docs/infrastructure/FileStorage?topic=FileStorage-dr-accessible)。
* 如果主位置停机，请参阅[通过不可访问的主卷进行故障转移](/docs/infrastructure/FileStorage?topic=FileStorage-dr-inaccessible)。

## 取消现有复制

您可以立即取消复制，也可以在周年日期取消复制；取消复制将导致记帐结束。可以在**主**或**副本**选项卡中取消复制。

1. 在 **{{site.data.keyword.filestorage_short}}** 页面中，单击卷。
2. 单击**主**或**副本**选项卡上的**操作**。
3. 选择**取消复制**。
4. 选择取消时间。选择**立即**或**周年日期**，然后单击**继续**。
5. 单击**我确认取消操作可能会导致数据丢失**，然后单击**取消复制**。


## 取消主卷时取消复制

取消主卷后，将删除副本数据中心内的复制安排和卷。副本将在 **{{site.data.keyword.filestorage_short}}** 页面中取消。

 1. 在 **{{site.data.keyword.filestorage_short}}** 页面上，突出显示卷。
 2. 单击**操作**，然后选择**取消 {{site.data.keyword.filestorage_short}}**。
 3. 选择取消卷的时间。选择**立即**或**周年日期**，然后单击**继续**。
 4. 单击**我确认取消操作可能会导致数据丢失**，然后单击**取消**。

## SLCLI 中与复制相关的命令
{: #clicommands}

* 列出特定卷的适用复制数据中心。
  ```
  # slcli file replica-locations --help
  用法：slcli file replica-locations [OPTIONS] VOLUME_ID

  选项：
  --sortby TEXT   要作为排序依据的列
  --columns TEXT  要显示的列。选项：标识、长名称、短名称
  -h, --help      显示此消息并退出。
  ```

* 订购文件存储器副本卷。
  ```
  # slcli file replica-order --help
  用法：slcli file replica-order [OPTIONS] VOLUME_ID

  选项：
  -s, --snapshot-schedule [INTERVAL|HOURLY|DAILY|WEEKLY]
                                  用于复制的快照安排，
                                  (INTERVAL | HOURLY | DAILY | WEEKLY)
                                  [必需]
  -l, --location TEXT             用于副本卷的数据中心的短名称
                                  （例如：dal09）[必需]
  --tier [0.25|2|4|10]             为其订购了副本卷的主卷的耐久性存储器层 (IOPS/GB) [可选]
  -h, --help                       显示此消息并退出。
  ```

* 列出文件卷的现有副本卷。
  ```
  # slcli file replica-partners --help
  用法：slcli file replica-partners [OPTIONS] VOLUME_ID

  选项：
  --sortby TEXT   要作为排序依据的列
  --columns TEXT  要显示的列。选项：标识、用户名、帐户标识、
                  容量 (GB)、硬件标识、访客标识、主机标识
  -h, --help      显示此消息并退出。
```

* 将文件卷故障转移到特定副本卷。
  ```
  # slcli file replica-failover --help
  用法：slcli file replica-failover [OPTIONS] VOLUME_ID

  选项：
  --replicant-id TEXT 副本卷的标识
  --immediate         立即故障转移到副本卷。
  -h, --help      显示此消息并退出。
```

* 从特定副本卷故障恢复文件卷。
  ```
  # slcli file replica-failback --help
  用法：slcli file replica-failback [OPTIONS] VOLUME_ID

  选项：
  --replicant-id TEXT  副本卷的标识
  -h, --help           显示此消息并退出。
  ```
