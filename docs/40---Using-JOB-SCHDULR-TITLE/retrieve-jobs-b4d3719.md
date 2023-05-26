<!-- loiob4d3719173f641b583c97ff0e8f0a7fa -->

# Retrieve Jobs

Retrieve all jobs in a service instance.

> ### Note:  
> This API supports pagination if you’ve set the required parameters. If you haven’t set the required parameters, all jobs are fetched.



<a name="loiob4d3719173f641b583c97ff0e8f0a7fa__section_e4z_mt5_ljb"/>

## Routes

```
GET /scheduler/jobs
```



<a name="loiob4d3719173f641b583c97ff0e8f0a7fa__section_czl_4t5_ljb"/>

## Request Parameters



### Body

**Body of Retrieve Jobs API**


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

 `number` 



</td>
<td valign="top">

Number of job schedules the API retrieves. The default number is `10`.

If you haven't set `page_size` and only `offset` is specified, the `page_size` parameter takes the default value of `10` records.



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

 `number` 



</td>
<td valign="top">

Number of job schedule records to skip. The default number is `1`.

The default offset is an indicator to fetch results without skipping any records.



</td>
</tr>
<tr>
<td valign="top">

 `tenantId` 



</td>
<td valign="top">

No



</td>
<td valign="top">

 `string` 



</td>
<td valign="top">

Tenant ID upon which the job lists are filtered. This parameter applies only if the API is invoked using an access token obtained on behalf of a PaaS tenant from XSUAA.



</td>
</tr>
</table>



### Example

```
GET /scheduler/jobs?page_size=10&offset=1&tenantId=8a324eec-94f1-43ae-b24a-0430aa157e14
```



<a name="loiob4d3719173f641b583c97ff0e8f0a7fa__section_ctj_qt5_ljb"/>

## Responses



### Status Code: 200

The API call was successful and the schedules were retrieved.

Example:

```
{
  "total": 5,
  "results": [
    {
      "jobId": 42,
      "name": "Example_Job",
      "description": "Example_Description",
      "action": "https://exampleapi.cfapps.sap.hana.ondemand.com/api",
      "active": true,
      "httpMethod": "GET",
      "user": null,
      "startTime": null,
      "endTime": null,
      "signatureVersion": 0,
      "jobType": "HTTP_ENDPOINT",
      "subDomain": null,
      "ansConfig": {
        "onError": true,
        "onSuccess": false
      },
      "createdAt": "1970-01-01 12:55:55",
      "ACTIVECOUNT": 0,
      "INACTIVECOUNT": 2
    }
  ],
  "prev_url": null,
  "next_url": "/scheduler/jobs/?page_size=1&offset=1"
}
```



### Status Code: 400

The API was unable to process the request due to invalid data provided.

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

[Activate or Deactivate All Job Schedules](activate-or-deactivate-all-job-schedules-fe9650b.md "This API activates or deactivates all the existing schedules for a job.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Retrieve Job Schedule](retrieve-job-schedule-251658d.md "This API retrieves schedule details for a specified job.")

[SAP Alert Notification service for SAP BTP](https://help.sap.com/docs/ALERT_NOTIFICATION?version=Cloud)

