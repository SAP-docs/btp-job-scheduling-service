<!-- loio9b22bbfbaacd49ac8340b06a44240bc4 -->

# Pagination Guide for `GET /scheduler/jobs`

Starting 25 June 2026, the `GET /scheduler/jobs` endpoint enforces pagination on all responses. If you currently call this endpoint without a `page_size` parameter, your response will be limited to 10 jobs by default instead of returning every job in your service instance.



## Context



### Why Is This Changing?

As adoption of SAP Job Scheduling Service grows, service instances are scaling to manage increasingly large volumes of jobs. To keep the service performant, reliable, and delay-free, a hard limit on the number of results returned per request is being introduced.

Pagination ensures that:

-   API responses remain fast regardless of how many jobs you have.

-   Memory and network consumption stay predictable.

-   The service remains stable for all tenants.




### Before/After Comparison


<table>
<tr>
<th valign="top">

Aspect

</th>
<th valign="top">

Before 25 June 2026

</th>
<th valign="top">

After 25 June 2026

</th>
</tr>
<tr>
<td valign="top">

Calling `GET /scheduler/jobs` without parameters

</td>
<td valign="top">

Returns all jobs.

</td>
<td valign="top">

Returns the first 10 jobs. This is the default `page_size` value.

</td>
</tr>
<tr>
<td valign="top">

`page_size` parameter

</td>
<td valign="top">

Optional

</td>
<td valign="top">

Optional. If you don't specify the parameter, the call returns the first 10 jobs.

</td>
</tr>
<tr>
<td valign="top">

Maximum `page_size` 

</td>
<td valign="top">

No enforced limit

</td>
<td valign="top">

100 jobs

</td>
</tr>
<tr>
<td valign="top">

Response fields

</td>
<td valign="top">

`total`, `results` 

</td>
<td valign="top">

`total`, `results`, `prev_url`, `next_url` 

</td>
</tr>
<tr>
<td valign="top">

Getting a list of all jobs

</td>
<td valign="top">

Single request

</td>
<td valign="top">

Iteration through pages

</td>
</tr>
<tr>
<td valign="top">

Response comparison

</td>
<td valign="top">

Returns all jobs:

```
{
  "total": 5000,
  "results": [ /* ...all 5000 job objects... */ ]
}
```



</td>
<td valign="top">

Returns a paginated response with no more than 100 jobs:

```
{
  "total": 5000,
  "results": [ /* ...up to page_size job objects... */ ],
  "prev_url": null,
  "next_url": "/scheduler/jobs?page_size=100&offset=100"
}
```



</td>
</tr>
</table>



### Best Practices

-   Fetch only the jobs you need. Use request parameters like `jobType`, `sort_by`, and `sort_order` to narrow results at the API level. For more information about the available parameter options, see [Retrieve All Jobs](retrieve-all-jobs-b4d3719.md).

-   Always check for 429 and 503 errors in your pagination loop. Retry after the Retry-After duration. For more information, check the code examples on this page.

-   Use `page_size=100` to minimize the number of requests. For example, paginating 10000 jobs requires only 100 requests at `page_size=100`, but requires 1000 requests at `page_size=10`.

-   Monitor the throttling header. If you see it, the API is signaling you to slow down.

-   For very large job sets \(tens of thousands of jobs\), consider adding a small delay \(for example, 100 ms\) between requests to stay well below the limit.

-   Delete jobs you no longer need. Fewer jobs means fewer pages to paginate through, faster responses, and less load on the service.


For more information, see [Rate Limits](rate-limits-a9cb164.md).



### What to Do?

Update all code that assumes all jobs are returned in a single response. Follow these steps:



## Procedure

1.  Consider setting `page_size` explicitly.

    We recommend that you set a value between 1 and 100 that suits your use case. Otherwise, the API returns the first 10 jobs by default.

    **Example:**

    ```
    GET /scheduler/jobs?page_size=100
    ```

