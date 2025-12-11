<!-- loio13d38f3a64874afc989eb35f1712fc33 -->

# Retrieve Job Run Logs

This API retrieves the run logs for a specified job schedule.



## Routes

*GET /scheduler/jobs/\{jobId\}/schedules/\{scheduleId\}/runs*



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

number

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

ID of the schedule whose run logs have to be retrieved

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

`page_size` 

</td>
<td valign="top">

No

</td>
<td valign="top">

integer

</td>
<td valign="top">

Number of job run logs that the API retrieves.

-   If `page_size` is not set, and only `offset` is specified, the `page_size` parameter will take the value of 10 run logs.

-   If both the `page_size` and `offset` parameters are not set, the retrieved run logs are no more than 200.




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

integer

</td>
<td valign="top">

Number of job run logs to skip. The default number is 0. The default `offset` is an indicator to fetch results without skipping any run logs.

</td>
</tr>
<tr>
<td valign="top">

`next` 

</td>
<td valign="top">

No

</td>
<td valign="top">

string

</td>
<td valign="top">

Returns the next page after a specific run log.

</td>
</tr>
<tr>
<td valign="top">

`prev` 

</td>
<td valign="top">

No

</td>
<td valign="top">

string

</td>
<td valign="top">

Returns the previous page before a specific run log.

</td>
</tr>
</table>



### Examples

```
GET /scheduler/jobs/2/schedules/5f58c2fb-a428-4f4b-9e1d-312e3be8952c/runs?page_size=3&offset=1

```

```
GET /scheduler/jobs/2/schedules/5f58c2fb-a428-4f4b-9e1d-312e3be8952c/runs?page_size=10&next=ef2581c0-a435-11f0-8c7c-331f5a8a59ef
```

```
GET /scheduler/jobs/2/schedules/5f58c2fb-a428-4f4b-9e1d-312e3be8952c/runs?page_size=10&prev=5f1ae560-a481-11f0-988b-27a53d8d12c8
```



## Responses



### Status Code: 200

The call was successful and returns the collection of job run logs.



### Example

```
{
    "total": 64,
    "results": [
        {
            "runId": "a18633fe-b299-41b5-9562-7902c2332070",
            "runText": "Something wrong happened",
            "httpStatus": 500,
            "executionTimestamp": "2015-11-14T04:15:22",
            "runStatus": "COMPLETED",
            "runState": "ERROR",
            "scheduleTimestamp": "2015-11-14T04:13:22",
            "completionTimestamp": "2015-11-14T04:15:22"
        },
        {
            "runId": "e23d217a-f061-4052-8740-6ed9284a56b6",
            "runText": "Request Error: Code:-ENOTFOUND, Message:-getaddrinfo ENOTFOUND www.app.acme.com",
            "httpStatus": 404,
            "executionTimestamp": "2015-11-14T04:17:22",
            "runStatus": "COMPLETED",
            "runState": "REQUEST_ERROR",
            "scheduleTimestamp": "2015-11-14T04:15:22",
            "completionTimestamp": "2015-11-14T04:17:22"
        },
        ...
        {
            "runId": "d0f0e158-73af-4953-a292-9b82ea82ccf9",
            "runText": "Sales order processed",
            "httpStatus": 200,
            "executionTimestamp": "2015-11-14T04:19:22", //indicates when actually the scheduler invoked action endpoint
            "runStatus": "COMPLETED",
            "runState": "SUCCESS",
            "scheduleTimestamp": "2015-11-14T04:17:22", //indicates when the schedule was picked up for calculation of next-run
            "completionTimestamp": "2015-11-14T04:19:22" //indicates when the scheduler received response from the action endpoint
        }
    ],
    "next_url": "/scheduler/jobs/2/schedules/5f58c2fb-a428-4f4b-9e1d-312e3be8952c/runs?page_size=10&next=d0f0e158-73af-4953-a292-9b82ea82ccf9",
    "prev_url": "/scheduler/jobs/2/schedules/5f58c2fb-a428-4f4b-9e1d-312e3be8952c/runs?page_size=10&prev=a18633fe-b299-41b5-9562-7902c2332070"
}
```



### Status Code: 404

The call could not find a run log that matches the provided job ID and schedule ID.



**Related Information**  


[Create Job](create-job-2c1ecb6.md "This API creates a job by accepting one or more job schedules to be created.")

[Configure Job \(Using ID\)](configure-job-using-id-514f2f6.md "This API configures a job with the updated runtime information using job ID.")

[Configure Job \(Using Name\)](configure-job-using-name-5790b8a.md "This API configures a job with the updated runtime information using job name.")

[Delete Job](delete-job-cd8feb7.md "This API deletes a job and all its runtime information such as schedules and logs.")

[Update Job Run Log](update-job-run-log-e85da40.md "This API is used by the application to inform the Job Scheduler about the status of an asynchronous, long-running job.")

[Retrieve Job Details](retrieve-job-details-815605d.md "This API retrieves the saved configuration settings of a specified job.")

[Retrieve Job Run Log Details](retrieve-job-run-log-details-e49a4b2.md "This API retrieves the details for a specified job run log.")

[Create Job Schedule](create-job-schedule-66ab3c1.md "This API creates a job schedule for a specified job.")

[Configure Job Schedule](configure-job-schedule-0a4d939.md "This API configures/updates the runtime information of a job schedule for a specified job.")

[Delete Job Schedule](delete-job-schedule-3066b6d.md "This API deletes the specified job schedule.")

[Activate or Deactivate All Job Schedules](activate-or-deactivate-all-job-schedules-fe9650b.md "This API activates or deactivates all the existing schedules for a job.")

[Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md "This API deletes all the schedules of the specified job.")

[Retrieve Job Schedule Details](retrieve-job-schedule-details-fa16c72.md "This API retrieves the saved configuration settings of a specified job schedule.")

[Retrieve Job Schedules](retrieve-job-schedules-251658d.md "This API retrieves all schedules for a specified job.")

[Retrieve All Jobs](retrieve-all-jobs-b4d3719.md "This API retrieves all jobs in a service instance.")

[Action on Job Run Logs](service-behavior-d09664b.md#loiod09664b7ae9d453e8b8a3a6e09449916__section_RunLogs)

[Understanding Offset and Cursor Pagination](understanding-offset-and-cursor-pagination-96ebd22.md "Pagination helps you manage large data sets by breaking them into smaller, more manageable chunks of data. When you retrieve job run logs, you can use two types of pagination: offset pagination and cursor pagination.")

