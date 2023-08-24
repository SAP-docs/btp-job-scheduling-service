<!-- loiofe9650b079c447c584d5d973d6f585f6 -->

# Activate or Deactivate All Job Schedules

This API activates or deactivates all the existing schedules for a job.



## Routes

*POST /scheduler/jobs/\{jobId\}/schedules/activationStatus*



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

ID of the job whose schedules are to be activated/deactivated



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

`activationStatus`



</td>
<td valign="top">

Yes



</td>
<td valign="top">

boolean



</td>
<td valign="top">

Requested activation status of the job schedules for the specified job. The values allowed are:

-   false: it indicates that all the schedules for the job need to be deactivated.

-   true: it indicates that all the schedules for the job need to be activated.




</td>
</tr>
</table>



### Example

```
POST /scheduler/jobs/3/schedules/activationStatus 
{
  "activationStatus": false
}
```



## Responses



### Status Code: 200

The API call was successful and the activation status of all the schedules were updated.



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

[Update Job Run Log](update-job-run-log-e85da40.md "This API is used by the application to inform the Job Scheduler about the status of an asynchronous, long-running job.")

[Retrieve Job Details](retrieve-job-details-815605d.md "This API retrieves the saved configuration settings of a specified job, optionally with its schedules.")

[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the details for a specified job schedule.")

[Retrieve Job Run Log Details](retrieve-job-run-log-details-e49a4b2.md "This API retrieves the details for a specified job run log.")

[Create Job Schedule](create-job-schedule-66ab3c1.md "This API creates a job schedule for a specified job.")

[Configure Job Schedule](configure-job-schedule-0a4d939.md "This API configures/updates the runtime information of a job schedule for a specified job.")

[Delete Job Schedule](delete-job-schedule-3066b6d.md "This API deletes the specified job schedule.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Retrieve Job Schedule](retrieve-job-schedule-251658d.md "This API retrieves schedule details for a specified job.")

[Retrieve Jobs](retrieve-jobs-b4d3719.md "Retrieve all jobs in a service instance.")

