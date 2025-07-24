<!-- loioe1805f2212844f0c93ad373c02da51be -->

# Schedule Lifecycle

A schedule passes through three lifecycle statuses for each run.

The lifecycle statuses are described in the following table:


<table>
<tr>
<th valign="top">

Status

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

SCHEDULED

</td>
<td valign="top">

The schedule has been queued for a future run.

</td>
</tr>
<tr>
<td valign="top">

RUNNING

</td>
<td valign="top">

The schedule is currently being executed.

</td>
</tr>
<tr>
<td valign="top">

COMPLETED

</td>
<td valign="top">

The schedule run has been completed.

</td>
</tr>
</table>

Each lifecycle status has a transitional state. Their combination helps you analyze and understand the schedule run. You can view the lifecycle details corresponding to a schedule in the schedule logs.

Each combination is described in the following table:


<table>
<tr>
<th valign="top">

Status

</th>
<th valign="top">

Transitional State

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

SCHEDULED

</td>
<td valign="top">

SCHEDULED

</td>
<td valign="top">

The schedule has been queued for a future run.

</td>
</tr>
<tr>
<td valign="top" rowspan="3">

RUNNING

</td>
<td valign="top">

TRIGGERED

</td>
<td valign="top">

The scheduler has triggered a request to the job action endpoint.

</td>
</tr>
<tr>
<td valign="top">

ACK\_RECVD

</td>
<td valign="top">

The application sends an “202 Accepted” message thus acknowledging the request sent by the scheduler.

</td>
</tr>
<tr>
<td valign="top">

ACK\_NOT\_RECVD

</td>
<td valign="top">

Even after a certain time, the application hasn't sent an “202 Accepted” message acknowledging the request sent by the scheduler.

</td>
</tr>
<tr>
<td valign="top" rowspan="4">

COMPLETED

</td>
<td valign="top">

REQUEST\_ERROR

</td>
<td valign="top">

Error encountered while invoking the job action endpoint.

</td>
</tr>
<tr>
<td valign="top">

SUCCESS

</td>
<td valign="top">

The application has successfully executed the job and has replied with a status code \(ranges from 200 to 399 except 202 Accepted\) to the scheduler.

</td>
</tr>
<tr>
<td valign="top">

ERROR

</td>
<td valign="top">

The application has encountered some error during the execution and has sent one of the server error codes as outlined in the HTTP protocol specification.

</td>
</tr>
<tr>
<td valign="top">

UNKNOWN

</td>
<td valign="top">

The application hasn't invoked the Update Job Run Log API to update the scheduler about the status of the job execution. The status will be set as UNKNOWN, after a configurable time interval.

For more information about this API, see [Update Job Run Log](../40---Using-JOB-SCHDULR-TITLE/update-job-run-log-e85da40.md).

</td>
</tr>
</table>

The following table helps you understand the status of actions corresponding to Cloud Foundry tasks:


<table>
<tr>
<th valign="top">

Status

</th>
<th valign="top">

Transitional State

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

SCHEDULED

</td>
<td valign="top">

SCHEDULED

</td>
<td valign="top">

The schedule has been queued for a future run.

</td>
</tr>
<tr>
<td valign="top" rowspan="2">

RUNNING

</td>
<td valign="top">

TRIGGERED

</td>
<td valign="top">

The scheduler has triggered a request to the cloud controller for creating Cloud Foundry tasks.

</td>
</tr>
<tr>
<td valign="top">

ACK\_RECVD

</td>
<td valign="top">

The cloud controller successfully creates a task.

</td>
</tr>
<tr>
<td valign="top" rowspan="3">

COMPLETED

</td>
<td valign="top">

SUCCESS

</td>
<td valign="top">

Cloud Foundry task successfully completed.

</td>
</tr>
<tr>
<td valign="top">

ERROR

</td>
<td valign="top">

Task didn't complete successfully resulting in a non-zero exit code.

</td>
</tr>
<tr>
<td valign="top">

TIMEOUT

</td>
<td valign="top">

Task didn't end within the configured execution timeframe.

</td>
</tr>
</table>

**Related Information**  


[Manage Jobs, Tasks, and Schedules with Service Dashboard](../40---Using-JOB-SCHDULR-TITLE/manage-jobs-tasks-and-schedules-with-service-dashboard-132fd06.md "The SAP Job Scheduling service dashboard enables you to manage jobs and tasks for a service instance.")

