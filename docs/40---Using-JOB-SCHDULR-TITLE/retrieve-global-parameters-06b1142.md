<!-- loio06b1142ede1242bcb71361d504edccce -->

# Retrieve Global Parameters

This API retrieves the global configuration parameters for a service instance.



> ### Note:  
> The REST API of the SAP Job Scheduling service is available on the SAP Business Accelerator Hub: [https://api.sap.com/api/sap-btpjss-admin-v1/overview](https://api.sap.com/api/sap-btpjss-admin-v1/overview). You can use this resource to explore the API, interact with its endpoints, and generate client libraries for your desired programming language. Refer to and bookmark the API documentation of this service on the SAP Business Accelerator Hub as the API documentation on the SAP Help Portal is planned to be removed in the coming months.



## Routes

*GET /scheduler/globalParameters*



### Request Parameters

This API doesn't require any request parameters.



## Responses



### Status Code: 200

The API call was successful and the global parameters were retrieved.

Example:

```
{
  "config": [
    {
      "CONFIG_NAME": "ASYNC_EXEC_TIMEOUT",
      "CONFIG_VALUE": "604800"
    }
  ]
}
```

**Reponse Fields**


<table>
<tr>
<th valign="top">

Field

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

`config` 

</td>
<td valign="top">

array

</td>
<td valign="top">

Array of configuration parameter objects.

</td>
</tr>
</table>

**Configuration Object Properties**


<table>
<tr>
<th valign="top">

Field

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

`CONFIG_NAME` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the configuration parameter.

</td>
</tr>
<tr>
<td valign="top">

`CONFIG_VALUE` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Current value of the configuration parameter.

</td>
</tr>
</table>


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Default Value

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`ASYNC_EXEC_TIMEOUT` 

</td>
<td valign="top">

604800

</td>
<td valign="top">

Timeout in seconds for asynchronous job executions.

Valid range: positive integer up to 604800 \(7 days\)

</td>
</tr>
</table>

**Related Information**  


[Create Job](create-job-2c1ecb6.md "This API creates a job by accepting one or more job schedules to be created.")

[Retrieve Job Details](retrieve-job-details-815605d.md "This API retrieves the saved configuration settings of a specified job.")

[Retrieve All Jobs](retrieve-all-jobs-b4d3719.md "This API retrieves all jobs in a service instance.")

[Configure Job \(Using ID\)](configure-job-using-id-514f2f6.md "This API configures a job with the updated runtime information using job ID.")

[Configure Job \(Using Name\)](configure-job-using-name-5790b8a.md "This API configures a job with the updated runtime information using job name.")

[Delete Job](delete-job-cd8feb7.md "This API deletes a job and all its runtime information such as schedules and logs.")

[Create Job Schedule](create-job-schedule-66ab3c1.md "This API creates a job schedule for a specified job.")

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Configure Job Schedule](configure-job-schedule-0a4d939.md "This API configures/updates the runtime information of a job schedule for a specified job.")

[Delete Job Schedule](delete-job-schedule-3066b6d.md "This API deletes the specified job schedule.")

[Activate or Deactivate All Job Schedules](activate-or-deactivate-all-job-schedules-fe9650b.md "This API activates or deactivates all the existing schedules for a job.")

[Retrieve Job Schedules](retrieve-job-schedules-251658d.md "This API retrieves all schedules for a specified job.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Run Log Details](retrieve-job-run-log-details-e49a4b2.md "This API retrieves the details for a specified job run log.")

[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the run logs for a specified job schedule.")

[Update Job Run Log](update-job-run-log-e85da40.md "This API is used by the application to inform the Job Scheduler about the status of an asynchronous, long-running job.")

[Update Global Parameters](update-global-parameters-aa638a7.md "This API updates the global configuration parameters for a service instance.")

[Retrieve Job Count](retrieve-job-count-f9bd567.md "This API retrieves the count of active and inactive jobs for a service instance.")

[Search Jobs](search-jobs-bf8f60b.md "This API searches for jobs in a service instance using a query string with optional qualifiers.")

[Search Schedules](search-schedules-137d28e.md "This API searches for schedules across all jobs in a service instance using a query string with optional qualifiers. Each schedule result includes a parent object with information about the parent job.")

[Update Global Parameters](update-global-parameters-aa638a7.md "This API updates the global configuration parameters for a service instance.")

