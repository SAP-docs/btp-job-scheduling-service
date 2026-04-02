<!-- loiobf8f60b0321e4a64bea79f122b57c307 -->

# Search Jobs

This API searches for jobs in a service instance using a query string with optional qualifiers.



> ### Note:  
> The REST API of the SAP Job Scheduling service is available on the SAP Business Accelerator Hub: [https://api.sap.com/api/sap-btpjss-admin-v1/overview](https://api.sap.com/api/sap-btpjss-admin-v1/overview). You can use this resource to explore the API, interact with its endpoints, and generate client libraries for your desired programming language. Refer to and bookmark the API documentation of this service on the SAP Business Accelerator Hub as the API documentation on the SAP Help Portal is planned to be removed in the coming months.



## Routes

*GET /scheduler/search/jobs*



### Request Parameters

*QUERY*


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

`q` 

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

Search query string. Supports free-text search combined with structured qualifiers separated by spaces.

For more information, see the *Search Query Syntax* section on this page.

</td>
</tr>
<tr>
<td valign="top">

`page_size` 

</td>
<td valign="top">

No

</td>
<td valign="top">

number

</td>
<td valign="top">

Number of results the API retrieves.

If you haven't set `page_size` and only `offset` is specified, the `page_size` parameter takes the value of 10.

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

number

</td>
<td valign="top">

Number of results to skip. The default number is 0.

</td>
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

Whether to include schedule details for each job in the response.

Allowed values: `true`, `false`

Default: `true`

</td>
</tr>
</table>



## Search Query Syntax

The `q` parameter accepts a search query string composed of space-separated tokens:

-   **Free text:** Plain text tokens are used for full-text search across job fields \(for example, name, description\).

-   **Qualifiers:** Structured filters using the format `field:operatorValue`.


**Supported Qualifiers**


<table>
<tr>
<th valign="top">

Qualifier

</th>
<th valign="top">

Operators

</th>
<th valign="top">

Value Format

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`active` 

</td>
<td valign="top">

\(equality, no operator needed\)

</td>
<td valign="top">

`true` or `false` 

</td>
<td valign="top">

Filter by job activation status.

</td>
</tr>
<tr>
<td valign="top">

`startTime` 

</td>
<td valign="top">

`<`, `>`, `<=`, `>=` 

</td>
<td valign="top">

`YYYY-MM-DDTHH:mm:ss` or `YYYY-MM-DD` 

</td>
<td valign="top">

Filter by job start time.

</td>
</tr>
<tr>
<td valign="top">

`endTime` 

</td>
<td valign="top">

`<`, `>`, `<=`, `>=` 

</td>
<td valign="top">

`YYYY-MM-DDTHH:mm:ss` or `YYYY-MM-DD` 

</td>
<td valign="top">

Filter by job end time.

</td>
</tr>
</table>



### Examples

-   Free-text search:

    ```
    GET /scheduler/search/jobs?q=salesOrder
    ```

-   Search for active jobs only:

    ```
    GET /scheduler/search/jobs?q=active:true
    ```

-   Combined free-text and qualifier:

    ```
    GET /scheduler/search/jobs?q=salesOrder active:true
    ```

-   Date range filter:

    ```
    GET /scheduler/search/jobs?q=startTime:>2025-01-01 endTime:<2025-12-31
    ```

-   With pagination:

    ```
    GET /scheduler/search/jobs?q=salesOrder&page_size=10&offset=0
    ```

-   Without schedules:

    ```
    GET /scheduler/search/jobs?q=salesOrder&displaySchedules=false
    ```




## Responses



### Status Code: 200

The API call was successful and the search results were retrieved.

Example:

```
{
  "total": 2,
  "results": [
    {
      "_id": 42,
      "name": "validateSalesOrder",
      "description": "cron job that validates sales order requests",
      "action": "https://salesOrderApp.hana.ondemand.com/salesOrders/validate",
      "user": "abc",
      "jobActive": true,
      "httpMethod": "PUT",
      "jobStartTime": null,
      "jobEndTime": null,
      "signatureVersion": 0,
      "schedules": [
        {
          "scheduleId": "cb5c9def-e2a0-4294-8a51-61e4db373f99",
          "scheduleDescription": "this schedule runs every 10 minutes",
          "type": "recurring",
          "active": true,
          "startTime": "2025-01-01 00:00:00",
          "endTime": null,
          "cron": "* * * * * */10 0",
          "repeatInterval": null,
          "repeatAt": null,
          "time": null,
          "data": "{\"salesOrderId\":\"1234\"}",
          "nextRunAt": "2025-08-11 10:00:00"
        }
      ]
    }
  ],
  "pagination_enabled": true,
  "prev_url": null,
  "next_url": "/scheduler/search/jobs?q=salesOrder&page_size=10&offset=10"
}
```

**Response Fields**


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

`total` 

</td>
<td valign="top">

number

</td>
<td valign="top">

Total number of matching results.

</td>
</tr>
<tr>
<td valign="top">

`results` 

</td>
<td valign="top">

array

</td>
<td valign="top">

Array of job objects matching the search query. See *Job Result Fields* on this page.

</td>
</tr>
<tr>
<td valign="top">

`pagination_enabled` 

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Whether pagination is active for this response.

`true` when `page_size` or `offset` is specified.

</td>
</tr>
<tr>
<td valign="top">

`prev_url` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

URL for the previous page of results.

`null` if on the first page or pagination is disabled.

</td>
</tr>
<tr>
<td valign="top">

`next_url` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

URL for the next page of results.

`null` if on the first page or pagination is disabled.

</td>
</tr>
</table>

**Job Result Fields**


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

`_id` 

</td>
<td valign="top">

number

</td>
<td valign="top">

Unique identifier for the job.

</td>
</tr>
<tr>
<td valign="top">

`name` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Name of the job.

</td>
</tr>
<tr>
<td valign="top">

`description` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Job description.

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

The URL endpoint called when the job runs.

</td>
</tr>
<tr>
<td valign="top">

`user` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

User who created the job.

</td>
</tr>
<tr>
<td valign="top">

`jobActive` 

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Whether the job is active.

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

HTTP method of the job action endpoint \(GET, POST, PUT, DELETE\).

</td>
</tr>
<tr>
<td valign="top">

`jobStartTime` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

Job start time in UTC.

</td>
</tr>
<tr>
<td valign="top">

`jobEndTime` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

Job end time in UTC.

</td>
</tr>
<tr>
<td valign="top">

`signatureVersion` 

</td>
<td valign="top">

number

</td>
<td valign="top">

Signature version of the job.

</td>
</tr>
<tr>
<td valign="top">

`schedules` 

</td>
<td valign="top">

array

</td>
<td valign="top">

Array of schedule objects for the job. Only included when `displaySchedules` is `true`. See *Schedule Fields* on this page.

</td>
</tr>
</table>

**Schedule Fields \(Within Job Results\)**


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

`scheduleId` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Unique identifier for the schedule.

</td>
</tr>
<tr>
<td valign="top">

`scheduleDescription` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

Description of the schedule.

</td>
</tr>
<tr>
<td valign="top">

`type` 

</td>
<td valign="top">

string

</td>
<td valign="top">

Schedule type: `recurring` or `one-time` 

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

Whether the schedule is active.

</td>
</tr>
<tr>
<td valign="top">

`startTime` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

Schedule start time in UTC.

</td>
</tr>
<tr>
<td valign="top">

`endTime` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

Schedule end time in UTC.

</td>
</tr>
<tr>
<td valign="top">

`cron` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

Cron expression for the schedule.

</td>
</tr>
<tr>
<td valign="top">

`repeatInterval` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

Repeat interval for the schedule.

</td>
</tr>
<tr>
<td valign="top">

`repeatAt` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

Repeat at time for the schedule.

</td>
</tr>
<tr>
<td valign="top">

`time` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

One-time execution time.

</td>
</tr>
<tr>
<td valign="top">

`data` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

JSON string of data passed to the endpoint.

</td>
</tr>
<tr>
<td valign="top">

`nextRunAt` 

</td>
<td valign="top">

string or null

</td>
<td valign="top">

Next scheduled execution time in UTC.

</td>
</tr>
</table>



### Status Code: 400

The API was unable to process the request due to invalid data provided.

Common error scenarios:

-   Search query not provided \(missing `q` parameter\):

    ```
    {
      "code": 400,
      "message": "Error in Job Scheduler action: Search query not provided",
      "type": "Bad Request/Invalid Request",
      "detailedError": "Error in Job Scheduler action: Search query not provided"
    }
    ```

-   Unrecognized qualifier field name:

    ```
    {
      "code": 400,
      "message": "Error in Job Scheduler action: Field not recognized",
      "type": "Bad Request/Invalid Request",
      "detailedError": "Error in Job Scheduler action: Field not recognized"
    }
    ```

-   Invalid date format \(must be `YYYY-MM-DDTHH:mm:ss` or `YYYY-MM-DD`\):

    ```
    {
      "code": 400,
      "message": "Error in Job Scheduler action: Date format must be YYYY-MM-DDTHH:mm:ss or YYYY-MM-DD",
      "type": "Bad Request/Invalid Request",
      "detailedError": "Error in Job Scheduler action: Date format must be YYYY-MM-DDTHH:mm:ss or YYYY-MM-DD"
    }
    ```

-   Equality operator \(`=`\) used for time qualifiers \(use `<`, `>`, `<=`, `>=` instead\):

    ```
    {
      "code": 400,
      "message": "Error in Job Scheduler action: Operator not specified for startTime",
      "type": "Bad Request/Invalid Request",
      "detailedError": "Error in Job Scheduler action: Operator not specified for startTime"
    }
    ```

-   Invalid `page_size` \(must be a positive number\)

-   Invalid `offset` \(must be a non-negative number\)

-   Invalid `active` qualifier value \(must be `true` or `false`\)


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

[Retrieve Global Parameters](retrieve-global-parameters-06b1142.md "This API retrieves the global configuration parameters for a service instance.")

[Update Global Parameters](update-global-parameters-aa638a7.md "This API updates the global configuration parameters for a service instance.")

[Retrieve Job Count](retrieve-job-count-f9bd567.md "This API retrieves the count of active and inactive jobs for a service instance.")

[Search Schedules](search-schedules-137d28e.md "This API searches for schedules across all jobs in a service instance using a query string with optional qualifiers. Each schedule result includes a parent object with information about the parent job.")

[Search Schedules](search-schedules-137d28e.md "This API searches for schedules across all jobs in a service instance using a query string with optional qualifiers. Each schedule result includes a parent object with information about the parent job.")

