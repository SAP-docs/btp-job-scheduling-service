<!-- loiofa16c72ffb31438faa5d896741f52e73 -->

# Retrieve Job Schedule Details

This API retrieves the saved configuration settings of a specified job schedule.



It retrieves the schedule logs if the `displayLogs` parameter is true.



## Routes

*GET /scheduler/jobs/\{jobId\}/schedules/\{scheduleId\}*



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

Integer



</td>
<td valign="top">

ID of the job to which scheduleId belongs



</td>
</tr>
<tr>
<td valign="top">

 `scheduleId` 



</td>
<td valign="top">

Yes



</td>
<td valign="top">

string



</td>
<td valign="top">

ID of the schedule whose details are to be retrieved



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

`displayLogs`



</td>
<td valign="top">

Yes



</td>
<td valign="top">

boolean



</td>
<td valign="top">

Controls whether the API should return all the generated logs for the schedule. Allowed value is true or false.



</td>
</tr>
</table>



### Example

```
GET /scheduler/jobs/3/schedules/cb5c9def-e2a0-4294-8a51-61e4db373f99?displayLogs=true 
```



## Responses



### Status Code: 200

The call was successful and returns the details of the schedule \(and its logs, based on the request parameter\).



### Example

```
{
   "scheduleId": "<schedule ID details>",
    "description": "this schedule runs every 1 hour",
    "data": "{\"salesOrderId\":\"1234\"}",
    "type": "recurring",
    "cron": "* * * * */1 0 0",
    "active": false,
    "startTime": "2015-10-20 04:30:00",
    "endTime": null,
    "nextRunAt": "2017-08-11 10:00:00",
    "logs": [
        {
            "runId": "7841efdb-7ee0-48a6-a8a5-cbcafa1035b9",
            "httpStatus": null,
            "executionTimestamp": null,
            "runStatus": "SCHEDULED",
            "runState": "SCHEDULED",
            "statusMessage": "The job has been scheduled for a future run",
            "scheduleTimestamp": "2017-08-10 11:00:00",
            "completionTimestamp": null,
            "runText": "[{\"time\":\"2017-08-10 11:00:00\",\"type\":\"SCHEDULED\",\"text\":\"\",\"code\":null}]",
            "locale": "en"
        },
        {
            "runId": "a68b86cf-1944-4e78-9cde-889e6bb713b3",
            "httpStatus": 404,
            "executionTimestamp": "2017-08-10 11:00:00", //indicates when actually the scheduler invoked action endpoint
            "runStatus": "COMPLETED",
            "runState": "REQUEST_ERROR",
            "statusMessage": "Error encountered while sending job execution request to the endpoint",
            "scheduleTimestamp": "2017-08-10 10:00:00", //indicates when the schedule was picked up for calculation of next-run
            "completionTimestamp": "2017-08-10 11:00:00", //indicates when the scheduler received response from the action endpoint
            "runText": "[{\"time\":\"2017-08-10 10:00:00\",\"type\":\"SCHEDULED\",\"text\":\"\",\"code\":null},{\"time\":\"2017-08-10 11:00:00\",\"type\":\"TRIGGERED\",\"text\":\"\",\"code\":null},{\"time\":\"2017-08-10 11:00:00\",\"type\":\"REQUEST_ERROR\",\"text\":\"Response: Cannot PUT /health_status\\n\",\"code\":404}]",
            "locale": "en"
        }
    ]
}
```



### Status Code: 404

Passing invalid Job ID.

 

**Related Information**  


[Rate Limits](rate-limits-a9cb164.md "When you use the SAP Job Scheduling service REST API, rate limits are used to limit the number of requests against the REST API. Requests can be throttled (delayed), and if there is a very high load also denied.")

[Create Job](create-job-2c1ecb6.md "This API creates a job by accepting one or more job schedules to be created.")

[Configure Job \(Using ID\)](configure-job-using-id-514f2f6.md "This API configures a job with the updated runtime information using job ID.")

[Configure Job \(Using Name\)](configure-job-using-name-5790b8a.md "This API configures a job with the updated runtime information using job name.")

[Delete Job](delete-job-cd8feb7.md "This API deletes a job and all its runtime information such as schedules and logs.")

[Update Job Run Log](update-job-run-log-e85da40.md "This API is used by the application to inform the Job Scheduler about the status of an asynchronous, long-running job.")

[Retrieve Job Details](retrieve-job-details-815605d.md "This API retrieves the saved configuration settings of a specified job, optionally with its schedules.")

[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the details for a specified job schedule.")

[Retrieve Job Run Log Details](retrieve-job-run-log-details-e49a4b2.md "This API retrieves the details for a specified job run log.")

[Create Job Schedule](create-job-schedule-66ab3c1.md "This API creates a job schedule for a specified job.")

[Configure Job Schedule](configure-job-schedule-0a4d939.md "This API configures/updates the runtime information of a job schedule for a specified job.")

[Delete Job Schedule](delete-job-schedule-3066b6d.md "This API deletes the specified job schedule.")

[Activate or Deactivate All Job Schedules](activate-or-deactivate-all-job-schedules-fe9650b.md "This API activates or deactivates all the existing schedules for a job.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Schedule](retrieve-job-schedule-251658d.md "This API retrieves schedule details for a specified job.")

[Retrieve Jobs](retrieve-jobs-b4d3719.md "Retrieve all jobs in a service instance.")

