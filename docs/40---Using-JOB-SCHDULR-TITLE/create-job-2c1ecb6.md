<!-- loio2c1ecb6dae0c42b4a850f7c07d1b7124 -->

# Create Job

This API creates a job by accepting one or more job schedules to be created.



## Routes

*POST /scheduler/jobs*



### Request Parameters

*BODY* 


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

`name`

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the job. Name must not contain special characters or only numbers.

> ### Note:  
> The job creation request fails if a job with the same name already exists for the technical user.



</td>
</tr>
<tr>
<td valign="top">

`description` 

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

Provides more details about a job.

</td>
</tr>
<tr>
<td valign="top">

`action` 

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

The fully qualified URL endpoint to be called when the job runs.

> ### Note:  
> Relevant for your **production scenario**: To encrypt data during the communication between the SAP Job Scheduling service and the application, make sure that you use HTTPS in the URL for the action endpoint to be called when the job runs.



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

Activation status of the job \(default value is false\).

</td>
</tr>
<tr>
<td valign="top">

`httpMethod` 

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

The HTTP method to be used to call the job action endpoint URL. Allowed values are “GET”, “POST” , “PUT”, and “DELETE”.

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

string/object/null

</td>
<td valign="top">

Start time for the job. The scheduler respects the start time of both the schedule and the job. For more information about the supported formats, see [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

</td>
</tr>
<tr>
<td valign="top">

`endTime` 

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string/object/null

</td>
<td valign="top">

End time for the job. The scheduler respects the end time of both the schedule and the job. For more information about the supported formats, see [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

</td>
</tr>
<tr>
<td valign="top">

`ansConfig`

</td>
<td valign="top">

No

</td>
<td valign="top">

object

</td>
<td valign="top">

The `ansConfig` object has two boolean keys:

-   `onSuccess`: On true, a success alert notification is sent to the SAP Alert Notification Service. On false, no notification is sent.
-   `onError`: On true, an error alert notification is sent to the SAP Alert Notification Service. On false, no notification is sent.

> ### Restriction:  
> This feature is only available in the Cloud Foundry environment.



</td>
</tr>
<tr>
<td valign="top">

`schedules` 

</td>
<td valign="top">

Yes

</td>
<td valign="top">

array

</td>
<td valign="top">

Contains one or more job schedules to be created.

</td>
</tr>
<tr>
<td valign="top" colspan="4">

The schedules array can be used to create job schedules. Each job schedule is composed of the following parameters:

</td>
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

Data value is passed to the job action endpoint when invoked by Job Scheduler. For the HTTP method “PUT” or “POST”, the data parameters are sent in the request body while invoking the endpoint. For the HTTP method “GET” or “DELETE”, the data parameters are sent as query strings.

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

Start time for the job schedule. For information about the supported formats, see the section on [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

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

End time for the job schedule. For information about the supported formats, see the section on [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

</td>
</tr>
<tr>
<td valign="top" colspan="4">

`cron`, `time`, `repeatInterval`, and `repeatAt` are the different scheduling options available. Use any one of the option that suits your requirement.

> ### Remember:  
> You must specify at most one scheduling mode.



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

string/object

</td>
<td valign="top">

[Human-Readable Date Formats](../20---Concepts/schedule-formats-54615f0.md#loioa323f2d365904499a83a1b60f473bb78) .

If an object is used, you must specify the date and time formats as strings. For information about the supported formats, see the section on [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

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

Used to run schedules repeatedly at some interval. Human-readable texts must comply with the rules outlined for human readable dates. For information about the supported formats, see the section on For one-time schedules, this denotes the task execution time. You can use human-readable text to denote a specific time. Example: "3.30pm", "tomorrow at 2am". For information about human readable dates and the supported readable strings, see the section on [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

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

For recurring schedules, this denotes the exact time when the job schedule must run. The human readable strings must comply with the rules outlined in the section Human Readable Dates. For information about human readable dates and the supported readable strings, see the section on [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

</td>
</tr>
</table>



### Example

*POST /scheduler/jobs* 

```
For one-time schedules, this denotes the task execution time. 

{
  "name": "validateSalesOrder",
  "description": "cron job that validates sales order requests",
  "action": "http://salesOrderApp.hana.ondemand.com:40023/salesOrders/validate",
  "active": true,
  "httpMethod": "PUT",
  "ansConfig": {
     "onError": false,
     "onSuccess": false
      },
  "schedules": [
    {
      "cron": "* * * * * */10 0",
      "description": "this schedule runs every 10 minutes",
      "data": {
        "salesOrderId": "1234"
      },
      "active": true,
      "startTime": {
        "date": "2015-10-20 04:30 +0000",
        "format": "YYYY-MM-DD HH:mm Z"
      }
    }
  ]
}
```



## Responses



### Status Code 201

The call was successful and the Job has been created. The API responds with a **Location** header which represents the relative resource URI for finding the job details.



### Example

```
{
  "name": "validateSalesOrder",
  "action": "http://<application-url>/action",
  "active": true,
  "httpMethod": "PUT",
  "description": "cron job that validates sales order requests",
  "startTime": null,
  "endTime": null,
  "signatureVersion": 0,
  "schedules": [
    {
      "active": true,
      "startTime": "2015-10-20 04:30:00",
      "endTime": null,
      "description": "every 10 seconds, every 2 minutes",
      "data": "{\"salesOrderId\":\"1234\"}",
      "cron": "* * * * * * */10",
      "type": "recurring",
      "scheduleId": "schedule ID details"
    }
  ],
  "_id": 3
}
```



### Status Code 400

The API was unable to process the request due to invalid data provided.



**Related Information**  


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

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Retrieve Job Schedule](retrieve-job-schedule-251658d.md "This API retrieves schedule details for a specified job.")

[Retrieve Jobs](retrieve-jobs-b4d3719.md "Retrieve all jobs in a service instance.")

[SAP Alert Notification service for SAP BTP](https://help.sap.com/docs/ALERT_NOTIFICATION?version=Cloud)

