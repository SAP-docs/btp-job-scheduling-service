<!-- loio22c2df4d22cb4a05af4c9502a67597ae -->

<link rel="stylesheet" type="text/css" href="css/sap-icons.css"/>

# What Is SAP Job Scheduling Service?

Define and manage one-time and recurring jobs or Cloud Foundry tasks.

SAP Job Scheduling service allows you to define and manage jobs that run once or on a recurring schedule. Use this runtime-agnostic service to schedule action endpoints in your application or long-running processes using Cloud Foundry tasks. Use REST APIs to schedule jobs, including long-running jobs asynchronously, and create multiple schedule formats for simple and complex recurring schedules. Manage jobs and tasks and manage schedules with a web-based user interface.

By using the SAP Job Scheduling service in the cloud, you benefit from its multitenancy capabilities, its uniform REST API, and you don’t have to switch feature sets.

If you are running your applications on multiple cloud hyperscalers, you don't have to make any changes to the applications when using the SAP Job Scheduling service. Customers who are implementing multitenancy applications can create and process tenant-specific jobs and schedules.

For more information, see also SAP Job Scheduling service on [SAP Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/job-scheduling-service?service_plan=standard&region=all&commercialModel=cloud).

> ### Tip:  
> The English version of this guide is open for contributions and feedback using GitHub. This allows you to get in contact with responsible authors of SAP Help Portal pages and the development team to discuss documentation-related issues. To contribute to this guide, or to provide feedback, choose the corresponding option on SAP Help Portal:
> 
> -   :pencil2:: Contribute to a documentation page. This option opens a pull request on GitHub.
> 
> -   <span class="SAP-icons"></span> Feedback: Provide feedback about a documentation page. This option opens an issue on GitHub.
> 
> 
> You need a GitHub account to use these options.
> 
> More information:
> 
> -   [Contribution Guidelines](https://help.sap.com/docs/open-documentation-initiative/contribution-guidelines/readme.html)
> 
> -   [Introduction Video](https://www.youtube.com/watch?v=WJ0oarMlVW4)
> 
> -   [Introduction Blog Post](https://blogs.sap.com/2021/11/29/sap-btp-documentation-goes-github-new-collaboration-process/)



<a name="loio22c2df4d22cb4a05af4c9502a67597ae__section_o3j_hhf_ynb"/>

## Features

  Use flexible schedule formats 
 :   Flexibly choose between cron and human-readable date formats for your schedules.

   Get secure access 
 :   Run jobs on behalf of an application secured by an OAuth 2.0 protected communication used when the service calls the action endpoint, and when the application invokes the services' REST APIs.

   Schedule synchronously or asynchronously 
 :   Define and manage jobs synchronously or asynchronously as well as run long-running CF tasks asynchronously.

   Optimize your resources usage 
 :   Run Cloud Foundry tasks asynchronously and thereby optimize your resources usage.

   App and scheduling logic seperated 
 :   USE REST APIs to perform CRUD operations on jobs and schedules and to retrieve run logs of executed schedules.

   Dashboard for managing jobs and tasks 
 :   Use the web-based user interface to create, edit, or delete jobs and tasks for a service instance. Create, manage, and monitor schedules for your jobs and tasks. Check the logs to see if a schedule was executed successfully.

   Supports Node-js client libraries 
 :   Convenient client library to execute CRUD operations, including create job, from your Node.js application.

 

<a name="loio22c2df4d22cb4a05af4c9502a67597ae__section_n3j_hhf_ynb"/>

## Environment

This service runs in the Cloud Foundry environment.



<a name="loio22c2df4d22cb4a05af4c9502a67597ae__section_cdq_wm5_prb"/>

## Technical Constraints

These are the general technical ranges of this service:


<table>
<tr>
<th valign="top">

Feature



</th>
<th valign="top">

Quantity



</th>
<th valign="top">

Details



</th>
<th valign="top">

Additional Information



</th>
</tr>
<tr>
<td valign="top">

Minimal schedule interval



</td>
<td valign="top">

5 minutes



</td>
<td valign="top">

You cannot create intervals between schedules of less than 5 minutes, for example, the interval for repeating the job execution cannot be 2 minutes.



</td>
<td valign="top">

[Schedule Types](20---Concepts/schedule-types-9cf8c14.md#loio9cf8c14da0144c84aac628dc56b00ffd)



</td>
</tr>
<tr>
<td valign="top">

Synchronous requests timeout



</td>
<td valign="top">

15 seconds



</td>
<td valign="top">

The SAP Job Scheduling service awaits response for the synchronous job from the action endpoint for the specified duration. If the application doesn't provide a response in the specified duration, there is a timeout and the application should use asynchronous requests.



</td>
<td valign="top">

[Asynchronous Mode](20---Concepts/asynchronous-mode-d9fd81c.md)



</td>
</tr>
<tr>
<td valign="top">

Asynchronous requests timeout



</td>
<td valign="top">

30 minutes



</td>
<td valign="top">

The SAP Job Scheduling service awaits response for the asynchronous job from the action endpoint for the specified duration. If the application doesn't provide a response in the specified duration, there is a timeout. You can change this setting in the configuration.



</td>
<td valign="top">

[Asynchronous Mode](20---Concepts/asynchronous-mode-d9fd81c.md)

[Manage Jobs with Service Dashboard](40---Using-JOB-SCHDULR-TITLE/manage-jobs-with-service-dashboard-132fd06.md)



</td>
</tr>
</table>

**Related Information**  


[Initial Setup](initial-setup-0adb655.md "You can get started with the SAP Job Scheduling service using the standard procedures for the Cloud Foundry environment.")

[Getting Started](30---Getting-Started/getting-started-02e4e8b.md "Once you've completed the initial setup for SAP Job Scheduling service, to use the service you create a service instance and bind it to your application.")

[Accessibility Features in SAP Job Scheduling Service](accessibility-features-in-sap-job-scheduling-service-12aa90f.md "To optimize your experience of SAP Job Scheduling service, SAP Business Technology Platform (SAP BTP) provides features and settings that help you use the software efficiently.")

[Guided Answers](https://ga.support.sap.com/dtp/viewer/#/tree/2797/actions/40871)

[SAP Job Scheduling Service REST APIs](40---Using-JOB-SCHDULR-TITLE/sap-job-scheduling-service-rest-apis-c513d2d.md "Use SAP Job Scheduling service REST APIs to create, manage, and monitor jobs and job schedules.")

[Cloud Foundry Tasks](https://docs.cloudfoundry.org/devguide/using-tasks.html#run-tasks)

[Secure Access](50---Security/secure-access-745ca50.md "The SAP Job Scheduling service provides options to secure job actions with action endpoints as well as to secure Cloud Foundry tasks.")

[Schedule Formats](20---Concepts/schedule-formats-54615f0.md#loio54615f087cca45c48f81ce4967c6f7f3 "The SAP Job Scheduling service supports several scheduling formats.")

[Asynchronous Mode](20---Concepts/asynchronous-mode-d9fd81c.md "The SAP Job Scheduling service executes jobs that support action endpoints in a synchronous mode or in an asynchronous (or batch) mode.")

