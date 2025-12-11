<!-- loio96ebd22ee6374fb28e8898bce22a335b -->

# Understanding Offset and Cursor Pagination

Pagination helps you manage large data sets by breaking them into smaller, more manageable chunks of data. When you retrieve job run logs, you can use two types of pagination: offset pagination and cursor pagination.



## Offset Pagination

Offset pagination uses a numeric offset to determine where to start returning results. You specify the offset and the page size in your request.

> ### Example:  
> If you set `offset=30` and `page_size=20`, you get results 31 through 50.



### How it works

-   Offset pagination uses a page number or an offset value to fetch a specific subset of results.

-   This approach lets you jump directly to any page in the data set.

-   The result set for a given offset can change over time.




### When to use offset pagination

-   You want to always see the most recent run logs.

-   You don't need to maintain a consistent view of the data as it changes. As schedules run and new run logs are added, the results change even though the pagination properties stay the same.




## Cursor Pagination

Cursor pagination uses a unique identifier called cursor, such as a run ID, to keep track of your position in a data set. Instead of specifying a page number, you use the `next` or `prev` query parameters to fetch the next or previous set of results. This method is especially useful for real-time data or data sets that change often.

In SAP Job Scheduling service, you can currently use cursor pagination only with the *Retrieve Job Run Logs* API. For more information, see [Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md).

> ### Example:  
> You use the request parameter `next=<runId:string>` to get the next page after a specific run log. For example, `GET /scheduler/jobs/2/schedules/5f58c2fb-a428-4f4b-9e1d-312e3be8952c/runs?page_size=10&next=d0f0e158-73af-4953-a292-9b82ea82ccf9`.



### How it works

-   The cursor is relative to a specific run log entry.

-   The result set doesn't change as new run logs are added.

-   Cursor pagination requires you to track the cursor \(run ID\) between requests.

-   The response includes `next_url` and `prev_url` properties. These URLs contain the correct cursor values for navigating to the next or previous page.

    > ### Example:  
    > Here is an example partial response:
    > 
    > > ### Sample Code:  
    > > ```
    > > "next_url": "/scheduler/jobs/2/schedules/5f58c2fb-a428-4f4b-9e1d-312e3be8952c/runs?page_size=10&next=d0f0e158-73af-4953-a292-9b82ea82ccf9",
    > > "prev_url": "/scheduler/jobs/2/schedules/5f58c2fb-a428-4f4b-9e1d-312e3be8952c/runs?page_size=10&prev=a18633fe-b299-41b5-9562-7902c2332070"
    > > 
    > > ```
    > 
    > You use the `next` and `prev` query parameters from these URLs to page forward or backward.

    > ### Note:  
    > If there are no results after the current page, you won't see a `next_url` in the response. Similarly, if there are no results before the current page, the response won't include a `prev_url`.




### When to use cursor pagination

-   You need a consistent view of the data, even as new run logs are added.

-   You want to implement features like limitless scrolling.


**Related Information**  


[Rate Limits](rate-limits-a9cb164.md "When you use the SAP Job Scheduling service REST API, rate limits are used to limit the number of requests against the REST API. Requests can be throttled (delayed), and if there is a very high load also denied.")

[Authentication](authentication-5dca60b.md "This section describes different ways how the application accesses the SAP Job Scheduling service REST APIs depending on the service plan you use.")

[REST APIs](rest-apis-3dcd04a.md "SAP Job Scheduling service REST APIs")

[Retrieve Job Run Logs](retrieve-job-run-logs-13d38f3.md "This API retrieves the run logs for a specified job schedule.")

