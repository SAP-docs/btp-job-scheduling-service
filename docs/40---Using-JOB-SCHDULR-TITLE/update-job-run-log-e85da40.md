<!-- loioe85da409cd574cce85eb79f059cec7d1 -->

# Update Job Run Log

This API is used by the application to inform the Job Scheduler about the status of an asynchronous, long-running job.



An application must call this API after completion of the asynchronous execution of the job. The API expects the status of the job run and optionally an appropriate message.



## Routes

*PUT /scheduler/jobs/ \{jobId\}/schedules/\{scheduleId\}/runs/\{runId\}*

> ### Note:  
> Job Scheduler passes jobId, scheduleId, and runId as part of the request headers while invoking the job action. For more information, see [Asynchronous Mode](../20---Concepts/asynchronous-mode-d9fd81c.md).



### Request Parameters

*Path* 


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Required

</th>
<th valign="top">

Data Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

jobId

</td>
<td valign="top">

Yes

</td>
<td valign="top">

integer

</td>
<td valign="top">

ID of the job to which the scheduleId belongs

</td>
</tr>
<tr>
<td valign="top">

scheduleId

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

ID of the schedule to which runId belongs

</td>
</tr>
<tr>
<td valign="top">

runId

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

ID of the run whose logs are to be retrieved

</td>
</tr>
</table>

*Body* 


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Required

</th>
<th valign="top">

Data Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`success`

</td>
<td valign="top">

Yes

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Indicates the status of the job run. Allowed values are true or false.

</td>
</tr>
<tr>
<td valign="top">

`message`

</td>
<td valign="top">

No

</td>
<td valign="top">

string

</td>
<td valign="top">

Information that accompanies the job run status.

</td>
</tr>
</table>



### Request Example

```
PUT /scheduler/jobs/3/schedules/cb5c9def-e2a0-4294-8a51-61e4db373f99/runs/ea16b621-eaa8-4824-8629-ff6e6221bb56

{
  "success": true,
  "message": "Long running operation to process employee salaries succeeded"
}
```



## Responses



### Status Code: 200

The log for the job run is successfully updated.



### Example

```
{
  "success": true
}
```



**Related Information**  


[Create Job](create-job-2c1ecb6.md "This API creates a job by accepting one or more job schedules to be created.")

[Configure Job \(Using ID\)](configure-job-using-id-514f2f6.md "This API configures a job with the updated runtime information using job ID.")

[Configure Job \(Using Name\)](configure-job-using-name-5790b8a.md "This API configures a job with the updated runtime information using job name.")

[Delete Job](delete-job-cd8feb7.md "This API deletes a job and all its runtime information such as schedules and logs.")

[Retrieve Job Details](retrieve-job-details-815605d.md "This API retrieves the saved configuration settings of a specified job, optionally with its schedules.")

[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the details for a specified job schedule.")

[Retrieve Job Run Log Details](retrieve-job-run-log-details-e49a4b2.md "This API retrieves the details for a specified job run log.")

[Create Job Schedule](create-job-schedule-66ab3c1.md "This API creates a job schedule for a specified job.")

[Configure Job Schedule](configure-job-schedule-0a4d939.md "This API configures/updates the runtime information of a job schedule for a specified job.")

[Delete Job Schedule](delete-job-schedule-3066b6d.md "This API deletes the specified job schedule.")

[Activate or Deactivate All Job Schedules](activate-or-deactivate-all-job-schedules-fe9650b.md "This API activates or deactivates all the existing schedules for a job.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Retrieve Job Schedule](retrieve-job-schedule-251658d.md "This API retrieves schedule details for a specified job.")

[Retrieve Jobs](retrieve-jobs-b4d3719.md "Retrieve all jobs in a service instance.")

