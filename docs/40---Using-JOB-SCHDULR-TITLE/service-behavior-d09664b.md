<!-- loiod09664b7ae9d453e8b8a3a6e09449916 -->

# Service Behavior

This topic helps you understand and analyze the behavior of the SAP Job Scheduling service under specific situations.



<a name="loiod09664b7ae9d453e8b8a3a6e09449916__section_w5c_qyt_trb"/>

## Skipped Schedule Executions

If the SAP Job Scheduling service has an issue which causes the schedule executions not to run for at least 20 minutes, the SAP Job Scheduling service skips all missed executions except the last one which is then executed immediately.

The new behavior is intended to stablize the service upon restart if too many missed executions are in the pipeline. Additionally the service does not want to overwhelm the target application with too many requests in a short period of time.



## Example

Schedule \(ID:1\) should be executed every 5 minutes at 11:55, 12:00, 12:05, 12:10, 12:15.

Schedule \(ID:2\) should be executed every 24 hours at 12:10.

The SAP Job Scheduling service has an issue at 11:51 and shuts down.

The SAP Job Scheduling service becomes healthy at 12:13. There is about 22 minutes of outage which is more than 20 minutes.

Schedule \(ID:1\): The SAP Job Scheduling service skipps executions at 11:55, 12:00, 12:05 and executes the last missed one planed at 12:10 at 12:13. Next execution will be run as expected at 12:15.

Schedule \(ID:2\): The SAP Job Scheduling service executes the last missed one planed at 12:10 at 12:13. Next execution will be run as expected at 12:10 on the next day.



## Example

Schedule \(ID:1\) should be executed every 5 minutes at 11:55, 12:00, 12:05, 12:10, 12:15.

Schedule \(ID:2\) should be executed every 24 hours at 12:10.

The SAP Job Scheduling service has an issue at 11:56 and shuts down.

The SAP Job Scheduling service becomes healthy at 12:13. There is about 17 minutes of outage which is less than 20 minutes.

Schedule \(ID:1\): The SAP Job Scheduling service re-executes the three missed executions from 12:00, 12:05 and 12:10 immediatly at 12:13. Next execution will be run as expected at 12:15. No skipped executions.

Schedule \(ID:2\): The SAP Job Scheduling service executes the last missed execution planed at 12:10 at 12:13. Next execution will be run as expected at 12:10 on the next day.



<a name="loiod09664b7ae9d453e8b8a3a6e09449916__section_o5j_2w1_mbb"/>

## Behavior of One-time Schedules

These are schedules that run only once. The behaviors of this schedule are described in the following table:


<table>
<tr>
<th valign="top">

Behavior



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

Schedule deactivated after a successful run or after an error



</td>
<td valign="top">

After a schedule run, whether the run was successful or had an error, the schedule action logs consider the event as DEACTIVATION\_ON\_COMPLETION. The corresponding job remains active.



</td>
</tr>
<tr>
<td valign="top">

Schedule executed on configured time



</td>
<td valign="top">

One-time schedules override the *startTime* configured at the job or schedule level.



</td>
</tr>
<tr>
<td valign="top">

Schedule executed immediately



</td>
<td valign="top">

If time is configured in the past and the *endTime* configured for the job or the schedule level is in the future, the schedule is executed immediately.



</td>
</tr>
<tr>
<td valign="top">

Schedule isn't executed



</td>
<td valign="top">

If time is configured in the past, and *endTime* configured at the job or the schedule level is also in the past, the schedule won't be executed.



</td>
</tr>
</table>



<a name="loiod09664b7ae9d453e8b8a3a6e09449916__section_kls_n34_y2b"/>

## Behavior of Cloud Foundry Tasks

If the creation of a task fails, check if the memory quota available for the space is sufficient.



<a name="loiod09664b7ae9d453e8b8a3a6e09449916__section_sms_fw1_mbb"/>

## Service Downtime and Schedule Runs

The objective of all cloud-based services is to provide availability all the time but downtime is possible. This could be due to issues with platform availability, network stability, planned downtime, and so on. During such occurrences, the service behaves as follows:


<table>
<tr>
<th valign="top">

Schedules



</th>
<th valign="top">

Behavior



</th>
</tr>
<tr>
<td valign="top">

One-time



</td>
<td valign="top">

-   Schedules that were already executed before the occurrence of the downtime won't be executed again when the service comes up.
-   Schedules that were scheduled to run during the occurrence of the downtime are executed when the service comes up.



</td>
</tr>
<tr>
<td valign="top">

Recurring



</td>
<td valign="top">

All the scheduled runs to be executed during the occurrence of the downtime are executed when the service comes up. If the downtime exceeds 20 minutes \(SAP Job Scheduling service SLA defines delays up to 20 minutes\), the action endpoint is called only once.

> ### Example:  
> A recurring schedule is configured to run every five minutes. The last run was at 07:55AM, and the next scheduled run is 08:00AM.
> 
> The service had a downtime starting from 07:59AM to 8:16AM \(such long downtimes are least likely to occur in production\).
> 
> According to the schedule pattern, there were supposed to be 4 runs during the downtime - 08:00AM, 08:05AM, 08:10AM and 08:15AM. When the service comes up, it will execute all these 4 runs at 08:16AM. The schedule will then be run according to the pattern from 08:20AM.



</td>
</tr>
</table>

> ### Note:  
> A scheduled job has a service level agreement of about 20 minutes from the scheduled time.



<a name="loiod09664b7ae9d453e8b8a3a6e09449916__section_RunLogs"/>

## Action on Job Run Logs

The SAP Job Scheduling service will automatically remove run logs 15 days after they're generated. You can archive run logs before the clean-up starts by downloading them to your local system using any of the following options:

-   Use the Retrieve Job Run Logs API.
-   In the service dashboard, navigate to *Schedules* \> *Logs* pane and choose the *Download* option.

**Related Information**  


[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the details for a specified job schedule.")

<a name="loio3aaa1cf65a30407da04d0755d5f92ab6"/>

<!-- loio3aaa1cf65a30407da04d0755d5f92ab6 -->

## Deactivated Schedules

A scheduled job might have a missed run.

This can happen if the SAP Job Scheduling service fails to process the schedule before the scheduled run time and the schedule is deactivated during this time. The SAP Job Scheduling service considers that this deactivated schedule isn't required to run again.

