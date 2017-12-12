---

copyright:
  years: 2014, 2017
lastupdated: "2017-12-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Working with Snapshots

Snapshots are a feature of {{site.data.keyword.filestorage_full}}. A snapshot represents a volume's contents at a particular point in time. Snapshots enable you to protect your data with no performance impact, minimal consumption of space, and are considered your first line of defense for data protection. Data can be easily and quickly restored from a snapshot copy if a user accidently modifies or deletes crucial data from a volume with the snapshot feature.

{{site.data.keyword.filestorage_short}} provides you with two ways to take your snapshots – through a configurable snapshot schedule that creates and deletes snapshot copies automatically for each storage volume. You can also create additional snapshot schedules, manually delete copies, and manage schedules based on your requirements. The second way is to take a manual snapshot.

A snapshot copy is a read-only image of a {{site.data.keyword.filestorage_short}} volume, that captures the state of the volume at a point in time. Snapshot copies are extremely efficient both in the time needed to create them and in storage space. A {{site.data.keyword.filestorage_short}} snapshot copy takes only a few seconds to create - typically less than 1 second, regardless of the size of the volume or the level of activity on the storage. After a snapshot copy has been created, changes to data objects are reflected in updates to the current version of the objects, as if Snapshot copies did not exist. Meanwhile, the copy of the data remains completely stable. 

A Snapshot copy incurs no performance overhead; users can easily store up to 50 scheduled snapshots and 50 manual snapshots per {{site.data.keyword.blockstorageshort}} volume, all of which are accessible as read-only and online versions of the data.

Snapshots let users

- Non-disruptively create point-in-time recovery points
- Revert volumes to previous points-in-time
- You must purchase some amount of snapshot space for your volume in order to take snapshots of it. The snapshot space can be added during initial volume ordering or after initial provisioning via volume Details page and clicking the Actions drop-down button, and select Add Snapshot Space. Be aware that scheduled and manual snapshots share the snapshot space, so order your space accordingly.

## Snapshot Best Practices
Snapshot design depends on the customer’s environment. The following design considerations will help you to plan and implement Snapshot copies: 
- 	Up to 50 snapshots can be created via schedule and up to 50 manually on each volume or LUN. 
- 	Do not over snap. Make sure that your scheduled snapshot frequency meets your RTO and RPO needs as well as your application business requirements by scheduling hourly, daily or weekly snapshots. 
- 	Snapshot AutoDelete should be used to control the growth of storage consumption. <br/>
    **Note**: the AutoDelete threshold is fixed at 95%.
    
## How do Snapshot Copies Consume Disk Space?
Snapshot copies minimize disk consumption by preserving individual blocks rather than whole files. Snapshot copies begin to consume extra space only when files in the active file system are changed or deleted. When this happens, the original file blocks are still preserved as part of one or more Snapshot copies.
In the active file system, the changed blocks are rewritten to different locations on the disk or removed as active file blocks entirely. As a result, in addition to the disk space used by blocks in the modified active file system, disk space used by the original blocks is still reserved to reflect the status of the active file system before the change.

<table>
    <colgroup>
      <col style="width: 33.3%;"/>
      <col style="width: 33.3%;"/>
      <col style="width: 33.3%;"/>
    </colgroup>
    <tbody>
      <tr>
        <th colspan="3" style="border: 0.0px;text-align: center;">Disk Space Usage Before and After Snapshot Copy</th>
     </tr><tr>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle1.png" alt="Before Snapshot Copy"></td>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle3.png" alt="After Snapshot Copy"></td>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle2.png" alt="Changes after Snapshot Copy"></td>
     </tr><tr>
        <td style="border: 0.0px;">Before any Snapshot copy is created, disk space is consumed by the active file system only.</td>
        <td style="border: 0.0px;">After a Snapshot copy is created, the active file system and Snapshot copy point to the same disk blocks. The Snapshot copy does not use extra disk space.</td>
        <td style="border: 0.0px;">After <i>myfile.txt</i> is deleted from the active file system, the Snapshot copy still includes the file and references its disk blocks. That is why deleting active file system data does not always free up disk space.</td>
      </tr>
    </tbody>
</table>



## How do I Purchase Snapshot Space?

