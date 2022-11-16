<!-- loio78f6a4b2a1f9481f9c83bee47c2ae50c -->

# 2021 What's New for SAP Job Scheduling Service \(Archive\)


 


**2021**


<table>
<tr>
<th valign="top">

Technical Component



</th>
<th valign="top">

Capability



</th>
<th valign="top">

Environment



</th>
<th valign="top">

Title



</th>
<th valign="top">

Description



</th>
<th valign="top">

Action



</th>
<th valign="top">

Type



</th>
<th valign="top">

Available as of



</th>
</tr>
<tr>
<td valign="top">

Job Scheduling Service



</td>
<td valign="top">

Extension Suite - Development Efficiency



</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

REST API - Rate Limits



</td>
<td valign="top">

When you use the REST API, rate limits are now in place. Requests may be denied. After less than one minute, you can execute the request again. A retry header is provided.

In the upcoming releases, the rate limits will be enforced.



</td>
<td valign="top">



</td>
<td valign="top">

Announcement



</td>
<td valign="top">

2021-12-16



</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service



</td>
<td valign="top">

Extension Suite - Development Efficiency



</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Behavior for missed runs during an outage



</td>
<td valign="top">

If the schedule executions are delayed by more than 20 minutes, the SAP Job Scheduling service skips all missed executions except the last one which is then executed immediately.

For more information, see [Skipped Schedule Executions](https://help.sap.com/viewer/07b57c2f4b944bcd8470d024723a1631/Cloud/en-US/d09664b7ae9d453e8b8a3a6e09449916.html).



</td>
<td valign="top">



</td>
<td valign="top">

Changed



</td>
<td valign="top">

2021-12-16



</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service



</td>
<td valign="top">

Extension Suite - Development Efficiency



</td>
<td valign="top">

 Cloud Foundry 



</td>
<td valign="top">

Support for custom identity providers with platform users



</td>
<td valign="top">

The SAP Job Scheduling service supports the use of custom identity providers with platform users.

For more information, see [Manage Jobs with Service Dashboard](../40---Using-JOB-SCHDULR-TITLE/manage-jobs-with-service-dashboard-132fd06.md) and [Supported Tools and Services When Using Custom Identity Providers for Platform Users\[Feature Set A\]](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/94ef5154e384408796c035a82b043f82.html).



</td>
<td valign="top">



</td>
<td valign="top">

New



</td>
<td valign="top">

2021-05-20



</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service



</td>
<td valign="top">

Extension Suite - Development Efficiency



</td>
<td valign="top">

 Cloud Foundry 



</td>
<td valign="top">

CF tasks are stopped according to default asynchronous execution timeout



</td>
<td valign="top">

By default, jobs executed in an asynchronous mode are stopped if the application doesn't provide a response within 30 minutes. This now applies also for CF tasks, that means a task running longer than 30 minutes is stopped.

You can change this setting for the selected service instance on the *Configurations* page in the service dashboard.

For more information, see [Manage Jobs with Service Dashboard](../40---Using-JOB-SCHDULR-TITLE/manage-jobs-with-service-dashboard-132fd06.md).



</td>
<td valign="top">



</td>
<td valign="top">

New



</td>
<td valign="top">

2021-02-25



</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service



</td>
<td valign="top">

Extension Suite - Development Efficiency



</td>
<td valign="top">

 Cloud Foundry 



</td>
<td valign="top">

Binding level secrets



</td>
<td valign="top">

New clientsecrets are created after you bind an application to the SAP Job Scheduling service.

You can use this to rotate clientsecrets by unbinding and then binding the SAP Job Scheduling service instance again to the application.

For more information, see *Binding Level Secrets* in [SAP Job Scheduling Service REST APIs](../40---Using-JOB-SCHDULR-TITLE/sap-job-scheduling-service-rest-apis-c513d2d.md).



</td>
<td valign="top">



</td>
<td valign="top">

New



</td>
<td valign="top">

2020-12-17



</td>
</tr>
</table>

