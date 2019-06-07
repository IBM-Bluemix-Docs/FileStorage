---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

keywords: File Storage, file storage, NFS, host queue depth, performance tuning

subcollection: FileStorage

---
{:external: target="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 调整主机队列深度设置
{: #hostqueuesettings}

{{site.data.keyword.cloud}} 建议为每个性能层设置最大主机和应用程序输入/输出 (I/O) 队列深度。

|性能层|最大主机队列深度|
|:------:|:------:|
|0.25 IOPS/GB|8|
|2 IOPS/GB|24|
|4 IOPS/GB|56|
{: caption="每个 IOPS 层的建议队列深度" caption-side="top"}


主机设置不会影响磁盘和控制器等待时间。它仅影响主机和应用程序遵循的等待时间。

超过所列数字的队列深度可能会增加主机 I/O 等待时间。低于所列数字的队列深度可能会降低主机 I/O 性能。由于每个应用程序各不相同，因此需要调整和观察以实现最高存储性能。

主机队列深度通常在主机总线适配器驱动程序或系统管理程序中进行调整，有时也在应用程序中进行调整。标准缺省值（如 32 或 64）可能会导致主机或应用程序等待时间太长。

如果一个主机或系统管理程序在使用多个性能层，请对速度最快的层使用队列深度，并观察速度最慢的性能层上的等待时间。

如果无法接受速度最慢的层上的等待时间，请调整队列深度，直至所有层的等待时间和性能达到平衡为止。
