---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-30"

---
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}


# Duplicating Replica Volumes for Disaster Recovery

In the event of a catastrophic failure or disaster that causes an outage on the primary site, customers can perform the following actions to quickly access their data on the secondary site.

## Failover with a duplicate of a replica volume on the secondary site

1. Log in to [The IBM Cloud console](https://console.bluemix.net/catalog/){:new_window} and click the **menu** icon on the upper left. Select **Classic Infrastructure**.

   Alternatively, you can log in to the [{{site.data.keyword.slportal}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){:new_window}.
2. Click **Storage** > **{{site.data.keyword.filestorage_short}}**.
3. Click the replica of the file share in the list to view its **Details** page.
4. On the **Details** page, scroll down and select an existing snapshot, then click **Actions** > **Duplicate**.
5. Make any necessary updates to the capacity (to increase size) or IOPs for the new volume.
6. You can update the snapshot space for the new new volume if needed.
7. Click **Continue** to place your order for the duplicate.

As soon as the volume is created, you can attach it to a host and perform read/write operations on that volume. While data is being copied from the original volume to the duplicate, you can see a status on the details page that shows the duplication is in progress. When the duplication process is complete, the new volume becomes completely independent from the original and can be managed with snapshots and replication as normal.

## Failback to the original primary site

If you want to return production to the original primary site, you must perform the following steps.

1. Log in to [The IBM Cloud console](https://{DomainName}/catalog/){:new_window} and click the **menu** icon on the top left. Select **Classic Infrastructure**.

   Alternatively, you can log in to the [{{site.data.keyword.slportal}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){:new_window}.
2. Click **Storage** > **{{site.data.keyword.filestorage_short}}**.
3. Click the LUN name and create a snapshot schedule (if one does not exist already).

   For more information about snapshot schedules, see [Managing Snapshots](working-with-snapshots.html#adding-a-snapshot-schedule).
   {:tip}
4. Click **Replica** and click **Purchase a replication**.
5. Select the existing snapshot schedule that you want the replication to follow. The list contains all of the active snapshot schedules.
6. Click **Location**, and select the data center that was the original production site.
7. Click **Continue**.
8. Click the **I have read the Master Service Agreement…** check box, and click **Place Order**.

After replication is complete, you need to create a duplicate volume of the new replica.
{:important}

1. Go back to **Storage** > **{{site.data.keyword.filestorage_short}}**.
2. Click the replica of the LUN in the list to view its **Details** page.
3. On the **Details** page, scroll down and select an existing snapshot, then click **Actions** > **Duplicate**.
4. Make any necessary updates to the capacity (to increase size) or IOPs for the new volume.
5. Update the snapshot space for the new volume if needed.
6. Click **Continue** to place your order for the duplicate.

When the duplication process is complete, you can cancel the replication and the volumes that were used to get the data back to the original primary site. The duplicate becomes the primary storage, and replication to the original secondary site can be established again.
