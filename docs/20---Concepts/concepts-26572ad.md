<!-- loio26572ad024c54643a2424524f60669a2 -->

# Concepts

SAP Job Scheduling service offers you flexible scheduling capabilities for action endpoints in your application or long-running processes using Cloud Foundry tasks.



## Key Terms



### Job

A collection of schedules associated with an action to be performed.

Each job defines an action and the schedules that determine when it runs - for example, every night. SAP Job Scheduling service supports three types of jobs, distinguished by the action they perform:

-   **HTTP job**: Invokes an action endpoint \(an HTTP or REST endpoint\) exposed by an application bound to the service.

-   **Destination job**: Calls an external application that is not part of your Cloud Foundry space or Kyma namespace. The call is made through a destination configured in the SAP Destination service.

-   **CF task job**: Runs a Cloud Foundry task, which consists of code deployed as part of an application that runs independently in its own container.


Jobs can run in two modes:

-   **Synchronous**: The service calls the action endpoint and the application logic completes withing a short time span.

-   **Asynchronous** \(batch\): Used for job runs that take a longer time to complete.


> ### Note:  
> The number of schedules depends on the SAP Job Scheduling service plan.



### Action Endpoint

An HTTP or REST endpoint exposed by an application that is bound to the SAP Job Scheduling service. The service invokes this endpoint to perform the job's defined action.



### Cloud Foundry Task

An application or script whose code is included as part of a deployed application, but runs independently in its own container and is designed to use minimal resources.



### Schedule

A one-time or a recurring entity within a job without an action endpoint.


<table>
<tr>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Schedule types

</td>
<td valign="top">

Runs one-time and recurring jobs or Cloud Foundry tasks.

</td>
</tr>
<tr>
<td valign="top">

Schedule formats

</td>
<td valign="top">

Supports several flexible schedule formats.

</td>
</tr>
<tr>
<td valign="top">

Schedule lifecycle

</td>
<td valign="top">

A schedule passes through three lifecycle statuses for each run.

</td>
</tr>
</table>



### Multitenancy

You can use the service with multitenant applications developed in the context of a Platform-as-a-Service \(PAAS\) tenant or as a Software-as-a-Service \(SaaS\) tenant.



### Security

You have to bind the Job Scheduling service instance to the application in the same Cloud Foundry space. When the service calls an endpoint, the request always contains the Authorization header \(JWT token\). To validate this token, make sure that your application is bound to the Job Scheduling service instance.

For more information, see [Binding Service Instances to Applications](https://help.sap.com/docs/btp/sap-business-technology-platform/binding-service-instances-to-applications?version=Cloud).

**Related Information**  


[Asynchronous Mode](asynchronous-mode-d9fd81c.md "The SAP Job Scheduling service executes jobs that support action endpoints in a synchronous mode or in an asynchronous (or batch) mode.")

[Schedule Types](schedule-types-9cf8c14.md#loio9cf8c14da0144c84aac628dc56b00ffd "SAP Job Scheduling service runs one-time and recurring jobs or Cloud Foundry tasks.")

[Schedule Formats](schedule-formats-54615f0.md#loio54615f087cca45c48f81ce4967c6f7f3 "The SAP Job Scheduling service supports several scheduling formats.")

[Schedule Lifecycle](schedule-lifecycle-e1805f2.md "A schedule passes through three lifecycle statuses for each run.")

[Multitenancy in SAP Job Scheduling Service](multitenancy-in-sap-job-scheduling-service-464b613.md "The SAP Job Scheduling service allows invocation of job actions in the context of Platform-as-a-Service (PaaS) or Software-as-a-Service (SaaS) tenants.")

[About Cloud Foundry Tasks](https://docs.cloudfoundry.org/devguide/using-tasks.html)

