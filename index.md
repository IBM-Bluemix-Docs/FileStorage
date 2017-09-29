---

copyright:
  years: 2014, 2017
lastupdated: "2017-09-29"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Getting Started with File Storage

File Storage is persistent, fast, and flexible Network Attached, NFS-based file storage. In this Network Attached Storage (NAS) environment, you have total control over your file shares function and performance. File storage shares can be connected to up to 64 authorized devices over routed TCP/IP connections for resiliency.

File Storage brings best-in-class levels of durability and availability with an unmatched feature set and is built using industry standards and best practices, and designed to protect the integrity of the data and maintain availability through maintenance events and unplanned failures while providing a consistent performance baseline.

Take advantage of the following core features of File Storage:

- **Consistent performance baseline**
   - Provided through the allocation of protocol-level input/output operations per second (IOPS) to individual volumes
- **File storage**
   - Available for file-based NFS shares
- **Highly durable and resilient**
   - Protects the integrity of the data and maintains availability through maintenance events and unplanned failures without the need to create and manage operating system-level redundant array of independent disk (RAID) arrays
- **Data-At-Rest Encryption** [(Available in select data centers.)](new-ibm-block-and-file-storage-location-and-features.html)
   - Provider managed encryption for data-at-rest at no additional cost
- **All Flash Backed Storage** [(Available in select data centers.)](new-ibm-block-and-file-storage-location-and-features.html)
   - All flash storage for volumes provisioned with Endurance or Performance at 2IOPS/GB or higher
- **Snapshots (When provisioned with Endurance or Performance in [select data centers]**(new-ibm-block-and-file-storage-location-and-features.html)).
   - Captures point-in-time data snapshots non-disruptively