2.  Implement pagination in your code.

    The response includes the `prev_url` and `next_url` fields. Use these parameters to navigate through pages, or manually manage pagination with the `offset` parameter.

    -   `next_url`: URL for the next page of results \(`null` if you are on the last page\)

    -   `prev_url`: URL for the previous page \(`null` if you are on the first page\)

    -   `total`: total number of jobs matching your query \(across all pages\)


3.  Update the code that collects all jobs.

    If your code collects all jobs into a single array, wrap the API call in a pagination loop.

    **Examples with `curl`**

    -   Fetch the first page \(100 jobs\):

        ```
        curl -X GET \
          "https://<jobscheduler-host>/scheduler/jobs?page_size=100" \
          -H "Authorization: Bearer <your-token>"
        ```

    -   Fetch the second page:

        ```
        curl -X GET \
          "https://<jobscheduler-host>/scheduler/jobs?page_size=100&offset=100" \
          -H "Authorization: Bearer <your-token>"
        ```

    -   Sort by name in ascending order:

        ```
        curl -X GET \
          "https://<jobscheduler-host>/scheduler/jobs?page_size=50&sort_by=name&sort_order=ASC" \
          -H "Authorization: Bearer 
        ```

    -   Fetch all jobs by looping through pages with a shell script:

        ```
        #!/bin/bash
        
        BASE_URL="https://<jobscheduler-host>/scheduler/jobs"
        TOKEN="<your-token>"
        PAGE_SIZE=100
        OFFSET=0
        ALL_JOBS="[]"
        
        while true; do
          HTTP_CODE=$(curl -s -o /tmp/response.json -w "%{http_code}" -X GET \
            "${BASE_URL}?page_size=${PAGE_SIZE}&offset=${OFFSET}" \
            -H "Authorization: Bearer ${TOKEN}")
        
          # Handle errors and rate limiting
          if [ "$HTTP_CODE" = "429" ] || [ "$HTTP_CODE" = "503" ]; then
            RETRY_AFTER=$(cat /tmp/response.json | jq -r '.retryAfter // 5')
            echo "Rate limited (HTTP ${HTTP_CODE}). Retrying in ${RETRY_AFTER}s..."
            sleep "$RETRY_AFTER"
            continue
          elif [ "$HTTP_CODE" != "200" ]; then
            echo "Error: HTTP ${HTTP_CODE}"
            cat /tmp/response.json | jq '.'
            exit 1
          fi
        
          RESPONSE=$(cat /tmp/response.json)
        
          # Extract results and total
          RESULTS=$(echo "$RESPONSE" | jq '.results')
          TOTAL=$(echo "$RESPONSE" | jq '.total')
          COUNT=$(echo "$RESULTS" | jq 'length')
        
          # Merge results
          ALL_JOBS=$(echo "$ALL_JOBS $RESULTS" | jq -s '.[0] + .[1]')
        
          echo "Fetched ${COUNT} jobs (offset: ${OFFSET}, total: ${TOTAL})"
        
          # Check if we have more pages
          NEXT_URL=$(echo "$RESPONSE" | jq -r '.next_url')
          if [ "$NEXT_URL" = "null" ] || [ -z "$NEXT_URL" ]; then
            break
          fi
        
          OFFSET=$((OFFSET + PAGE_SIZE))
        done
        
        echo "Total jobs collected: $(echo "$ALL_JOBS" | jq 'length')"
        ```


    **Examples with JavaScript/Node.js \(async/await\)**

    > ### Note:  
    > These examples use the built-in fetch API available in Node.js 18 and later. If you're using an older version of Node.js:
    > 
    > 1.  Install the node-fetch package from [https://www.npmjs.com/package/node-fetch](https://www.npmjs.com/package/node-fetch).
    > 
    > 2.  Add the beginning of your script, add the following line:
    > 
    >     ```
    >     add const fetch = require('node-fetch');
    >     ```

    -   Retrieve all jobs with pagination:

        ```
        const BASE_URL = 'https://<jobscheduler-host>/scheduler/jobs';
        const TOKEN = '<your-token>';
        
        async function fetchJobsPage(pageSize = 100, offset = 0) {
          const url = `${BASE_URL}?page_size=${pageSize}&offset=${offset}`;
          const response = await fetch(url, {
            headers: { 'Authorization': `Bearer ${TOKEN}` }
          });
        
          if (!response.ok) {
            throw new Error(`HTTP ${response.status}: ${response.statusText}`);
          }
        
          return response.json();
        }
        
        // Usage
        try {
          const page = await fetchJobsPage(100, 0);
          console.log(`Total jobs: ${page.total}`);
          console.log(`Jobs on this page: ${page.results.length}`);
          console.log(`Next page: ${page.next_url}`);
        } catch (error) {
          console.error('Failed to fetch jobs:', error);
        }
        ```

    -   Fetch all jobs with pagination loop:

        ```
        const BASE_URL = 'https://<jobscheduler-host>/scheduler/jobs';
        const TOKEN = '<your-token>';
        
        async function fetchWithRetry(url, headers, maxRetries = 3) {
          for (let attempt = 1; attempt <= maxRetries; attempt++) {
            const response = await fetch(url, { headers });
        
            if (response.status === 429 || response.status === 503) {
              const retryAfter = parseInt(response.headers.get('Retry-After') || '5', 10);
              console.warn(`Rate limited (${response.status}). Retrying in ${retryAfter}s... (attempt ${attempt}/${maxRetries})`);
              await new Promise(resolve => setTimeout(resolve, retryAfter * 1000));
              continue;
            }
        
            if (!response.ok) {
              throw new Error(`HTTP ${response.status}: ${response.statusText}`);
            }
        
            return response.json();
          }
          throw new Error('Max retries exceeded due to rate limiting');
        }
        
        async function fetchAllJobs(pageSize = 100) {
          const allJobs = [];
          let offset = 0;
          let total = 0;
          const headers = { 'Authorization': `Bearer ${TOKEN}` };
        
          do {
            const url = `${BASE_URL}?page_size=${pageSize}&offset=${offset}`;
            const data = await fetchWithRetry(url, headers);
            allJobs.push(...data.results);
            total = data.total;
            offset += pageSize;
        
            console.log(`Fetched ${allJobs.length} of ${total} jobs...`);
          } while (offset < total);
        
          return allJobs;
        }
        
        // Usage
        try {
          const jobs = await fetchAllJobs();
          console.log(`Collected ${jobs.length} jobs total.`);
        } catch (error) {
          console.error('Failed to fetch jobs:', error);
        }
        ```

    -   Fetch all jobs using `next_url`:

        > ### Remember:  
        > The `next_url` only contains `page_size` and `offset`. It doesn't preserve other query parameters such as `jobType`, `sort_by`, or `sort_order`. If you use filters or sorting, use the offset-based pagination approach instead and re-include those parameters in every request. For more information, see .

        ```
        const HOST = 'https://<jobscheduler-host>';
        const TOKEN = '<your-token>';
        
        async function fetchAllJobsViaNextUrl(pageSize = 100) {
          const allJobs = [];
          let url = `${HOST}/scheduler/jobs?page_size=${pageSize}`;
        
          while (url) {
            const response = await fetch(url, {
              headers: { 'Authorization': `Bearer ${TOKEN}` }
            });
        
            if (!response.ok) {
              throw new Error(`HTTP ${response.status}: ${response.statusText}`);
            }
        
            const data = await response.json();
            allJobs.push(...data.results);
        
            // next_url is a relative path; prepend the host
            url = data.next_url ? `${HOST}${data.next_url}` : null;
          }
        
          return allJobs;
        }
        ```


    **Example with JavaScript/Node.js \(promises\)**

    Fetch all jobs with promise chaining:

    ```
    const BASE_URL = 'https://<jobscheduler-host>/scheduler/jobs';
    const TOKEN = '<your-token>';
    
    function fetchAllJobs(pageSize = 100) {
      const allJobs = [];
    
      function fetchPage(offset) {
        const url = `${BASE_URL}?page_size=${pageSize}&offset=${offset}`;
    
        return fetch(url, {
          headers: { 'Authorization': `Bearer ${TOKEN}` }
        })
          .then(function (response) {
            if (!response.ok) {
              throw new Error('HTTP ' + response.status + ': ' + response.statusText);
            }
            return response.json();
          })
          .then(function (data) {
            allJobs.push.apply(allJobs, data.results);
            console.log('Fetched ' + allJobs.length + ' of ' + data.total + ' jobs...');
    
            if (data.next_url) {
              return fetchPage(offset + pageSize);
            }
            return allJobs;
          });
      }
    
      return fetchPage(0);
    }
    
    // Usage
    fetchAllJobs()
      .then(function (jobs) {
        console.log('Collected ' + jobs.length + ' jobs total.');
      })
      .catch(function (err) {
        console.error('Error fetching jobs:', err);
      });
    ```

4.  Test the implementation.

    Verify that your updated code correctly iterates through all pages:

    1.  Make a paginated request and inspect the response.

        Send a request with the `page_size` parameter and check the response structure:

        ```
        curl -s "https://<jobscheduler-host>/scheduler/jobs?page_size=10" \
          -H "Authorization: Bearer <token>" | jq '{total: .total, results_count: (.results | length), next_url: .next_url, prev_url: .prev_url}'
        ```

        The expected response is:

        ```
        {
          "total": 250,
          "results_count": 10,
          "next_url": "/scheduler/jobs?page_size=10&offset=10",
          "prev_url": null
        }
        ```

        If you have fewer jobs than `page_size`, `results_count` equals `total` and `next_url` is `null`. This behavior is expected and it means that all your jobs fit on one page.

    2.  Understand the pagination fields.

        -   `"prev_url": null`: This means that you're on the first page.

        -   `"next_url": null`: This means that you're on the last or only page.

        -   Both `"prev_url": null` and `"next_url": null`: All jobs fit within the requested `page_size`.

        -   Both `prev_url` and `next_url` have values: You're on the middle page.


    3.  Verify that your pagination loop collects all jobs.

        If you implemented a pagination loop, confirm that it terminates and collects the expected count:

        ```
        const jobs = await fetchAllJobs(100);
        const firstPage = await fetchJobsPage(100, 0);
        
        console.log(`Total reported by API: ${firstPage.total}`);
        console.log(`Jobs collected by loop: ${jobs.length}`);
        ```

        > ### Note:  
        > If jobs are created or deleted while you paginate, the `total` value may change between requests. This is expected. Your loop should still terminate correctly when either `"next_url": null` or `offset` equals or is greater than `total`.



**Related Information**  


[Understanding Offset and Cursor Pagination](understanding-offset-and-cursor-pagination-96ebd22.md "Pagination helps you manage large data sets by breaking them into smaller, more manageable chunks of data. When you retrieve job run logs, you can use two types of pagination: offset pagination and cursor pagination.")

[Rate Limits](rate-limits-a9cb164.md "When you use the SAP Job Scheduling service REST API, rate limits are used to limit the number of requests against the REST API. Requests can be throttled (delayed), and if there is a very high load also denied.")

[Authentication](authentication-5dca60b.md "This section describes how the application accesses the SAP Job Scheduling service REST APIs. The access method depends on the service plan and authentication method you use.")

[REST APIs](rest-apis-3dcd04a.md "SAP Job Scheduling service REST APIs")

[What's New for SAP Job Scheduling Service](../10---What-s-New/what-s-new-for-sap-job-scheduling-service-35dd2f8.md)

[Frequently Asked Questions](../frequently-asked-questions-d72c276.md "Find troubleshooting information in this section. We strongly recommend you use our Guided Answers for step-by-step solutions to some issues that may occur in your work with the SAP Job Scheduling service.")

[Troubleshooting Scenarios](../troubleshooting-scenarios-b05dc8c.md "Find solutions to the most common issues related to SAP Job Scheduling service.")

