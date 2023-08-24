<!-- loio66ab3c1404e34a3b9f04b968ecb3fd5f -->

# Create Job Schedule

This API creates a job schedule for a specified job.



The job configuration settings \(Action URL, HTTP Method, User, Password, and Job Activation Status\) are valid for the new schedule.



## Routes

*POST /scheduler/jobs/\{jobId\}/schedules*



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

ID of the job for which schedules are to be created.



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

`data`



</td>
<td valign="top">

No



</td>
<td valign="top">

object



</td>
<td valign="top">

Data value is passed to the job action endpoint when invoked by Job Scheduler. For the HTTP method “PUT” or “POST”, the data parameters are sent in the request body while invoking the endpoint. For the HTTP method “GET” or “DELETE”, the data parameters are sent as query strings .



</td>
</tr>
<tr>
<td valign="top">

`description` 



</td>
<td valign="top">

No



</td>
<td valign="top">

string



</td>
<td valign="top">

Provides more details about a schedule.



</td>
</tr>
<tr>
<td valign="top">

`active` 



</td>
<td valign="top">

Yes



</td>
<td valign="top">

boolean



</td>
<td valign="top">

Activation status of the job schedule. The allowed values are true or false.



</td>
</tr>
<tr>
<td valign="top">

`startTime` 



</td>
<td valign="top">

No



</td>
<td valign="top">

string/object



</td>
<td valign="top">

Start time for the job schedule. For information about the supported formats, see [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).



</td>
</tr>
<tr>
<td valign="top">

`endTime` 



</td>
<td valign="top">

No



</td>
<td valign="top">

string/object



</td>
<td valign="top">

End time for the job.

For information about the supported formats, see [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).



</td>
</tr>
<tr>
<td valign="top" colspan="4">

`Cron`, `time`, `repeatInterval`, and `repeatAt` are the different scheduling modes available. Use any one that suits your requirement. You must specify at most one scheduling mode.



</td>
</tr>
<tr>
<td valign="top">

`cron` 



</td>
<td valign="top">

\-



</td>
<td valign="top">

string



</td>
<td valign="top">

Crontab pattern for triggering the schedule. For more information, see the section on [Cron Format](../20---Concepts/schedule-formats-54615f0.md#loio37af46344c4d46a9b8695d2c9775c34f).



</td>
</tr>
<tr>
<td valign="top">

`time` 



</td>
<td valign="top">

\-



</td>
<td valign="top">

string



</td>
<td valign="top">

For one-time schedules, this denotes the task execution time. You can use human-readable text to denote a specific time. Example: "3.30pm", "tomorrow at 2am". For information about human readable dates and the supported readable strings, see [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

If an object is used, you must specify the date and time formats as strings. For information about the supported formats, see [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).



</td>
</tr>
<tr>
<td valign="top">

`repeatInterval` 



</td>
<td valign="top">

\-



</td>
<td valign="top">

string



</td>
<td valign="top">

Used to run schedules repeatedly at some interval. Human-readable texts must comply with the rules outlined for human readable dates. For information about the supported formats, see [Human-Readable Date Formats](../20---Concepts/schedule-formats-54615f0.md#loioa323f2d365904499a83a1b60f473bb78).



</td>
</tr>
<tr>
<td valign="top">

`repeatAt` 



</td>
<td valign="top">

\-



</td>
<td valign="top">

string



</td>
<td valign="top">

For recurring schedules, this denotes the exact time when the job schedule must run. The human readable strings must comply with the rules outlined in the section Human Readable Dates. For information about human readable dates and the supported readable strings, see [Human-Readable Date Formats](../20---Concepts/schedule-formats-54615f0.md#loioa323f2d365904499a83a1b60f473bb78).



</td>
</tr>
</table>



### Example

```
PUT /scheduler/jobs/3/schedules
{
    "repeatInterval":"2 hours",
    "active":true, 
    "description":"New Schedule",
    "startTime": {
        "date": "2017-08-21", 
        "format": "YYYY-MM-DD"
    }
}
```



## Responses



### Status Code: 201

The API call was successful and a schedule has been created.

The API responds with a Location header representing the relative resource URI for finding the schedule details.



### Example

```
{
  "repeatInterval": "2 hours",
  "repeatAt": null,
  "time": null,
  "cron": null,
  "data": "{\"order_id\":\"abcd\"}",
  "description": "New Schedule",
  "type": "recurring",
  "active": true,
  "startTime": "2015-04-20 18:30:00",
  "endTime": null,
  "jobId": 3,
  "scheduleId": "<schedule ID details>"
}
```



**Related Information**  


[Create Job](create-job-2c1ecb6.md "This API creates a job by accepting one or more job schedules to be created.")

[Configure Job \(Using ID\)](configure-job-using-id-514f2f6.md "This API configures a job with the updated runtime information using job ID.")

[Configure Job \(Using Name\)](configure-job-using-name-5790b8a.md "This API configures a job with the updated runtime information using job name.")

[Delete Job](delete-job-cd8feb7.md "This API deletes a job and all its runtime information such as schedules and logs.")

[Update Job Run Log](update-job-run-log-e85da40.md "This API is used by the application to inform the Job Scheduler about the status of an asynchronous, long-running job.")

[Retrieve Job Details](retrieve-job-details-815605d.md "This API retrieves the saved configuration settings of a specified job, optionally with its schedules.")

[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the details for a specified job schedule.")

[Retrieve Job Run Log Details](retrieve-job-run-log-details-e49a4b2.md "This API retrieves the details for a specified job run log.")

[Configure Job Schedule](configure-job-schedule-0a4d939.md "This API configures/updates the runtime information of a job schedule for a specified job.")

[Delete Job Schedule](delete-job-schedule-3066b6d.md "This API deletes the specified job schedule.")

[Activate or Deactivate All Job Schedules](activate-or-deactivate-all-job-schedules-fe9650b.md "This API activates or deactivates all the existing schedules for a job.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Retrieve Job Schedule](retrieve-job-schedule-251658d.md "This API retrieves schedule details for a specified job.")

[Retrieve Jobs](retrieve-jobs-b4d3719.md "Retrieve all jobs in a service instance.")

