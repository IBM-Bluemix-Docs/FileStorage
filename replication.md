---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Working with Replication

Replication uses one of your snapshot schedules to automatically copy snapshots to a destination volume in a remote data center. The copies can be recovered in the remote site in the event of corrupted data or a catastrophic event.

Replicas let you

- Recover from site failures and other disasters quickly by failing over to the destination volume,
- Failover to a specific point in time in the DR copy.

Before you can replicate, you must create a snapshot schedule. When you failover, you’re “"flipping the switch" from your storage volume in your primary data center to the destination volume in your remote data center. For example, your primary data center is London and your secondary data center is Amsterdam. In the case of a failure event, you'd fail over to Amsterdam – connecting to the now-primary volume from a compute instance in Amsterdam. After your volume in London has been repaired, a snapshot is taken of the Amsterdam volume in order to fail back to London and the once-again primary volume from a compute instance in London.


## How do I determine the remote data center for my replicated storage volume?

{{site.data.keyword.BluSoftlayer_full}}'s data centers have been paired into primary and remote combinations worldwide.
See Table 1 for the complete list of data center availability and replication targets.


<table style="width: 80.0%;">
	<caption style="text-align: left;"><p>Table 1 - This table shows the complete list of data centers with enhanced capabilities in each region. Every region is a separate column. Some cities, such as Dallas, San Jose, Washington DC, Amsterdam, Frankfurt, London and Sydney have multiple data centers.</p>
		<p>&#42; Data centers in US 1 region do NOT have enhanced storage. Hosts in data centers with enhanced storage capabilities <strong>can't</strong> initiate replication with replica targets in US 1 data centers.</p>
</caption>
	<thead>
		<tr>
			<th>US 1 &#42;</th>
			<th>US 2</th>
			<th>Latin America</th>
			<th>Canada</th>
			<th>Europe</th>
			<th>Asia-Pacific</th>
			<th>Australia</strong></t>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>DAL01<br />
				DAL05<br />
				DAL06<br />
				HOU02<br />
				SJC01<br />
				WDC01<br />
				<br />
				<br />
				<br />
				<br />
			</td>
			<td>SJC03<br />
			       SJC04<br />
			       WDC04<br />
			       WDC06<br />
			       WDC07<br />
			       DAL09<br />
				DAL10<br />
				DAL12<br />
				DAL13<br />
				<br />
			</td>
			<td>MEX01<br />
				SAO01<br /><br /><br /><br /><br /><br /><br /><br /><br />
			</td>
			<td>TOR01<br />
				MON01<br /><br /><br /><br /><br /><br /><br /><br /><br />
			</td>
			<td>
				AMS01<br />
				AMS03<br />
				FRA02<br />
				FRA04<br />
				LON02<br />
				LON04<br />
				LON06<br />
				OSL01<br />
				PAR01<br />
				MIL01<br />
			</td>
			<td>HKG02<br />
				TOK02<br />
				SNG01<br />
				SEO01<br />
                                CHE01<br />
				<br />
				<br />
				<br />
				<br />
				<br />
			</td>
			<td>
				SYD01<br />
				SYD04<br />
				MEL01<br />
				<br /><br /><br /><br /><br /><br /><br />
			</td>
		</tr>
	</tbody>
</table>


## How Do I Create an Initial Replication?

Replications work off of a snapshot schedule. You must first have snapshot space and a snapshot schedule set up for the source volume before you can replicate. You’ll receive prompts letting you know space needs to be purchased or a schedule set up if you try to set up replication and one or the other is not in place. Replications are managed under **Storage** > **{{site.data.keyword.filestorage_short}}** in the [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window} .

1. Click on your storage volume.
2. Click on the **Replica** tab and click the **Purchase a replication** link.
3. Select an existing snapshot schedule that you want your replications to follow. The list contains all of your active snapshot schedules.
  **Note:** You can only select one schedule even if you have a mix of hourly, daily, and weekly.  All snapshots captured since the previous replication cycle will be replicated regardless of the schedule that originated.
