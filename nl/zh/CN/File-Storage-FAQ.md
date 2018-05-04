---

copyright:
  years: 2014, 2018
lastupdated: "2018-04-24"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.filestorage_short}} - 常见问题

## 如何度量 IOPS？

IOPS 根据 16 KB 块的负载概要文件来度量，其中随机 50% 读操作和 50% 写操作。不同于此概要文件的工作负载可能会遇到性能降低问题。

## 如果在度量性能时使用更小的块大小，会发生什么情况？

使用更小的块大小时，仍然可以获得最大 IOPS，但是吞吐量会下降。例如：下面是具有 6000 IOPS 的卷在各种不同块大小时的吞吐量：

- 16 KB * 6000 IOPS == 约 93.75 MB/秒
- 8 KB * 6000 IOPS == 约 46.88 MB/秒
- 4 KB * 6000 IOPS == 约 23.44 MB/秒


## 卷需要预热才能达到所需吞吐量吗？

不需要预热。在供应卷之后，您将立即观察到指定的吞吐量。

## 如何判断哪些 {{site.data.keyword.filestorage_short}} LUN/卷已加密？

在客户门户网站中查看 {{site.data.keyword.filestorage_short}} 的列表时，加密 LUN/卷的名称右侧会显示“锁定”图标。

## 如果数据中心内有在升级前供应的非加密 {{site.data.keyword.filestorage_short}}，那么在数据中心升级进行加密后我能对此 {{site.data.keyword.filestorage_short}} 进行加密吗？

无法对数据中心升级之前供应的 {{site.data.keyword.filestorage_short}} 进行加密。在已升级的数据中心内供应的新 {{site.data.keyword.filestorage_short}} 会自动加密；没有加密设置可供选择，这是自动执行的操作。通过创建新的文件卷，然后使用基于主机的迁移将数据复制到新的加密卷，可以对已升级数据中心内非加密存储器上的数据进行加密。有关如何执行迁移的指示信息，请参阅[此文章](/docs/infrastructure/FileStorage/migrate-file-storage-encrypted-file-storage.html)。

## 怎样知道是在已升级的数据中心内供应 {{site.data.keyword.filestorage_short}}？

供应 {{site.data.keyword.filestorage_short}} 时，在订购表单中会用星号 (`*`) 表示所有已升级的数据中心，并指示将供应使用加密的存储器。供应存储器后，在存储器列表中会看到相应图标，指示该卷已加密。所有加密卷仅在已升级的数据中心内供应。您可以在[此处](/docs//infrastructure/BlockStorage/new-ibm-block-and-file-storage-location-and-features.html)找到已升级的数据中心和可用功能的完整列表。

## 为什么可以在一些数据中心内供应耐久性 10 IOPS 层的 {{site.data.keyword.filestorage_short}}，而在其他数据中心内不行？

{{site.data.keyword.filestorage_short}} 耐久性类型 10 IOPS/GB 层仅在精选数据中心内可用，很快会增加新的数据中心。您可以在[此处](/docs//infrastructure/BlockStorage/new-ibm-block-and-file-storage-location-and-features.html)找到已升级的数据中心和可用功能的完整列表。

## 如何找到 {{site.data.keyword.filestorage_short}} 的正确安装点？

这些数据中心内供应的所有加密 {{site.data.keyword.filestorage_short}} 卷的安装点与非加密卷不同。要确保对加密和非加密 {{site.data.keyword.filestorage_short}} 卷使用正确的安装点，可以在 UI 中的**卷详细信息**页面中查看安装点信息，还可以通过以下 API 调用来访问正确的安装点：`SoftLayer_Network_Storage::getNetworkMountAddress()`。

## 每种文件卷大小允许多少个文件共享？每种卷大小允许的最大文件共享数是多少？
下面是根据卷大小允许的最大索引节点数或文件共享数：

<table>
        <tbody>
          <tr>
            <th>卷大小</th>
            <th>索引节点数/文件数</th>
          </tr>
          <tr>
            <td>20 GB</td>
            <td>622,484</td>
          </tr>
          <tr>
            <td>40 GB</td>
            <td>1,245,084</td>
          </tr>          
          <tr>
            <td>80 GB</td>
            <td>2,490,263</td>
          </tr>          
          <tr>
            <td>100 GB</td>
            <td>3,112,863</td>
          </tr>          
          <tr>
            <td>250 GB</td>
            <td>7,782,300</td>
          </tr>          
          <tr>
            <td>500 GB</td>
            <td>15,564,695</td>
          </tr>
          <tr>
            <td>1 TB+</td>
            <td>31,876,593</td>
          </tr>
        </tbody>
</table>

## 可以供应多少个卷？

缺省情况下，总共可以供应 250 个块存储卷和文件存储卷。要增加卷数，请联系销售代表。

## 一个供应的 {{site.data.keyword.filestorage_short}} 卷可以由多少个实例共享使用？

每个文件卷的缺省授权数限制为 64。要增大此限制，请联系销售代表。

## 供应“性能”或“耐久性”{{site.data.keyword.filestorage_short}} 时，是按实例还是按卷强制执行分配的 IOPS？

IOPS 会在卷级别强制执行。换句话说，连接到一个具有 6000 IOPS 的卷的两个主机会共享 6000 IOPS。

## 使用更快的以太网连接时是否能够实现更高的吞吐量？

吞吐量限制是按卷/LUN 级别设置的，因此使用更快的以太网连接并不会增加该设定限制。但是，使用较慢的以太网连接时，带宽可能是潜在瓶颈。

## 防火墙/安全组会影响性能吗？

建议的最佳做法是在绕过防火墙的 VLAN 上运行存储流量。通过软件防火墙运行存储流量会延长等待时间，并对存储器性能产生负面影响。

## 预计 {{site.data.keyword.filestorage_short}} 中的性能等待时间是多少？   

存储器中的目标等待时间小于 1 毫秒。存储器连接到共享网络上的计算实例，所以确切的性能等待时间将取决于给定时间范围内的网络流量。

## 删除 {{site.data.keyword.filestorage_short}} 卷时，数据会发生什么情况？

删除存储器时，会除去该卷上数据的所有指针，因此数据会变得完全不可访问。如果将物理存储器重新供应给其他帐户，那么会分配一组新指针。新帐户无法访问物理存储器上原先可能存在的任何数据，这组新指针会显示全为 0。将新数据写入卷/LUN 时，会覆盖仍存在的任何不可访问的数据。 

## 使驱动器从云数据中心退役时会发生什么情况？

使驱动器退役后，IBM 会在处置前先销毁驱动器，从而使其无法使用。写入该驱动器的任何数据都将变得无法访问。