- **Replication** (When provisioned with Endurance or Performance in [select data centers](new-ibm-block-and-file-storage-location-and-features.html).
   - Automatically copies snapshots to a partner {{site.data.keyword.BluSoftlayer_full)} data center
- **Highly available connectivity**
   - Uses redundant networking connections to maximize availability - NFS-based File Storage routed TCP/IP connections
- **Concurrent access**
   - Allows multiple hosts (up to 64) to simultaneously access file volumes
- **Clustered databases**
   - Supports advanced use cases, such as clustered databases

## Hourly / Monthly Billing

You can select hourly or monthly billing for a File Volume. The type of billing selected for a LUN will apply to its snapshot space and replicas. For example, if you provision a LUN with hourly billing, any snapshots or replica fees will be billed hourly. If you provision a LUN with monthly billing, any snapshots or replica fees will be billed monthly. 

With **hourly billing**, the calculation of the number of hours the file volume existed on the account is performed at the time the volume is deleted or at the end of the billing cycle, which ever comes first.  Hourly billing is a good choice for storage that is used for a few days or less than a full month. Hourly billing is only available for storage provisioned in [select data centers](new-ibm-block-and-file-storage-location-and-features.html). 

With **monthly billing**, the calculation for the price is pro-rated from the date of creation to the end of the billing cycle and billed immediately. There is no refund If a file volume is deleted before the end of the billing cycle.  Monthly billing is a good choice for storage used in production workloads that use data that needs to be stored and accessed for long periods of time (one month or longer).  

## Provisioning

File Storage volumes can be provisioned from 20GB to 12TB with two options for provisioning:

Provision with Endurance tiers – featuring pre-defined performance levels and features like snapshots and replication or build a high-powered Performance environment with allocated input/output operations per second (IOPS).

 
### Endurance Tiers

When ordering with Endurance choose from multiple performance tiers to support varied application needs.

Endurance is available in three IOPS performance tiers to support varying application needs.

**Note:** Once provisioned, you cannot migrate between tiers.

- **0.25 IOPS per GB** is designed for workloads with low I/O intensity. These workloads are typically characterized by having a large percentage of data inactive at a given time. Example applications include storing mailboxes or departmental level file shares.
- **2 IOPS per GB** is designed for most general purpose usage. Example applications include hosting small databases backing web applications or virtual machine disk images for a hypervisor.
- **4 IOPS per GB** is designed for higher-intensity workloads. These workloads are typically characterized by having a high percentage of data active at a given time. Example applications include transactional and other performance-sensitive databases.
- **10 IOPS per GB** is designed for the most demanding workloads such as those created by NoSQL Databases, and data processing for Analytics.  This tier is available for storage provisioned up to 4TB in size in [select data centers](new-ibm-block-and-file-storage-location-and-features.html).

Up to 48,000 IOPS are available with a 12TB Endurance volume.


While choosing the right tier of Endurance file storage for your workload it is key, it is equally important to use the block size, Ethernet connection speed, and number of hosts necessary to achieve maximum performance. If any of these parts do not align with the other, it can have a significant impact on the resulting throughput
 
### Performance

Performance is a class of {{site.data.keyword.BluSoftlayer_full)} file storage that is designed to support high I/O applications with well understood performance requirements that don’t fit well within an Endurance tier. Predictable performance is achieved through the allocation of protocol-level IOPS to individual volumes. IOPS ranging from 100 through 6,000 can be provisioned with storage sizes that range from 20 GB to 12 TB. 

Performance for file storage is accessed and mounted through a Network File System (NFS) connection. File Storage is typically used when the volume will be accessed by multiple machines simultaneously. Consistent Performance volumes can be ordered according to the Sizes and IOPS in Table 1 and can be used with Linux operating systems.

<table cellpadding="1" cellspacing="1" style="width: 99%;">
        <colgroup>
          <col/>
          <col/>
          <col/>
        </colgroup>
        <tbody>
          <tr>
            <th>Size (GB)</th>
            <th>Min IOPS</th>
            <th>Max IOPS</th>
          </tr>
          <tr>
            <td>20</td>
            <td>100</td>
            <td>1,000</td>
          </tr>
          <tr>
            <td>40</td>
            <td>100</td>
            <td>2,000</td>
          </tr>
          <tr>
            <td>80</td>
            <td>100</td>
            <td>4,000</td>
          </tr>
          <tr>
            <td>100</td>
            <td>100</td>
            <td>6,000</td>
          </tr>
          <tr>
            <td>250</td>
            <td>100</td>
            <td>6,000</td>
          </tr>
          <tr>
            <td>500</td>
            <td>100</td>
            <td>6,000 or 10,000<sup><img src="/images/numberone.png" alt="footnote" /></sup></td>
          </tr>
          <tr>
            <td>1,000</td>
            <td>100</td>
            <td>6,000 or 20,000<sup><img src="/images/numberone.png" alt="footnote" /></sup></td>
          </tr>
          <tr>
            <td>2,000-3,000</td>
            <td>200</td>
            <td>6,000 or 40,000<sup><img src="/images/numberone.png" alt="footnote" /></sup></td>
          </tr>
          <tr>
            <td>4,000-7,000</td>
            <td>300</td>
            <td>6,000 or 48,000<sup><img src="/images/numberone.png" alt="footnote" /></sup></td>
          </tr>
          <tr>
            <td>8,000-9,000</td>
            <td>500</td>
            <td>6,000 or 48,000<sup><img src="/images/numberone.png" alt="footnote" /></sup></td>
          </tr>
          <tr>
            <td>10,000-12,000</td>
            <td>1,000</td>
            <td>6,000 or 48,000<sup><img src="/images/numberone.png" alt="footnote" /></sup></td>
          </tr>
        </tbody>
</table>

<sup>![footnote](/images/numberone.png)</sup>  IOPs limit above 6,000 is available in select data centers.


Performance volumes are designed to perform consistently close to the provisioned IOPS level. Consistency makes it easier to size and scale application environments with a given level of performance. Additionally, given the range of volume sizes and IOPS counts, it becomes possible to optimize an environment by building a volume with the ideal price-to-performance ratio.

IOPS, for both Endurance and Performance, are measured based on a 16KB block size with a 50/50 read/write mix. To achieve maximum IOPS on a volume, adequate network resources need to be in place. Other considerations include private network usage outside of storage and host side and application specific tunings (IP stack, queue depths, and so on). 

### Tips for provisioning IOPS for file storage

Choosing the storage solution that is right for your workload is important, and equally important is how to avoid bottlenecks.  IOPS for both Endurance and Performance is measured based on a 16KB block size with a 50/50 read/write mix. This is important because if you choose a size larger than 16KB, the throughput is affected. The reason is that a 16KB block is the equivalent of one write to the volume. Each multiple adds more writes decreasing the response time to the server. For example, a 64KB block size is the equivalent to four writes to the volume. Or, four IOPS per GB at 16KB block size is equivalent to one IOPS per GB at 64KB block size.

Knowing how many IOPS you are getting from your volume can help you determine what your throughput will be. A way to calculate expected throughput is to multiply block size by IOPS (block size * IOPS = throughput). However, throughput can also be constrained by other factors. The speed of your Ethernet connection must be faster than the expected maximum throughput from your volume. For example, if you have 6,000 IOPS and are using a 16KB block size, the volume is capable of approximately 94MB per second. If you have a 1Gbps Ethernet connection to your LUN, it will become a bottleneck when your servers attempt to utilize the maximum available throughput.

As a general rule you should not expect to saturate your Ethernet connection beyond 70% of the available bandwidth. If expected workload will require the maximum throughput of your volume, it is recommended to assure that your Ethernet connection speed can accommodate the necessary throughput. In the example above, 70% of the theoretical limit of a 1Gbps Ethernet connection (125MB per second) would allow for 88MB per second. You would encounter a bottleneck if you were attempting to utilize the maximum throughput of 94MB per second of your volume.

Another factor to consider is the number of hosts that are utilizing your volume. If there is a single host that is accessing the volume it may be difficult to realize the maximum IOPS available, especially at extreme IOPS counts (10,000s). If your workload requires high throughput it would best to configure at least two or three servers to access your volume to avoid a single server bottleneck.

To achieve maximum IOPS, adequate network resources need to be in place. Other considerations include private network usage outside of storage and host side and application specific tunings (IP stack, queue depths, and so on).

Both NFS v3 and NFS v4.1 are supported in the {{site.data.keyword.BluSoftlayer_full)} environment. However, it is our recommendation that NFS v3 be used. NFS v4.1 is a stateful protocol (not stateless like NFSv3) and thus protocol issues can occur during network events. NFS v4.1 must quiesce operations and then perform lock reclamation. On a relatively busy NFS file server, the increased latency can cause disruptions. The lack of NFS v4.1 multipath/trunking can also extend NFS operations recovery.