In order to create snapshots of your storage volume, either automated or manually, you need to purchase space to hold them. You can purchase capacity up to your storage volume amount (during the initial volume purchase or later using the below steps).

1. Access your Storage via **Storage** > **{{site.data.keyword.filestorage_short}}** tab of the [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}
2. Click the Add Snapshot Space link in the Snapshots frame.Click the **Purchase snapshot space now** link in the Snapshots frame.
3. Select the amount of space you need by clicking the radio button next to the appropriate amount.
4. Click **Continue**.
5. Enter any Promo Code you have and click **Recalculate**. The Charges for this order and Order Review will have default values.
6. Click the **I have read the Master Service Agreement…** checkbox and click **Place Order**. Your snapshot space will be provisioned in a few minutes.

## How do I Create a Snapshot Schedule?

Snapshot schedules let you decide how often and when you want to create a point-in-time reference of your storage volume. You can have a maximum of 50 snapshots per storage volume. Schedules are managed via the **Storage** > **{{site.data.keyword.filestorage_short}}** tab of the [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}.

Before you can set up your initial schedule, you must first purchase snapshot space if you did not purchase it during the initial provisioning of the storage volume.

### Add a Snapshot Schedule

Snapshots schedules can be set up for hourly, daily, and weekly intervals, each with a distinct retention cycle. There is a maximum of 50 scheduled snapshots, which can be a mix of hourly, daily, and weekly schedules, and manual snapshots per storage volume.

1. Click on your storage volume, click the **Actions** drop-down box, and click **Schedule Snapshot**.
2. In the New Schedule Snapshot dialog there are three different snapshot frequencies to select from. Use any combination of the three to create a comprehensive snapshot schedule.
   - Hourly
      - Specify the minute each hour that a snapshot should be performed; default is the current minute.
      - Specify the number of hourly snapshots to be retained before discarding the oldest.
   - Daily
      - Specify the hour and minute that a snapshot should be performed; default is the current hour and minute.
      - Select the number of hourly snapshots to be retained before discarding the oldest.
   - Weekly
      - Specify the day of the week, hour, and minute that a snapshot should be performed; default is the current day, hour, and minute.
      - Select the number of weekly snapshots to be retained before discarding the oldest.
3. Click **Save** and create another schedule with a different frequency. Note that you will receive a warning message and will not be able to save if the total number of scheduled snapshots is over 50.

A list of the snapshots will display as they’re taken in the Snapshots section of the Detail page.

## How Do I Take a Manual Snapshot?

Manual snapshots can be taken at various points during an application upgrade or maintenance. They also let you take snapshots across multiple machines that have been temporarily inactivated at the application level.

There is a maximum of 50 manual snapshots per storage volume.

1. Click on your storage volume.
2. Click the Actions drop-down box.
3. Click **Take Manual Snapshot**.
The snapshot will be taken and will display in the Snapshots section of the Detail page. Its schedule will be Manual.

## How Do I See a List of Snapshots with Space Consumed and Management Functions?

A list of retained snapshots and space consumed can be seen on the Detail page (**Storage** > **{{site.data.keyword.filestorage_short}}**). Management functions (editing schedules and adding more space) are conducted on the **Detail** page using the **Actions** drop-down menu or links in the various sections on the page.

## How Do I View a List of Retained Snapshots?

Retained snapshots are based on the number you entered in the **Keep the last field** when setting up your schedules. You can view the snapshots that have been taken under the **Snapshot** section. Snapshots are listed by schedule.

## How Do I See How Much Snapshot Space Has Been Used?

The pie chart at the top of the **Details** page displays how much space has been used and how much space is left. You’ll receive notifications when you begin to reach space thresholds – 75%, 90%, and 95%.

## How Do I Change the Amount of Snapshot Space for My Volume?

You may need to add snapshot space to a volume that did not previously have any or may require additional snapshot space. You can add between 5 GB and 4,000 GB depending on your needs. Note: Snapshot space can only be increased and not reduced. You may want to select a smaller amount of space until you determine how much space you actually need. Remember, automated and manual snapshots share the same space.

Snapshot space is changed via **Storage** > **{{site.data.keyword.filestorage_short}}**.

