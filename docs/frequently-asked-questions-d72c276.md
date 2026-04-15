<!-- loiod72c276ec60c4bbe89c0b9328a926500 -->

# Frequently Asked Questions

Find troubleshooting information in this section. We strongly recommend you use our **Guided Answers** for step-by-step solutions to some issues that may occur in your work with the SAP Job Scheduling service.

For more information, see [Guided Answers](https://ga.support.sap.com/dtp/viewer/#/tree/2797/actions/40871).



<a name="loiod72c276ec60c4bbe89c0b9328a926500__section_dwx_hhd_x1b"/>

## General Questions

**What is the component to raise a ticket for issues related to the SAP Job Scheduling service?**

The support component for the SAP Job Scheduling service is **BC-CP-CF-JBS**.

**What are the prerequisites to use the SAP Job Scheduling service?**

-   You need access to the SAP Job Scheduling service. Check the Cloud Foundry marketplace to see if the service is available.

-   For jobs with action endpoints, you need an authentication service instance. Depending on your chosen authentication method:

    -   XSUAA \(default\): Create a SAP Authorization and Trust Management service instance.

    -   SAP Cloud Identity Services - Identity Authentication: Create a Cloud Identity Services service instance.


    Both services are available in the service marketplace.


**What is the service level agreement \(SLA\) of a scheduled job?**

A scheduled job has a service level agreement of about 20 minutes from the scheduled time.

**As a subscription customer, what does the number of units selected on SAP Store indicate?**

Currently, the number of units selected on SAP Store indicates the number of SAP Job Scheduling service instances that can be created.

> ### Example:  
> If you choose a value of 5, you can create 5 instances of the SAP Job Scheduling service.



<a name="loiod72c276ec60c4bbe89c0b9328a926500__section_t3s_jhd_x1b"/>

## Service Dashboard

**How to access the dashboard or the SAP Job Scheduling service?**

You can use SAP BTP cockpit or the command line interface to access the dashboard or the SAP Job Scheduling service.

-   1.  From the SAP BTP cockpit, choose your application.

2.  From the navigation panel, choose **Service Bindings**.

3.  Select the SAP Job Scheduling service instance and choose the ![](images/Open_Dashboard_icon_56d92fb.png) \(Open Dashboard\) icon from the *Actions* column. This launches the dashboard.


-   From the command line interface

    1.  Enter the command to fetch service instance details `cf service <service-instance-name>`.

    2.  From the listed service instance details, copy the dashboard URL and paste the URL in a Web browser.

    3.  Enter the credentials to log on to your SAP BTP account.



**When I initially accessed the dashboard, I didn't grant the SAP Job Scheduling service any permissions. Now I get an error response \(`500`\). What can I do?**

If your account is missing the authorization for a service, you can grant or revoke the access rights on the login route of the corresponding landscape:

```
https://uaa.<landscape.url.com>/profile
```

For eu10, for example, the login route looks as follows:

> ### Sample Code:  
> ```
> https://uaa.cf.eu10.hana.ondemand.com/profile
> ```

For more information, see [Regions](https://help.sap.com/viewer/3504ec5ef16548778610c7e89cc0eac3/Cloud/en-US/350356d1dc314d3199dca15bd2ab9b0e.html).

**How can I access my job logs from the dashboard?**

From the dashboard, choose a job. This lists all the schedules for the job. Choose a schedule to view the logs.



<a name="loiod72c276ec60c4bbe89c0b9328a926500__section_sr2_khd_x1b"/>

## Date-Time and Cron Formats

**How to provide the cron format ?**

SAP Job Scheduling service supports the SAP cron format. For more information, see [Cron Format](20---Concepts/schedule-formats-54615f0.md#loio37af46344c4d46a9b8695d2c9775c34f).

**Does SAP Job Scheduling service support Linux Cron format?**

No, SAP Job Scheduling service does not support the Linux cron format. Only the SAP cron format is supported.



<a name="loiod72c276ec60c4bbe89c0b9328a926500__section_r5v_k41_bbb"/>

## Schedules and Their Executions

**Why is my schedule not getting triggered?**

This can occur if the date-time format or the cron format is not appropriately specified or the specified endTime is in the past. Verify the schedule settings.

**Why is my job not getting executed at the right time as per the specified format?**

SAP Job Scheduling service runs jobs in the UTC time zone. Verify if the jobs are executed in the UTC time zone as per the format.

**Why is my schedule getting deactivated automatically?**

This can happen if the following applies:

-   For one-time schedules after their execution

-   For cron patterns if there is no valid future execution date

-   If the end time of the job or schedule is reached

-   If the SAP Job Scheduling service can't reach the action endpoint for more than 10 days consistently, then the SAP Job Scheduling service deactivates this schedule with the next maintenance activity. The deactivation is then logged in the action history of the schedule.

**I receive run-log details with runStatus "Running" and runState "ACK\_NOT\_RECVD". Why does this happen?**

This occurs in case of asynchronous jobs. SAP Job Scheduling service can access the action endpoint but the application does not update the status of the run log using Run Log Update API as expected. Thus, the job has the ACK\_NOT\_RECVD status.

To resolve the issue, update your application such that it notifies SAP Job Scheduling service after processing of the job is complete.

**How can I create a one-time schedule that is immediately executed using the API?**

You can create a one-time schedule with the following POST request:

```
POST /scheduler/jobs/3/schedules
{
    "active":"true",
    "description":"One-time schedule that will be executed immediately",
    "time": "now"
} 
```

For more information, see [Create Job Schedule](40---Using-JOB-SCHDULR-TITLE/create-job-schedule-66ab3c1.md).

**My schedule has disappeared. Why did this happen?**

Was your job a one-time schedule? One-time schedules are deleted if they haven't been run in the last 30 days.



<a name="loiod72c276ec60c4bbe89c0b9328a926500__section_uhv_kkh_2fb"/>

## Multitenancy

**General**

**What do you mean by multitenancy in the context of the SAP Job Scheduling service?**

SAP Job Scheduling service invokes action endpoints of applications configured as job actions while registering the job.

A multitenant application in SAP BTP can register jobs on behalf of a tenant \(or subaccount\) who has subscribed to the application.

A multitenant application can retrieve information \(tenant ID, subdomain, and so on\) of the tenant \(or subaccount\) on behalf of which the application should execute the job when the SAP Job Scheduling service invokes the application's action endpoint.

Multitenancy in SAP Job Scheduling service enables multitenant applications in SAP BTP to register jobs on behalf of tenants \(or subaccounts\) who have subscribed to the application. It also enables the multitenant application to be aware of tenant information \(tenant ID, subdomain, and so on\) for whom the job has to be executed when the SAP Job Scheduling service invokes its action endpoint.

**Platform as a Service Tenant**

**How can I register a job on behalf of a tenant \(or subaccount\) where my multitenant application is deployed?**

The SAP Job Scheduling service instance receives the credentials required to register and manage jobs when the instance of the service is bound to a multitenant application.

To register a job on behalf of a tenant \(subaccount\), fetch an access token from the User Access and Authorization \(XSUAA\) service as follows:

-   Fetch clientid, clientsecret, and URL from the UAA section of the SAP Job Scheduling service instance bound with your application
-   Use Post /oauth/token
-   Use body format: x-www-form-urlencoded
-   Use parameters: client\_id \(as fetched from previous step\)
-   Use client\_secret \(as fetched from previous step\)
-   Use grant\_type: client\_credentials
-   Use response\_type: token

Using the access token received, invoke the SAP Job Scheduling service REST API to create a job. The access token has to be used in the header as **Authorization:Bearer**.

Such jobs will provide the tenant details of the multitenant application in the access token while invoking the configured job action.

**How can I register a Job on behalf of a tenant, which has subscribed to my multitenant application?**

A SAP Job Scheduling service instance bound to your multitenant application receives the credentials required to register and manage jobs. To register jobs on behalf of the tenant \(subaccount\) subscribed to your multitenant application, fetch an access token from the XSUAA service using the steps below:

Use the libraries provided by the XSUAA service.

Exchange the access token received from your logged user for a SAP Job Scheduling service token using the method **requestToken** and type as USER\_TOKEN.

Refer library documentation for more specific details on how to obtain an access token using the user\_token grant type. Using the access token received, invoke SAP Job Scheduling service REST API to create Job. The access token has to be used in header as authorization: bearer

The jobs thus created will provide the SaaS tenant \(subaccount\) details in the access token while invoking the configured job action.

**How can I register a Job on behalf of a Tenant when a user is not logged on to my multitenant application?**

If you want to create/delete/update/fetch a job on behalf of a SaaS tenant who has not logged on to your multitenant application, you can use client credentials flow with SaaS user subdomain. The XSUAA API to request a token with client credentials flow is mentioned at the following link: [https://docs.cloudfoundry.org/api/uaa/version/4.23.0/index.html\#client-credentials-grant](https://docs.cloudfoundry.org/api/uaa/version/4.23.0/index.html#client-credentials-grant)

Note that you must use **jwt** as **token\_format** \(instead of **opaque**\). You receive a URL concatenated by **oauth/token** as described in the topic available at the link mentioned above. Further, remember that you need to replace the URL subdomain with the corresponding SaaS subdomain for which the token is requested. Using the access token that you receive, call the SAP Job Scheduling service REST API to Create Job. The access token has to be used in the header as **Authorization: Bearer**. Such created jobs will provide the SaaS tenant \(or subaccount\) details in the access token while calling the job action that you configured.

**How can I fetch all Jobs or a specific Job \(using id or name\) registered in my SAP Job Scheduling service instance?**

You can fetch all jobs registered in your service instance as client, client secret, and URL from the UAA section of the SAP Job Scheduling service instance bound with your application.

Use POST / oauth/token, body format: x-www-form-urlencoded, parameters: client\_id \(fetched from previous step\), client\_secret \(fetched from previous step\), grant\_type is client\_credentials, response\_type as token.

Using the access token received, invoke SAP Job Scheduling service REST API to fetch all jobs using job ID or name. The access token has to be used in the header as authorization:bearer.

**Can I filter on tenant while fetching Jobs registered for a Tenant?**

Yes you can filter on tenant while fetching jobs registered for a tenant. If you have obtained an access token with grant type as client\_credentials using the credentials from SAP Job Scheduling service instance binding, you can invoke the REST API to fetch all the jobs with tenantID as query parameter.

Example: GET https:///scheduler/jobs?tenantId=<tenantID\>

This will retrieve all jobs registered on behalf of the tenant with tenant ID details. However, this query parameter based filter is not applicable if the token used belongs to a SaaS tenant and the API will return Status Code 400. This filtering is required to restrict access of a SaaS tenant to jobs created for another SaaS tenant.

**Where do I find the tenant information when SAP Job Scheduling service invokes the action endpoint of the multitenant application?**

The tenant information is provided in the access token sent by the SAP Job Scheduling service in the request headers while invoking the action endpoint. You may use the convenient client libraries provided by XSUAA to parse the information out of the access token. You will receive information like tenant id, subdomain, grant type and so on.

**Which jobs does the Service Dashboard show when I launch it for a service instance from SAP BTP cockpit?**

The service dashboard shows the jobs created in your service instance along with its tenant ID. It will also list the tenant information in the overview page for all the jobs. You may also sort the jobs based on tenant ID by clicking on the table header.

**Can I create tenant-specific jobs from Service Dashboard?**

No. Creating a job from service dashboard will always create a job specific to the PaaS tenant. If you are trying to create a job specific for a SaaS tenant who has subscribed to your multitenant application, you need to exchange the JSON Web Token \(JWT\) with XSUAA and fetch a token specific for SAP Job Scheduling service \(using client\_id and client\_secret provided to your application by SAP Job Scheduling service instance binding\).

**Software as a Service Tenant**

**How can I fetch Jobs registered for a SaaS Tenant?**

You can fetch all jobs registered for a SaaS tenant using the libraries provided by XSUAA service, exchange the access token received from the logged user for the SAP Job Scheduling service token using the method requestToken and type as USER\_TOKEN.

Refer the API Client library documentation for more specific details on how to obtain an access token using user\_token grant type. Using the access token received, invoke the SAP Job Scheduling service REST API to fetch all jobs. The access token has to be used in header as authorization: bearer.



<a name="loiod72c276ec60c4bbe89c0b9328a926500__section_ddv_3rr_zbc"/>

## REST API

**Can I create a CF task using the REST API?**

You cannot create CF tasks using the REST API because they are bound to a specific application. Only developers with the Space Developer role are authorized to create such tasks.

If you have the Space Developer role, you can create a task in the Job Scheduling service dashboard. When you access the dashboard, go to *Tasks* and choose *Create Task*.



<a name="loiod72c276ec60c4bbe89c0b9328a926500__section_t3y_thn_53c"/>

## Pagination for `GET /scheduler/jobs`

**Does this change affect my existing code?**

Yes. If your code calls `GET /scheduler/jobs` without `page_size` and expects all jobs in a single response, it will now only receive the first 10 jobs. To retrieve all jobs, add `page_size` and implement a pagination loop. For more information, see [Pagination Guide for GET /scheduler/jobs](40---Using-JOB-SCHDULR-TITLE/pagination-guide-for-get-scheduler-jobs-9b22bbf.md).

**What happens if I don't update my code?**

During the rollout windows, and permanently after the rollout is complete, any call to `GET /scheduler/jobs` that doesn't include `page_size` will return only the first 10 jobs instead of all jobs.

If your application relies on getting a complete list in one call, it will silently receive an incomplete result. This can lead to missing data, broken reports, or incorrect behavior. The API won't return an error, but it will return fewer results than expected.

**How do I request more time?**

If you need more time to make this change, report a case using the **BC-CP-CF-JBS** component. In the description, include your service instance ID and a brief explanation of your migration timeline.

**How do I test before June 25?**

You can start testing pagination right away. The `page_size` and `offset` parameters are already available. To verify that your code handles the paginated response correctly, add `page_size=100` to your existing calls. For more information, see *step 4: Test the implementation* in [Pagination Guide for GET /scheduler/jobs](40---Using-JOB-SCHDULR-TITLE/pagination-guide-for-get-scheduler-jobs-9b22bbf.md).

**What if I have more than 100 jobs?**

Use a pagination loop to iterate through all pages. Set `page_size=100` \(the maximum\) and increment the `offset` by 100 on each request until you've collected all jobs. For example, if you have 500 jobs, your loop will make 5 requests.

For more information, check the code examples with curl, JavaScript \(async/await\), and JavaScript \(Promises\) in [Pagination Guide for GET /scheduler/jobs](40---Using-JOB-SCHDULR-TITLE/pagination-guide-for-get-scheduler-jobs-9b22bbf.md).

**Does this change affect the SAP Job Scheduling service dashboard?**

No. This change only affects direct API calls to `GET /scheduler/jobs`. If you only interact with jobs through the dashboard, no action is required.

**Is there a way to get all jobs in one call?**

No. After 25 June 2026, all responses are paginated with a maximum of 100 jobs per page. You can't bypass this limit.

**Can I still look up a single job by `name` or `jobId`?**

Yes. Single-job lookups via the `name` or `jobId` query parameters aren't affected by pagination. However, you can't combine `name` or `jobId` with `page_size` or `offset`. If you do, the API returns a 400 Bad Request error:

```
{
  "code": 400,
  "message": "Error while fetching job details: Invalid query",
  "type": "Bad Request/Invalid Request",
  "detailedError": "Error while fetching job details: Invalid query"
}
```

**Does `next_url` preserve my filters and sort order?**

No. The `next_url` field only includes the `page_size` and `offset` parameters. If you use `jobType`, `sort_by`, `sort_order`, or other filters, they're silently dropped when you follow `next_url`.

When you use filters or sorting, manage pagination manually with `offset` and re-include those parameters in every request:

```
const BASE_URL = 'https://<jobscheduler-host>/scheduler/jobs';
const TOKEN = '<your-token>';

async function fetchAllJobs(pageSize = 100, filters = {}) {
  const allJobs = [];
  let offset = 0;
  let total = 0;

  // Build query params once — reuse on every page
  const params = new URLSearchParams({ page_size: pageSize, ...filters });

  do {
    params.set('offset', offset);
    const url = `${BASE_URL}?${params}`;
    const response = await fetch(url, {
      headers: { 'Authorization': `Bearer ${TOKEN}` }
    });

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }

    const data = await response.json();
    allJobs.push(...data.results);
    total = data.total;
    offset += pageSize;
  } while (offset < total);

  return allJobs;
}

// Usage with filters
const jobs = await fetchAllJobs(100, {
  jobType: 'HTTP_ENDPOINT',
  sort_by: 'name',
  sort_order: 'ASC'
});
console.log(`Collected ${jobs.length} jobs total.`);
```

**What happens if `offset` exceeds the total number of jobs?**

You receive a valid response with an empty `results` array. The `next_url` is `null` and `prev_url` points back to a prior page. This isn't an error. Your pagination loop should stop when `results` is empty or `next_url` is `null`.

```
{
  "total": 923,
  "results": [],
  "prev_url": "/scheduler/jobs?page_size=10&offset=99989",
  "next_url": null
}
```

**What values of `page_size` are valid?**

The `page_size` must be a positive integer between 1 and 100. Invalid values return a 400 Bad Request error.

**Can I use pagination with `jobType` or other filters?**

Yes. The `page_size` and `offset` parameters work alongside `jobType`, `sort_by`, and `sort_order`. For example:

```
GET /scheduler/jobs?page_size=50&jobType=HTTP_ENDPOINT&sort_by=name&sort_order=ASC
```

Just remember that `next_url` won't include these filters. Use the offset-based approach described in *Does `next_url` preserve my filters and sort order?*.

**Related Information**  


[Guided Answers](https://ga.support.sap.com/dtp/viewer/#/tree/2797/actions/40871)

