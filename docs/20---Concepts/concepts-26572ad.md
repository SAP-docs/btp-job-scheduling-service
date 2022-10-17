<!-- loio26572ad024c54643a2424524f60669a2 -->

# Concepts

 SAP Job Scheduling service offers you flexible scheduling capabilities for action endpoints in your application or long-running processes using Cloud Foundry tasks.



 **Job**
 :   A collection of schedules with an action endpoint

    A job is configured with a URL, which means that your job invokes this URL, for example, every night. A job can also be configured with a Cloud Foundry task.

 :   Synchronous requests are used if the service calls the action endpoint of the application and the application logic is executed in a short span of time. Jobs can be executed in an asynchronous \(or batch\) mode for job runs with a large span of time.

 :   A service plan within SAP Job Scheduling service considers the number of schedules within a job.

  **Action Endpoint**
 :   An HTTP or REST endpoint which is exposed by the application that is bound to the SAP Job Scheduling service and invoked by the service to perform the defined action.

  **Cloud Foundry Task**
 :   An app or script whose code is included as part of a deployed app, but runs independently in its own container and is designed to use minimal resources.

  **Schedule**
 :   A one-time or a recurring entity within a job without an action endpoint.

 :   <a name="loio26572ad024c54643a2424524f60669a2__table_ids_12t_d4b"/>


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

A schedule passes through three lifecycle states for each run.



</td>
</tr>
</table>

  **Multitenancy**
 :   You can use the service with multitenant applications developed in the context of a Platform-as-a-Service \(PAAS\) tenant or as a Software-as-a-Service \(SaaS\) tenant.

 **Related Information**  


[Asynchronous Mode](asynchronous-mode-d9fd81c.md "The SAP Job Scheduling service executes jobs that support action endpoints in a synchronous mode or in an asynchronous (or batch) mode.")

[Schedule Types](schedule-types-9cf8c14.md#loio9cf8c14da0144c84aac628dc56b00ffd "SAP Job Scheduling service runs one-time and recurring jobs or Cloud Foundry tasks.")

[Schedule Formats](schedule-formats-54615f0.md#loio54615f087cca45c48f81ce4967c6f7f3 "The SAP Job Scheduling service supports several scheduling formats.")

[Schedule Lifecycle](schedule-lifecycle-e1805f2.md "A schedule passes through three lifecycle states for each run.")

[Multitenancy in SAP Job Scheduling Service](multitenancy-in-sap-job-scheduling-service-464b613.md "The SAP Job Scheduling service allows invocation of job actions in the context of Platform-as-a-Service (PAAS) or Software-as-a-Service (SaaS) tenants.")

[About Cloud Foundry Tasks](https://docs.cloudfoundry.org/devguide/using-tasks.html)

