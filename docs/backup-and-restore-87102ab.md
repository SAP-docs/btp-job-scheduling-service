<!-- loio87102abccdc64d949c5c7954a26f67ba -->

# Backup and Restore

The SAP Job Scheduling service enables the restoration of accidentally deleted instances and subscriptions. This ensures business continuity and minimizes disruption.

> ### Caution:  
> Jobs and schedules that are created, modified, or deleted on the same day can't be restored. This is because restoration relies on daily database backups. If a backup doesn't exist for that day, restoration isn't possible.



<a name="loio87102abccdc64d949c5c7954a26f67ba__section_fvd_t4p_hgc"/>

## What Is Restored?

-   Job and task configurations

    All defined configurations before deletion, except the active property. The active property is automatically set to false.

-   Schedule configurations

    All defined configurations before deletion, except the active property. The active property is automatically set to false.


> ### Note:  
> Run logs aren't restored by the SAP Job Scheduling service.



<a name="loio87102abccdc64d949c5c7954a26f67ba__section_jp4_ppp_hgc"/>

## Restoration Procedures



### Restoring Jobs/Tasks from Deleted Instance

To restore a SAP Job Scheduling service instance, report a case. For more details on reporting a case, see [Getting Support](https://help.sap.com/docs/btp/sap-business-technology-platform/btp-getting-support).

Provide the following information in the case:


<table>
<tr>
<th valign="top">

Required Information

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Tenant ID

</td>
<td valign="top">

The Tenant ID of the subaccount where the instance was deleted.

</td>
</tr>
<tr>
<td valign="top">

Deletion Timestamp

</td>
<td valign="top">

Date and time of deletion, valid only if within:

-   14 days for AWS and Azure regions

-   7 days for GCP regions




</td>
</tr>
<tr>
<td valign="top">

Old Instance GUID

</td>
<td valign="top">

The Instance ID of the deleted instance. For information on how to obtain it, check the *Troubleshooting* section on this page.

</td>
</tr>
<tr>
<td valign="top">

New Instance GUID

</td>
<td valign="top">

The GUID of the new empty SAP Job Scheduling service instance for recovering deleted jobs/tasks.

</td>
</tr>
</table>

After you've reported the case, await the completion of the restore process. Once restored, the jobs should be visible and accessible again.



### Restoring Jobs from Deleted Subscription

To restore a subscription associated with a multitenant application using the SAP Job Scheduling service, report a case. For more details, see [Getting Support](https://help.sap.com/docs/btp/sap-business-technology-platform/btp-getting-support).

Provide the following information in the case:


<table>
<tr>
<th valign="top">

Required Information

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Tenant ID

</td>
<td valign="top">

The Tenant ID of the subaccount where the instance was deleted.

</td>
</tr>
<tr>
<td valign="top">

Deletion Timestamp

</td>
<td valign="top">

Date and time of deletion, valid only if within:

-   14 days for AWS and Azure regions

-   7 days for GCP regions




</td>
</tr>
<tr>
<td valign="top">

Provider Instance GUID

</td>
<td valign="top">

The Instance ID of the SAP Job Scheduling service where the jobs were previously running.

</td>
</tr>
</table>

After you've reported the case, create a new subscription to the multitenant application. Await the restore process completion. After restoration, jobs should reappear and be fully operational.



<a name="loio87102abccdc64d949c5c7954a26f67ba__section_nvg_zxp_hgc"/>

## Troubleshooting

The following troubleshooting steps are valid only for the Cloud Foundry environment.

1.  If you don't know the deleted instance GUID, you can usually find it on the *Space Events* page in the SAP BTP cockpit, in the space where the instance was created or deleted.

2.  Search for the event `audit.service_instance.delete` and target `{deleted_jobscheduler_instance_name}`.

3.  Below this event, you should find the `audit.service_binding.delete` event. This event includes the deleted instance GUID, provided the instance was bound to an application. You can find this information in the *Description* column in the following format:

    ```
    App GUID: <bound_app_guid>
    Service instance GUID: <deleted_jobscheduler_service_instance>
    ```

4.  If the deleted instance wasn't bound to an application, please report a case for further information and assign it to the **BC-CP-CF-JBS** component.


