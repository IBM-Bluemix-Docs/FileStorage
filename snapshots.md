---

copyright:
  years: 2014, 2018
lastupdated: "2018-11-13"

---
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Snapshots

Snapshots are a feature of {{site.data.keyword.filestorage_full}}. A snapshot represents a volume's contents at a particular point in time. With snapshots, you can protect your data with no performance impact and minimal consumption of space. Snapshots are considered your first line of defense for data protection. If a user accidentally modifies or deletes crucial data from a volume, the data can be easily and quickly restored from a snapshot copy.

{{site.data.keyword.filestorage_short}} provides you with two ways to take your snapshots.

* First, through a configurable snapshot schedule that creates and deletes snapshot copies automatically for each storage volume. You can also create extra snapshot schedules, manually delete copies, and manage schedules based on your requirements.
* The second way is to take a manual snapshot.

A snapshot copy is a read-only image of a {{site.data.keyword.filestorage_short}} volume that captures the state of the volume at a point in time. Snapshot copies are efficient both in the time that is needed to create them and in storage space. A {{site.data.keyword.filestorage_short}} snapshot copy takes only a few seconds to create. It's typically less than 1 second, regardless of the size of the volume or the level of activity on the storage. After a snapshot copy is created, changes to data objects are reflected in updates to the current version of the objects, as if Snapshot copies didn't exist. Meanwhile, the copy of the data remains stable.

A Snapshot copy incurs no performance decrease. Users can easily store up to 50 scheduled snapshots and 50 manual snapshots per {{site.data.keyword.filestorage_short}} volume, all of which are accessible as read-only and online versions of the data.

With snapshots, you can:

- Non-disruptively create point-in-time recovery points,
- Revert volumes to previous points-in-time.

You must purchase some amount of snapshot space for your volume first so you can take snapshots of it. The snapshot space can be added during the initial order or afterward through the **Volume Details** page. Scheduled and manual snapshots share the snapshot space, so make sure you order enough Snapshot space.  For more information, see [Ordering Snapshots](ordering-snapshots.html).

## Snapshot best practices

Snapshot design depends on the customer’s environment. The following design considerations can help you to plan and implement Snapshot copies:
- Up to 50 snapshots can be created through a schedule and up to 50 manually on each volume or LUN.
- Don't over snap. Make sure that your scheduled snapshot frequency meets your RTO and RPO needs and your application business requirements by scheduling hourly, daily, or weekly snapshots.
- Snapshot AutoDelete can be used to control the growth of storage consumption.

  The AutoDelete threshold is fixed at 95 percent.
  {:note}

Snapshots are not replacements for actual off-site Disaster Recovery replication or long-retention backup.
{:important}

## Security

All snapshots and replicas of encrypted {{site.data.keyword.filestorage_short}} are also encrypted by default. This feature can't be turned off on a volume basis. For more information about provider-managed encryption-at-rest, see [Securing your data](block-file-storage-encryption-rest.html).

## How Snapshots affect the disk space

Snapshot copies minimize disk consumption by preserving individual blocks rather than whole files. Snapshot copies use extra space only when files in the active file system are changed or deleted.

In the active file system, the changed blocks are rewritten to different locations on the disk or removed as active file blocks entirely. When files are changed or deleted, the original file blocks are preserved as part of one or more Snapshot copies. As a result, disk space that is used by the original blocks is still reserved to reflect the status of the active file system before the change. This space is reserved in addition to the disk space that is used by blocks in the modified active file system.

<table>
    <colgroup>
      <col style="width: 33.3%;"/>
      <col style="width: 33.3%;"/>
      <col style="width: 33.3%;"/>
    </colgroup>
      <tr>
        <th colspan="3" style="border: 0.0px;text-align: center;">Disk Space Usage Before and After Snapshot Copy</th>
     </tr>
     <tr>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle1.png" alt="Before Snapshot Copy"></td>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle3.png" alt="After Snapshot Copy"></td>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle2.png" alt="Changes after Snapshot Copy"></td>
     </tr>
     <tr>
        <td style="border: 0.0px;">Before any Snapshot copy is created, disk space is used by the active file system only.</td>
        <td style="border: 0.0px;">After a Snapshot copy is created, the active file system and Snapshot copy point to the same disk blocks. The Snapshot copy doesn't use extra disk space.</td>
        <td style="border: 0.0px;">After <i>myfile.txt</i> is deleted from the active file system, the Snapshot copy still includes the file, and references its disk blocks. That's why deleting active file system data doesn't always free up disk space.</td>
      </tr>
</table>

For more information about snapshot space usage, see [Managing Snapshots](working-with-snapshots.html).
