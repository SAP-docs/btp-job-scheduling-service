<!-- loioe49a4b2a8b2d43d3a9e4629ba29521f4 -->

# Retrieve Job Run Log Details

This API retrieves the details for a specified job run log.



## Routes

*GET /scheduler/jobs/\{jobId\}/schedules/\{scheduleId\}/runs/\{runId\}*



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

Integer



</td>
<td valign="top">

ID of the job to which scheduleId belongs



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

ID of the run whose logs are to be retrived



</td>
</tr>
</table>



### Example

```
GET /scheduler/jobs/2/schedules/5f58c2fb-a428-4f4b-9e1d-312e3be8952c/runs/5646889BB133728EE10000000A61A0D8 
```



## Responses



### Status Code: 200

The call was successful and returns details of the job run log.



### Example

```
{
        "runId": "56468DB7B133728EE10000000A61A0D8",
        "runText": "Sales order processed",
        "httpStatus": 200,
        "executionTimestamp": "2015-11-14T04:19:22", //indicates when actually the scheduler invoked action endpoint
        "runStatus": "COMPLETED",
        "runState": "SUCCESS",
        "scheduleTimestamp": "2015-11-14T04:17:22", //indicates when the schedule was picked up for calculation of next-run
        "completionTimestamp": "2015-11-14T04:19:22" //indicates when the scheduler received response from the action endpoint
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

[Retrieve Job Details](retrieve-job-details-815605d.md "This API retrieves the saved configuration settings of a specified job, optionally with its schedules.")

[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the details for a specified job schedule.")

[Create Job Schedule](create-job-schedule-66ab3c1.md "This API creates a job schedule for a specified job.")

[Configure Job Schedule](configure-job-schedule-0a4d939.md "This API configures/updates the runtime information of a job schedule for a specified job.")

[Delete Job Schedule](delete-job-schedule-3066b6d.md "This API deletes the specified job schedule.")

[Activate or Deactivate All Job Schedules](activate-or-deactivate-all-job-schedules-fe9650b.md "This API activates or deactivates all the existing schedules for a job.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Retrieve Job Schedule](retrieve-job-schedule-251658d.md "This API retrieves schedule details for a specified job.")

[Retrieve Jobs](retrieve-jobs-b4d3719.md "Retrieve all jobs in a service instance.")

