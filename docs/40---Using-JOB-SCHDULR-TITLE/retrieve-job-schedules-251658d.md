<!-- loio251658d477804d8cb53ef94d0ec231ce -->

# Retrieve Job Schedules

This API retrieves all schedules for a specified job.



## Routes

*GET /scheduler/jobs/\{jobId\}/schedules*



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

`jobId` 

</td>
<td valign="top">

Yes

</td>
<td valign="top">

integer

</td>
<td valign="top">

ID of the job whose schedules have to be retrieved.

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

`page_size` 

</td>
<td valign="top">

No

</td>
<td valign="top">

number

</td>
<td valign="top">

Number of job schedules that the API retrieves.

If you haven't set `page_size` and only `offset` is specified, the`page_size` parameter takes the value of 10 job schedules.

</td>
</tr>
<tr>
<td valign="top">

`offset` 

</td>
<td valign="top">

No

</td>
<td valign="top">

number

</td>
<td valign="top">

Number of job schedules to skip. The default number is 1. The default `offset` is an indicator to fetch results without skipping any schedules.

</td>
</tr>
</table>



### Example

```
GET /scheduler/jobs/1/schedules?page_size=10&offset=1 
```



## Responses



### Status Code: 200

The API call was successful and the schedules were retrieved.



### Example

```
{
				{
				"total": 2,
				"results": [
				{
				"scheduleId": "52cd418d-4a13-45fb-a9b7-b2b15f546d5f",
				"description": "updated scheudle",
				"data": "{\"order_id\":\"1234\"}",
				"type": "recurring",
				"cron": "* * * * 10 0 0",
				"repeatInterval": null,
				"repeatAt": null,
				"active": true,
				"startTime": "2015-10-20 00:00:00",
				"endTime": null,
				"time": null,
				"nextRunAt": "2017-08-11 10:00:00"
				}
				],
				"prev_url": "/scheduler/jobs/27/schedules?page_size=1",
				"next_url": null
				}
```



### Status Code: 404

Passing invalid Job ID.



**Related Information**  


[Create Job](create-job-2c1ecb6.md "This API creates a job by accepting one or more job schedules to be created.")

[Configure Job \(Using ID\)](configure-job-using-id-514f2f6.md "This API configures a job with the updated runtime information using job ID.")

[Configure Job \(Using Name\)](configure-job-using-name-5790b8a.md "This API configures a job with the updated runtime information using job name.")

[Delete Job](delete-job-cd8feb7.md "This API deletes a job and all its runtime information such as schedules and logs.")

[Update Job Run Log](update-job-run-log-e85da40.md "This API is used by the application to inform the Job Scheduler about the status of an asynchronous, long-running job.")

[Retrieve Job Details](retrieve-job-details-815605d.md "This API retrieves the saved configuration settings of a specified job.")

[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the run logs for a specified job schedule.")

[Retrieve Job Run Log Details](retrieve-job-run-log-details-e49a4b2.md "This API retrieves the details for a specified job run log.")

[Create Job Schedule](create-job-schedule-66ab3c1.md "This API creates a job schedule for a specified job.")

[Configure Job Schedule](configure-job-schedule-0a4d939.md "This API configures/updates the runtime information of a job schedule for a specified job.")

[Delete Job Schedule](delete-job-schedule-3066b6d.md "This API deletes the specified job schedule.")

[Activate or Deactivate All Job Schedules](activate-or-deactivate-all-job-schedules-fe9650b.md "This API activates or deactivates all the existing schedules for a job.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Retrieve Jobs](retrieve-jobs-b4d3719.md "This API retrieves all jobs in a service instance.")

