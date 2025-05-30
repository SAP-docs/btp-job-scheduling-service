<!-- loio5790b8a42b174f4194f5182ee103e32a -->

# Configure Job \(Using Name\)

This API configures a job with the updated runtime information using job name.



If you use this API to create a job, the parameters must conform to the same constraints as provided in the create job API. You must also ensure that the job name in the request URI matches with the job name in the request body.

> ### Note:  
> If the job name already exists, the API will replace the job content with the new content retaining the same job ID and name.



## Routes

*PUT /scheduler/jobs/ \{name\}*



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

`name` 

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the job to be updated

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

Sets the description of the job.

-   If it's not passed, the value is set to empty.

-   If there is already a description, not sending the property changes the value to "".




</td>
</tr>
<tr>
<td valign="top">

`active` 

</td>
<td valign="top">

No

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Determines if a job must be activated or deactivated.

-   If it's not passed, the value is set to `false`.

-   If the `true` value is already set, not sending the property changes the value to `false`.




</td>
</tr>
<tr>
<td valign="top">

`httpMethod` 

</td>
<td valign="top">

No

</td>
<td valign="top">

string

</td>
<td valign="top">

HTTP method of the job action endpoint URL. Allowed values are `GET`, `POST`, `PUT`, and `DELETE`.

-   If it's not passed, the value is set to `POST`.

-   If a value is already set, not sending the property changes the value to `POST`.




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

string/object/null

</td>
<td valign="top">

End time for the job. The scheduler respects the end time of both the schedule and the job. For more information about supported formats, see [Date and Time Format](../20---Concepts/schedule-formats-54615f0.md#loio333e7ce070c245d0bb8493cff2e3027b).

-   If it's not passed, the value is set to `null`.

-   If a value is already set, not sending the property changes the value to `null`.




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

`calmConfig` 

</td>
<td valign="top">

No

</td>
<td valign="top">

object

</td>
<td valign="top">

The `calmConfig` object has the following boolean key:

-   `enabled`: By default, it is set to false. On true, you can start monitoring jobs in the SAP Cloud ALM dashboard.

    For more information, see [Integration with SAP Cloud ALM](../integration-with-sap-cloud-alm-f82790e.md).




</td>
</tr>
</table>

*Body*

The parameters are the same as in [Create Job](create-job-2c1ecb6.md) API.



### Example

*PUT /scheduler/jobs/newSalesOrderJob* 

```
{
  "name": "newSalesOrderJob",
  "description": "Sales order Job",
  "action": "http://<application-url>/action",
  "active": true,
  "httpMethod": "PUT",
  "ansConfig": {
     "onError": false,
     "onSuccess": false
      },
  "calmConfig": {
     "enabled": true
      },
  "schedules": [
    {
      "cron": "* * * * * */10 0",
      "description": "this schedule runs every 10 minutes",
      "data": {
        "order_id": "1234"
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

The response body is the same as specified in [Create Job](create-job-2c1ecb6.md) API.



### Status Code: 200



### Status Code: 200

The call was successful.



### Example

```
{
  "name": "newSalesOrderJob",
  "action": "http://sales.acme.com/orders",
  "active": true,
  "httpMethod": "PUT",
  "description": "Sales order Job",
  "startTime":
    {
      "date": "2015-10-20 04:30 +0000",
      "format": "YYYY-MM-DD HH:mm Z"
    },
  "endTime": "2026-11-05T08:15:30-05:00",
  "signatureVersion": 0,
  "schedules": [
    {
      "active": true,
      "startTime": "2015-10-20 04:30:00",
      "endTime": null,
      "description": "this schedule runs every 10 minutes",
      "data": "{\"order_id\":\"1234\"}",
      "cron": "* * * * * */10 0",
      "type": "recurring",
      "scheduleId": "63c05418-f399-49ad-b141-e128f1a3b114"
    }
  ],
  "_id": 4
}
```



### Status Code: 201

If you use the API to create job, this response code appears indicating that a new job was created.



### Status Code: 400

The API was unable to process the request due to invalid data provided.



### Examples

-   You are not allowed to leave the `calmConfig` object empty. Provide either `"enabled": true` or `"enabled": false` as properties in the request body:

    ```
    {
      "code": 400,
      "message": "Error while creating job: 'calmConfig' object cannot be empty",
      "type": "Bad Request/Invalid Request",
      "detailedError": "Error while creating job: 'calmConfig' object cannot be empty"
    }
    ```

-   The `enabled` key of the `calmConfig` object is of boolean type. Use `"enabled": true` or `"enabled": false` as properties in the request body:

    ```
    {
      "code": 400,
      "message": "Error while creating job: 'enabled' in 'calmConfig' must be of type 'boolean'",
      "type": "Bad Request/Invalid Request",
      "detailedError": "Error while creating job: 'enabled' in 'calmConfig' must be of type 'boolean'"
    }
    ```

-   There is a typo or an unsupported property:

    ```
    {
      "code": 400,
      "message": "Error while creating job: 'enabled' is a required property for object 'calmConfig'",
      "type": "Bad Request/Invalid Request",
      "detailedError": "Error while creating job: 'enabled' is a required property for object 'calmConfig'"
    }
    ```

-   There is an unsupported property:

    ```
    {
      "code": 400,
      "message": "Error while creating job: '<property>' is not an allowed property for object 'calmConfig'",
      "type": "Bad Request/Invalid Request",
      "detailedError": "Error while creating job: '<property>' is not an allowed property for object 'calmConfig'"
    }
    ```




**Related Information**  


[Create Job](create-job-2c1ecb6.md "This API creates a job by accepting one or more job schedules to be created.")

[Configure Job \(Using ID\)](configure-job-using-id-514f2f6.md "This API configures a job with the updated runtime information using job ID.")

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

[Retrieve Job Schedules](retrieve-job-schedules-251658d.md "This API retrieves all schedules for a specified job.")

[Retrieve All Jobs](retrieve-all-jobs-b4d3719.md "This API retrieves all jobs in a service instance.")

[SAP Alert Notification service for SAP BTP](https://help.sap.com/docs/ALERT_NOTIFICATION?version=Cloud)

