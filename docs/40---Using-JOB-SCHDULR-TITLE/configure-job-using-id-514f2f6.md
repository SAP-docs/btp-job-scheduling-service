<!-- loio514f2f618c934b8a8aac639adfa1cb29 -->

# Configure Job \(Using ID\)

This API configures a job with the updated runtime information using job ID.



You can update one or more attributes of the job using this API. If a parameter is not provided in the request or is `undefined`, then the existing value for the parameter is retained.

You can also use this API to create a job by providing a job name along with the job in the URI. If you use the API to create a job, the parameters must conform to the same constraints as provided in the create job API. You must also ensure that the job name in the request URI matches with the job name in the request body.



## Routes

*PUT /scheduler/jobs/ \{jobId\}* 



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

ID of the job to be updated

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

Data Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`description`

</td>
<td valign="top">

string

</td>
<td valign="top">

Sets the description of the job.

</td>
</tr>
<tr>
<td valign="top">

`active`

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Determines if a job must be activated or deactivated.

</td>
</tr>
<tr>
<td valign="top">

`action`

</td>
<td valign="top">

string

</td>
<td valign="top">

Sets the job action url.

> ### Note:  
> Relevant for your **production scenario**: To encrypt data during the communication between the SAP Job Scheduling service and the application, make sure that you use HTTPS in the URL for the action endpoint to be called when the job runs.



</td>
</tr>
<tr>
<td valign="top">

`httpMethod` 

</td>
<td valign="top">

string

</td>
<td valign="top">

HTTP method of the job action endpoint URL. Allowed values are “GET”, “POST”, “PUT”, and “DELETE”.

</td>
</tr>
<tr>
<td valign="top">

`startTime` 

</td>
<td valign="top">

string/object/null

</td>
<td valign="top">

Start time for the job. The scheduler respects the start time of both the schedule and the job. For more information about supported formats, see [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

</td>
</tr>
<tr>
<td valign="top">

`endTime` 

</td>
<td valign="top">

string/object/null

</td>
<td valign="top">

End time for the job. The scheduler respects the end time of both the schedule and the job. For more information about supported formats, see [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

</td>
</tr>
<tr>
<td valign="top">

`ansConfig`

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
</table>



### Example

*PUT /scheduler /jobs/3*

```

{
	"active": true,
	"httpMethod": "GET"
}

 
```



## Responses



### Status Code: 200

The call was successful.



### Example

```
{
  "success": true
}
```



### Status Code: 400

The API was unable to process the request because of invalid data provided.

**Related Information**  


[Create Job](create-job-2c1ecb6.md "This API creates a job by accepting one or more job schedules to be created.")

[Configure Job \(Using Name\)](configure-job-using-name-5790b8a.md "This API configures a job with the updated runtime information using job name.")

[Delete Job](delete-job-cd8feb7.md "This API deletes a job and all its runtime information such as schedules and logs.")

[Retrieve Job Details](retrieve-job-details-815605d.md "This API retrieves the saved configuration settings of a specified job.")

[Retrieve All Jobs](retrieve-all-jobs-b4d3719.md "This API retrieves all jobs in a service instance.")

[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the run logs for a specified job schedule.")

[Retrieve Job Run Log Details](retrieve-job-run-log-details-e49a4b2.md "This API retrieves the details for a specified job run log.")

[Update Job Run Log](update-job-run-log-e85da40.md "This API is used by the application to inform the Job Scheduler about the status of an asynchronous, long-running job.")

[Create Job Schedule](create-job-schedule-66ab3c1.md "This API creates a job schedule for a specified job.")

[Configure Job Schedule](configure-job-schedule-0a4d939.md "This API configures/updates the runtime information of a job schedule for a specified job.")

[Delete Job Schedule](delete-job-schedule-3066b6d.md "This API deletes the specified job schedule.")

[Activate or Deactivate All Job Schedules](activate-or-deactivate-all-job-schedules-fe9650b.md "This API activates or deactivates all the existing schedules for a job.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Retrieve Job Schedules](retrieve-job-schedules-251658d.md "This API retrieves all schedules for a specified job.")

[SAP Alert Notification service for SAP BTP](https://help.sap.com/docs/ALERT_NOTIFICATION?version=Cloud)

