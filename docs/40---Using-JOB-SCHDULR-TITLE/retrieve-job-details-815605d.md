<!-- loio815605d5b17d4647939ef0221886de7b -->

# Retrieve Job Details

This API retrieves the saved configuration settings of a specified job.



It also retrieves the job schedules if the `displaySchedules` parameter is true.



## Routes

*GET /scheduler/jobs/\{jobId\} *

You can also use `jobId` or `name` as query parametes to fetch the job details.

-   *GET /scheduler/jobs?name=\{jobName\} *
-   *GET /scheduler/jobs?jobId=\{jobId\}*

> ### Note:  
> If both the parameters are used, ensure that the D matches with the corresponding name.



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

number

</td>
<td valign="top">

ID of the job to be retrieved

</td>
</tr>
</table>

*Query* 


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

`displaySchedules`

</td>
<td valign="top">

No

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Controls if the API should return all the schedule details of the job. Allowed value is true or false.

</td>
</tr>
<tr>
<td valign="top">

`jobId`

</td>
<td valign="top">

Yes

</td>
<td valign="top">

number

</td>
<td valign="top">

ID of the job to be retrieved

</td>
</tr>
<tr>
<td valign="top">

`name`

</td>
<td valign="top">

No

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the job to be retrieved

</td>
</tr>
</table>

Using `jobId` as path parameter

```
GET /scheduler/jobs/3?displaySchedules=true
```

Using `name` as query parameter

```
GET /scheduler/jobs?name=mySalesOrder&displaySchedules=true
```



## Responses



### Status Code: 200

The call was successful and returns the details of the job \(and its schedules, based on the request parameters\).



### Example

```
{
"name": "mySalesOrderJob",
  "description": "cron job that validates sales orders",
  "action": "http://<application-uri>/action",
  "user": "abc",
  "httpMethod": "GET",
  "startTime": null,
  "endTime": null,
  "ansConfig": {
    "onError": true,
    "onSuccess": false
  },
  "signatureVersion": 0,
  "active": true,
  "_id": 3,
  "schedules": [
    {
      "data": {
        "customData": "some_value"
      },
      "type": "recurring",
      "cron": "* * * * * */10 */5",
      "active": false,
      "startTime": "2015-10-19T23:00:00.000Z",
      "endTime": null,
      "scheduleId": "<schedule ID details>",
      "description": "every 10 hours, every 5 minutes"
    }
  ]} 
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

[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the run logs for a specified job schedule.")

[Retrieve Job Run Log Details](retrieve-job-run-log-details-e49a4b2.md "This API retrieves the details for a specified job run log.")

[Create Job Schedule](create-job-schedule-66ab3c1.md "This API creates a job schedule for a specified job.")

[Configure Job Schedule](configure-job-schedule-0a4d939.md "This API configures/updates the runtime information of a job schedule for a specified job.")

[Delete Job Schedule](delete-job-schedule-3066b6d.md "This API deletes the specified job schedule.")

[Activate or Deactivate All Job Schedules](activate-or-deactivate-all-job-schedules-fe9650b.md "This API activates or deactivates all the existing schedules for a job.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Retrieve Job Schedules](retrieve-job-schedules-251658d.md "This API retrieves all schedules for a specified job.")

[Retrieve Jobs](retrieve-jobs-b4d3719.md "This API retrieves all jobs in a service instance.")

[SAP Alert Notification service for SAP BTP](https://help.sap.com/docs/ALERT_NOTIFICATION?version=Cloud)

