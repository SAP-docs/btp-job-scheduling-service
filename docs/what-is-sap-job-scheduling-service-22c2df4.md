<!-- loio22c2df4d22cb4a05af4c9502a67597ae -->

# What Is SAP Job Scheduling Service?

Define and manage one-time and recurring jobs or Cloud Foundry tasks.

SAP Job Scheduling service allows you to define and manage jobs that run once or on a recurring schedule. Use this runtime-agnostic service to schedule action endpoints in your application or long-running processes using Cloud Foundry tasks. Use REST APIs to schedule jobs, including long-running jobs asynchronously, and create multiple schedule formats for simple and complex recurring schedules. Manage jobs and tasks and manage schedules with a web-based user interface.

By using the SAP Job Scheduling service in the cloud, you benefit from its multitenancy capabilities, its uniform REST API, and you don’t have to switch feature sets.

If you are running your applications on multiple cloud hyperscalers, you don't have to make any changes to the applications when using the SAP Job Scheduling service. Customers who are implementing multitenancy applications can create and process tenant-specific jobs and schedules.

For more information, see also SAP Job Scheduling service on [SAP Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/job-scheduling-service?service_plan=standard&region=all&commercialModel=cloud).

> ### Tip:  
> The English version of this guide is open for contributions and feedback using GitHub. This allows you to get in contact with responsible authors of SAP Help Portal pages and the development team to discuss documentation-related issues. To contribute to this guide, or to provide feedback, choose the corresponding option on SAP Help Portal:
> 
> -   *Feedback* \> *Create issue*: Provide feedback about a documentation page. This option opens an issue on GitHub.
> 
> -   *Feedback* \> *Edit page*: Contribute to a documentation page. This option opens a pull request on GitHub.
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


<dl>
<dt><b>

Use flexible schedule formats 

</b></dt>
<dd>

Flexibly choose between cron and human-readable date formats for your schedules.



</dd><dt><b>

Get secure access 

</b></dt>
<dd>

Run jobs on behalf of an application secured by an OAuth 2.0 protected communication used when the service calls the action endpoint, and when the application invokes the services' REST APIs.



</dd><dt><b>

Schedule synchronously or asynchronously 

</b></dt>
<dd>

Define and manage jobs synchronously or asynchronously as well as run long-running CF tasks asynchronously.



</dd><dt><b>

Optimize your resources usage 

</b></dt>
<dd>

Run Cloud Foundry tasks asynchronously and thereby optimize your resources usage.



</dd><dt><b>

App and scheduling logic seperated 

</b></dt>
<dd>

USE REST APIs to perform CRUD operations on jobs and schedules and to retrieve run logs of executed schedules.



</dd><dt><b>

Dashboard for managing jobs and tasks 

</b></dt>
<dd>

Use the web-based user interface to create, edit, or delete jobs and tasks for a service instance. Create, manage, and monitor schedules for your jobs and tasks. Check the logs to see if a schedule was executed successfully.



</dd><dt><b>

Supports Node-js client libraries 

</b></dt>
<dd>

Convenient client library to execute CRUD operations, including create job, from your Node.js application.



</dd><dt><b>

Benefit from multitenancy support 

</b></dt>
<dd>

Use this service in tenant-aware \(multitenant\) applications. Run them on a shared compute unit that can be used by multiple consumers \(tenants\).



</dd>
</dl>



<a name="loio22c2df4d22cb4a05af4c9502a67597ae__section_n3j_hhf_ynb"/>

## Environment

The service can be consumed in the following runtimes:

-   Cloud Foundry runtime

-   Kyma runtime

    > ### Note:  
    > The SAP Job Scheduling service can be cross-consumed from Kyma applications on Microsoft Azure, Google Cloud Platform, and Amazon Web Services \(excluding Government Cloud \(US\) regions\).




## Multitenancy Support

This service supports multitenancy. It can be used in tenant-aware applications.



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
<tr>
<td valign="top">

Sending notifications

</td>
<td valign="top">

 

</td>
<td valign="top">

Sending notifications using the SAP Alert Notification service for SAP BTP if a job or a task is successful or fails is only available in the Cloud Foundry environment.

</td>
<td valign="top">

[Manage Jobs with Service Dashboard](40---Using-JOB-SCHDULR-TITLE/manage-jobs-with-service-dashboard-132fd06.md)

[Create Job](40---Using-JOB-SCHDULR-TITLE/create-job-2c1ecb6.md)

</td>
</tr>
</table>

**Related Information**  


[Initial Setup](initial-setup-0adb655.md "You can get started with the SAP Job Scheduling service by following the steps below.")

[Getting Started](getting-started-02e4e8b.md "Once you've created a service instance for the SAP Job Scheduling service and bound it to your application, you can use the service.")

 <?sap-ot O2O class="- topic/link " href="8d30095891db417f9b9351570b1679b2.xml" text="" desc="" xtrc="link:3" xtrf="file:/home/builder/src/dita-all/jjq1673438782153/loio4b3e16d4e4d14242bdc2ab48d2aec6be_en-US/src/content/localization/en-us/22c2df4d22cb4a05af4c9502a67597ae.xml" output-class="" current-file="file:/home/builder/tp.net.sf.dita-ot/2.3/plugins/com.elovirta.dita.markdown_1.3.0/xsl/dita2markdownImpl.xsl" ?> 

[Accessibility Features in SAP Job Scheduling Service](accessibility-features-in-sap-job-scheduling-service-12aa90f.md "To optimize your experience of SAP Job Scheduling service, SAP Business Technology Platform (SAP BTP) provides features and settings that help you use the software efficiently.")

[Guided Answers](https://ga.support.sap.com/dtp/viewer/#/tree/2797/actions/40871)

[SAP Job Scheduling Service REST APIs](40---Using-JOB-SCHDULR-TITLE/sap-job-scheduling-service-rest-apis-c513d2d.md "Use SAP Job Scheduling service REST APIs to create, manage, and monitor jobs and job schedules.")

[Cloud Foundry Tasks](https://docs.cloudfoundry.org/devguide/using-tasks.html#run-tasks)

[Secure Access](50---Security/secure-access-745ca50.md "The SAP Job Scheduling service provides options to secure job actions with action endpoints as well as to secure Cloud Foundry tasks.")

[Schedule Formats](20---Concepts/schedule-formats-54615f0.md#loio54615f087cca45c48f81ce4967c6f7f3 "The SAP Job Scheduling service supports several scheduling formats.")

[Asynchronous Mode](20---Concepts/asynchronous-mode-d9fd81c.md "The SAP Job Scheduling service executes jobs that support action endpoints in a synchronous mode or in an asynchronous (or batch) mode.")

