<!-- loiod72c276ec60c4bbe89c0b9328a926500 -->

# Frequently Asked Questions

Find troubleshooting information in this section. We strongly recommend you use our **Guided Answers** for step-by-step solutions to some issues that may occur in your work with the SAP Job Scheduling service.

For more information, see [Guided Answers](https://ga.support.sap.com/dtp/viewer/#/tree/2797/actions/40871).



<a name="loiod72c276ec60c4bbe89c0b9328a926500__section_dwx_hhd_x1b"/>

## General Questions

**What is the component to raise a ticket for issues related to the SAP Job Scheduling service?**

The support component for the SAP Job Scheduling service is **BC-XS-SRV-JBS**.

**What are the prerequisites to use the SAP Job Scheduling service?**

-   You need access to the SAP Job Scheduling service. Check the Cloud Foundry marketplace to see if the service is available.

-   For jobs with action endpoints, check if you have access and if you can create a service instance of the User Access and Authorization service \(xsuaa\). This service is available in the service marketplace.


**What is the service level agreement \(SLA\) of a scheduled job?**

A scheduled job has a service level agreement of about 20 minutes from the scheduled time.

**As a subscription customer, what does the number of units selected on SAP Store indicate?**

Currently, the number of units selected on SAP Store indicates the number of SAP Job Scheduling service instances that can be created.

> ### Example:  
> If you opt for a value of 5, it indicates that you can create 5 instances of the SAP Job Scheduling service. For each instance, you can create 10,000 job executions.



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
https://login.<landscape.url.com>/profile
```

For eu10, for example, the login route looks as follows:

> ### Sample Code:  
> ```
> https://login.cf.eu10.sap.hana.ondemand.com/profile
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

## Schedules and their Executions

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

To register a job on behalf of a tenant \(subaccount\), fetch an access token from the User Access and Authorization \(xsuaa\) service as follows:

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

A SAP Job Scheduling service instance bound to your multitenant application receives the credentials required to register and manage jobs. To register jobs on behalf of the tenant \(subaccount\) subscribed to your multitenant application, fetch an access token from the xsuaa service using the steps below:

Use the libraries provided by the xsuaa service.

Exchange the access token received from your logged user for a SAP Job Scheduling service token using the method **requestToken** and type as USER\_TOKEN.

Refer library documentation for more specific details on how to obtain an access token using the user\_token grant type. Using the access token received, invoke SAP Job Scheduling service REST API to create Job. The access token has to be used in header as authorization: bearer

The jobs thus created will provide the SaaS tenant \(subaccount\) details in the access token while invoking the configured job action.

**How can I register a Job on behalf of a Tenant when a user is not logged on to my multitenant application?**

If you want to create/delete/update/fetch a job on behalf of a SaaS tenant who has not logged on to your multitenant application, you can use client credentials flow with SaaS user subdomain. The xsuaa API to request a token with client credentials flow is mentioned at the following link: [https://docs.cloudfoundry.org/api/uaa/version/4.23.0/index.html\#client-credentials-grant](https://docs.cloudfoundry.org/api/uaa/version/4.23.0/index.html#client-credentials-grant)

Note that you must use **jwt** as **token\_format** \(instead of **opaque**\). You will receive a URL concatenated by **oauth/token** as described in the topic available at the link mentioned above. Further, remember that you need to replace the URL subdomain with the corresponding SaaS subdomain for which the token is requested. Using the access token that you receive, call the SAP Job Scheduling service REST API to Create Job. The access token has to be used in the header as **Authorization: Bearer**. Such created jobs will provide the SaaS tenant \(or subaccount\) details in the access token while calling the job action that you configured.

**How can I fetch all Jobs or a specific Job \(using id or name\) registered in my SAP Job Scheduling service instance?**

You can fetch all jobs registered in your service instance as client, client secret, and URL from the UAA section of the SAP Job Scheduling service instance bound with your application.

Use POST / oauth/token, body format: x-www-form-urlencoded, parameters: client\_id \(fetched from previous step\), client\_secret \(fetched from previous step\), grant\_type is client\_credentials, response\_type as token.

Using the access token received, invoke SAP Job Scheduling service REST API to fetch all jobs using job ID or name. The access token has to be used in the header as authorization:bearer.

**Can I filter on tenant while fetching Jobs registered for a Tenant?**

Yes you can filter on tenant while fetching jobs registered for a tenant. If you have obtained an access token with grant type as client\_credentials using the credentials from SAP Job Scheduling service instance binding, you can invoke the REST API to fetch all the jobs with tenantID as query parameter.

Example: GET https:///scheduler/jobs?tenantId=<tenantID\>

This will retrieve all jobs registered on behalf of the tenant with tenant ID details. However, this query parameter based filter is not applicable if the token used belongs to a SaaS tenant and the API will return Status Code 400. This filtering is required to restrict access of a SaaS tenant to jobs created for another SaaS tenant.

**Where do I find the tenant information when SAP Job Scheduling service invokes the action endpoint of the multitenant application?**

The tenant information is provided in the access token sent by the SAP Job Scheduling service in the request headers while invoking the action endpoint. You may use the convenient client libraries provided by xsuaa to parse the information out of the access token. You will receive information like tenant id, subdomain, grant type and so on.

**Which jobs does the Service Dashboard show when I launch it for a service instance from SAP BTP cockpit?**

The service dashboard shows the jobs created in your service instance along with its tenant ID. It will also list the tenant information in the overview page for all the jobs. You may also sort the jobs based on tenant ID by clicking on the table header.

**Can I create tenant-specific jobs from Service Dashboard?**

No. Creating a job from service dashboard will always create a job specific to the PaaS tenant. If you are trying to create a job specific for a SaaS tenant who has subscribed to your multitenant application, you need to exchange the Jason Web Token with XSUAA and fetch a token specific for SAP Job Scheduling service \(using client\_id and client\_secret provided to your application by SAP Job Scheduling service instance binding\).

**Software as a Service Tenant**

**How can I fetch Jobs registered for a SaaS Tenant?**

You can fetch all jobs registered for a SaaS tenant using the libraries provided by XSUAA service, exchange the access token received from the logged user for the SAP Job Scheduling service token using the method requestToken and type as USER\_TOKEN.

Refer the API Client library documentation for more specific details on how to obtain an access token using user\_token grant type. Using the access token received, invoke the SAP Job Scheduling service REST API to fetch all jobs. The access token has to be used in header as authorization: bearer.

**Related Information**  


[Guided Answers](https://ga.support.sap.com/dtp/viewer/#/tree/2797/actions/40871)