4. Click the **Location** drop-down arrow and select the data center that will be your DR site.
5. Click **Continue**.
6. Enter in a **Promo Code** if you have one and click **Recalculate**. The other fields in the dialog box will default.
7. Click the **I have read the Master Service Agreement…** check box and click **Place Order**.


## How do I edit an existing replication?

You can edit your replication schedule and change your replication space from either the **Primary** or **Replica** tab under **Storage** > **{{site.data.keyword.filestorage_short}}** from the [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}.


## How Do I Edit a Replication Schedule?

You're actually changing a snapshot schedule because your replication schedule is based on an existing snapshot schedule. To change the replica schedule, for example, from Hourly to Weekly, you must cancel the replication schedule and set up a new one.

Changing the schedule can be done on the **Primary** or **Replica** tab.

1. Click the **Actions** menu from either the **Primary** or **Replica** tab.
2. Select **Edit Snapshot Schedule**.
3. Look in the Snapshot frame under Schedule to determine which schedule you're using for replication. Make the changes to the schedule that is being used for replication. For example, if your replication schedule is **Daily**, you can change the time of day replication is to take place.
4. Click **Save**.


## How do I change replication space?

You primary snapshot space and your replica space must be the same. If you change the space on the **Primary** or **Replica** tab, it will automatically add space to both your source and destination data centers. Be aware that increasing snapshot space will trigger an immediate replication update.

1. Click the **Actions** menu from either the **Primary** or **Replica** tab.
2. Select **Add More Snapshot Space**.
3. Select the storage size and click **Continue**.
4. Enter a **Promo Code** if you have one and click **Recalculate**. The other fields in the dialog box will default.
5. Click the **I have read the Master Service Agreement…** check box and click **Place Order**.


## How do I see my replica volumes in the Volume List?

You can view your replication volumes from the {{site.data.keyword.filestorage_short}} page under **Storage** > **{{site.data.keyword.filestorage_short}}**. The Volume Name has the primary volume’s name followed by REP. The Type is Endurance(Performance) – Replica. the Target Address is N/A because the replica volume is not mounted at the replica data center, and the Status is Inactive.



## How do I view a replicated volume's details at the replica data center?

You can view the replica volume details on the **Replica** tab under **Storage** > **{{site.data.keyword.filestorage_short}}**. Another option is to select the replica volume from the **{{site.data.keyword.filestorage_short}}** page and click on the **Replica** tab.



## How do I specify host authorizations before failing over to the secondary data center?

Authorized hosts and volumes must be in the same data center. You can't have a replica volume in London and the host in Amsterdam; both have to be London or both have to be Amsterdam.

1. Click your source or destination volume on the **{{site.data.keyword.filestorage_short}}** page.
2. Click the **Replica** tab.
3. Scroll to the **Authorize Hosts** frame and click on **Authorize Hosts** on the right.
4. Highlight the host that is to be authorized for replications. To select multiple hosts, use the CTRL-key and click the applicable hosts.
5. Click **Submit**. If you have no hosts, the dialog box will offer you the option of purchasing compute resources in the same data center or you can click **Close**.


## How do I increase my snapshot space in my replica data center when I increase space in my primary data center?

Your volume sizes must be the same for your primary and replica storage volumes; one can't be larger than the other. When you increase your snapshot space for your primary volume, the replica space is automatically increased. Be aware that increasing snapshot space will trigger an immediate replication update. The increase to both volumes will show as line items on your invoice and will be prorated as necessary.

Click [here](snapshots.html) for how to increase your snapshot space.

## How do I initiate a failover from a volume to its replica?

In the case of a failure event, you can initiate a **Failover** to your destination, or target, volume. The target volume becomes active. The last successfully replicated snapshot is activated, and the volume becomes available for mounting. Any data written to the source volume since the previous replication cycle will be destroyed. Be aware that when a failover is initiated, the replication relationship flipped. Your target volume is now your source volume, and your former source volume becomes your target as indicated by the **REP** that follows your original LUN Name.