1. Click on your storage volumes, click the **Actions** drop-down box, and click **Add More Snapshot Space**.
2. Select from a range of sizes from the prompt. Sizes typically range from 0 to the size of your volume.
3. Click **Continue** to provision the additional space.
4. Enter any Promo Code you have and click **Recalculate**. The **Charges for this order** and **Order Review** show default values.
5. Click the **I have read the Master Service Agreement…** checkbox and click **Place Order**. Your additional snapshot space will be provisioned in a few minutes.

## How Do I Receive Notifications When I'm Close to My Snapshot Space Limit and Snapshots Are Deleted?

Notifications are sent via support tickets from Support to the Master User on your account when you reach three different space thresholds – 75%, 90%, and 95%.

- 75% capacity: A warning is sent that snapshot space utilization has exceeded 75%. If you heed the warning and manually add space or delete retained and unnecessary snapshots, the action is noted and the ticket’s closed. If you do nothing, you must manually acknowledge the ticket and then it’s closed.
- 90% capacity: A second warning is sent when snapshot space utilization has exceeded 90%. Like with reaching 75% capacity, if you take the necessary actions to decrease the space used, the action is noted and the ticket’s closed. If you do nothing, you must manually acknowledge the ticket and then it’s closed.
- 95% capacity: A final warning is sent. If no action is taken to bring your space below the threshold, a notification is generated and automatic deletion occurs so that future snapshots can be created. Scheduled snapshots are deleted, starting with the oldest, until usage drops below 95%, and will continue to be deleted each time utilization exceeds 95% until it drops below the threshold. If the space is manually increased or snapshots deleted, the warning will be reset and re-issued if the threshold is exceeded again. If no actions are taken, this will be the only warning that will be received.

## How Do I Delete a Snapshot Schedule?

Snapshot schedules can be cancelled via **Storage** > **{{site.data.keyword.filestorage_short}}**.

1. Click on the schedule to be deleted in the **Snapshot Schedules** frame on the **Details** page.
2. Click in the checkbox next to the schedule to be deleted and click **Save**.<br/>
Caution: If you’re using the replication feature, be sure that the schedule you’re deleting is not the schedule that is used by replication. Click [here](replication.html) for more information on deleting a replication schedule.

## How Do I Delete a Snapshot?

Snapshots that are no longer needed can be manually removed to free up space for future snapshots. Deletion is done via **Storage** > **{{site.data.keyword.filestorage_short}}**.

1. Click on your storage volume and scroll down to the Snapshot section to see a list of existing snapshots.
2. Click the Actions drop-down list next to a particular snapshot and click **Delete** to delete the snapshot. This will not affect any future or past snapshots on the same schedule as there is no dependency between snapshots.

Manual snapshots that are not deleted in the way described above, are automatically deleted (oldest first) when you reach space limitations.

## How Do I Restore My Storage Volume to a Specific Point in Time Using a Snapshot?

You may need to take your storage volume back to a specific point in time because of user error or data corruption.

1. Unmount and detach your storage volume from the host.
   - Click [here](accessing-file-storage-linux.html) for {{site.data.keyword.filestorage_short}} on Linux instructions.
2. Click **Storage**, **{{site.data.keyword.filestorage_short}}** in the [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}.
3. Scroll down and click on your volume to be restored. The Snapshots section of the Detail page will display a list of all saved snapshots along with their size and creation date.
4. Click the **Actions** button for the snapshot to be used and click **Restore**. 

   **Note**: Performing a restore will result in a loss of data that has been created or modified since the snapshot being used was taken. Once complete, your storage volume will be returned to the same state it was in when the snapshot was taken. A prompt will appear to notify you of this.
5. Click **Yes** to initiate the restore. You will receive a message across the top of the page stating the volume was restored using the selected snapshot. Additionally, an icon will appear next to your volume on the {{site.data.keyword.filestorage_short}} indicating that an active transaction is in progress. Hovering over the icon produces a dialog indicating the transaction. The icon will disappear once the transaction is complete.
6. Mount and re-attach your storage volume to the host.
   - Click [here](accessing-file-storage-linux.html) for {{site.data.keyword.filestorage_short}} on Linux instructions.
   
**Note**: Restoring a volume will result in deleting all snapshots prior to the restored snapshot.