Failovers are initiated under **Storage** > **{{site.data.keyword.filestorage_short}}** from the [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}.

**Before proceeding with this process, it's recommended to disconnect the volume. Failure to do so, will end with corruption and data loss.**

1. Click your active LUN (“source”).
2. Click the Replica tab and click **Actions** in the upper-right corner.
3. Select **Failover**.
   Expect a message across the top stating the failover is in progress. Additionally, an icon appears next to your volume on the **{{site.data.keyword.filestorage_short}}** indicating that an active transaction is occurring. Hovering over the icon produces a dialog indicating the transaction. The icon disappears when the transaction is complete. During the failover process, configuration-related actions are read only. You can't edit any snapshot schedule or change snapshot space, and so on. The event is logged in replication history.
4. When your target volume is live, your original source volume’s LUN Name is updated to include "REP" and its Status shows as Inactive.
4. Click the **View All {{site.data.keyword.filestorage_short}}** link in the upper-right corner.
5. Click your active LUN (formerly your target volume). This volume is now in **Active** status.
6. Mount and attach your storage volume to the host.


## How do I initiate a failback from a volume to its replica?

Once your original source volume has been repaired, the **failback** action lets you initiate a controlled failback to your original source volume. In a controlled failback,

- The acting source volume is taken offline;
- A snapshot is taken;
- The replication cycle is completed;
- The just-taken data snapshot is activated;
- And the source volume is made active for mounting.

Be aware that when a failback is initiated, the replication relationship is flipped again. Your source volume is restored as your source volume, and your target volume is the target volume again as indicated by the **REP** that follows the LUN Name.

Failbacks are initiated under **Storage** > **{{site.data.keyword.filestorage_short}}** from the [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}..

1. Click your active Endurance LUN ("target").
2. Click the **Replica** tab and click **Actions** in the upper-right corner.
3. Select **failback**.
   Expect a message across the top of the page stating the failover is in progress. Additionally, an icon appears next to your volume indicating that an active transaction is occurring. Hovering over the icon produces a dialog indicating the transaction. The icon disappears when the transaction is complete. <br /> During the failback process, configuration-related actions are read only. You can't edit any snapshot schedule, change snapshot space, and so on. The event is logged in replication history.
5. When your source volume is live, your target volume will become Inactive.
4. Click **View All {{site.data.keyword.filestorage_short}}** in the upper-right corner.
5. Click your active LUN (source). This volume is now in an **Active** status.
6. Mount and attach your storage volume to the host. Click [here](provisioning-file-storage.html) for instructions.


## How do I see my replication history?

Replication history is viewed on the **Audit Log** on the **Account** tab under **Manage**. Both the primary and replica volumes display identical replication history, which includes

- Type for replication (failover or failback)
- When it was initiated,
- Snapshot used for the replication
- Size of the replication
- When it completed


## How do I cancel an existing replication?

Cancellation can be performed either immediately or on the anniversary date, which causes billing to terminate. Replication can be canceled from either the **Primary** or **Replica** tabs.

1. Click the volume from the **{{site.data.keyword.filestorage_short}}** page.
2. Click **Actions** on either the **Primary** or **Replica** tab.
3. Select **Cancel Replica**.
4. Select when to cancel. **Immediately** or **Anniversary Date** and click **Continue**.
5. Click the **I acknowledge that due to cancellation, data loss may occur** check box and click **Cancel Replica**.


## How do I cancel replication when the primary volume is canceled?

When a primary volume is canceled, the replication schedule and the volume in the replica data center are deleted. Replicas are canceled from the **{{site.data.keyword.filestorage_short}}** page.

 1. Highlight your volume on the **{{site.data.keyword.filestorage_short}}** page.
 2. Click **Actions** and select **Cancel for {{site.data.keyword.filestorage_short}}**.
 3. Select when to cancel the volume.**Immediately** or **Anniversary Date** and click **Continue**.
 4. Click the **I acknowledge that due to cancellation, data loss may occur** check box and click **Cancel**.
