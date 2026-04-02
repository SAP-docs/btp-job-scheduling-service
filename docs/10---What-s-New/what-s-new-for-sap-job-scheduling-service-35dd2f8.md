<!-- loio35dd2f8d1060419f896169b928dc590f -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# What's New for SAP Job Scheduling Service 





**2024 - 26**


<table>
<tr>
<th valign="top">

Technical Component

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

Lifecycle

</th>
<th valign="top">

Type

</th>
<th valign="top">

Line of Business

</th>
<th valign="top">

Modular Business Process

</th>
<th valign="top">

Product

</th>
<th valign="top">

Latest Revision

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

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Deprecation of Node.js Library

</td>
<td valign="top">

The Node.js client library is deprecated. The library is planned to receive security updates for one year after deprecation.

See [Node.js Client Library \(Deprecated\)](../40---Using-JOB-SCHDULR-TITLE/node-js-client-library-deprecated-9b86127.md).

Action: Use the REST API published on SAP Business Accelerator Hub instead. You can use it to generate a client library for your preferred programming language that contains all up-to-date APIs and features. See [https://api.sap.com/api/sap-btpjss-admin-v1/overview](https://api.sap.com/api/sap-btpjss-admin-v1/overview).

</td>
<td valign="top">

Recommended

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

Announcement

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2026-03-30

</td>
<td valign="top">

2026-04-02

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Identity Authentication Support

</td>
<td valign="top">

As an alternative to SAP Authorization and Trust Management service \(XSUAA\) authentication, the SAP Job Scheduling service now supports SAP Cloud Identity Services - Identity Authentication.

Key features:

-   OAuth 2.0 authentication via Identity Authentication service

-   Integration with `consumed-services` of the SAP Cloud Identity Services - Identity Authentication service instance configuration

-   Support for multitenancy with the Subscription Management service


See [Secure Access](../50---Security/secure-access-745ca50.md) and [Authentication](../40---Using-JOB-SCHDULR-TITLE/authentication-5dca60b.md).

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2026-03-30

</td>
<td valign="top">

2026-04-02

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Mark Jobs, Tasks, Schedules as Favorites \(Experimental\)

</td>
<td valign="top">

The SAP Job Scheduling service dashboard now includes an experimental feature that lets you mark frequently visited jobs, tasks, and schedules as favorites.

On the overview page of each job, task, and schedule, choose the <span class="SAP-icons-V5"></span> \(Add to Favorites\) button to add the resource to your favorites. To view all favorites, go to the *Service Instance Overview* page in the dashboard.

The *Favorite Jobs*, *Favorite Tasks*, and *Favorite Schedules* cards display the top five most visited favorites. If there are fewer than five favorites, the cards also show the most visited resources that aren't yet added as favorites. You can visit each favorite directly from the cards.

> ### Note:  
> Experimental features aren't part of the officially delivered scope that SAP guarantees for future releases. For more information, see [Important Disclaimers and Legal Information](https://help.sap.com/viewer/disclaimer).

The favorites are currently stored locally in the browser.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

Beta

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2026-03-16

</td>
<td valign="top">

2026-03-19

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

REST API Available on SAP Business Accelerator Hub 

</td>
<td valign="top">

The REST API of the SAP Job Scheduling service is now available on the SAP Business Accelerator Hub: [https://api.sap.com/api/sap-btpjss-admin-v1/overview](https://api.sap.com/api/sap-btpjss-admin-v1/overview). You can use this resource to explore the API, interact with its endpoints, and generate client libraries for your desired programming language.

Action: Refer to and bookmark the API documentation of this service on the SAP Business Accelerator Hub as the API documentation on the SAP Help Portal is planned to be removed in the coming months.

</td>
<td valign="top">

Recommended

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Changed

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2026-03-02

</td>
<td valign="top">

2026-03-05

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

New Page Size Limits for the `GET /scheduler/jobs` API

</td>
<td valign="top">

Starting 25 June, a new default page size of 10 and a maximum page size of 100 are enforced on the `GET /scheduler/jobs` endpoint. This change aims to ensure stability of the service and makes this endpoint consistent with the other API endpoints of the service.

Action: To retrieve all jobs, implement offset pagination. For more information, see [Understanding Offset and Cursor Pagination](../40---Using-JOB-SCHDULR-TITLE/understanding-offset-and-cursor-pagination-96ebd22.md).

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Changed

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2026-03-12

</td>
<td valign="top">

2026-06-25

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Dashboard Statistics \(Experimental\)

</td>
<td valign="top">

We're introducing an experimental feature adding new statistics and recommendations for optimal job configuration across the following pages of the SAP Job Scheduling service dashboard:

-   On the *Service Instance Overview* page, look for the cards *Job Statistics* and *Job Schedule Statistics*.

-   On the overview page of each job, look for the cards *Schedule Statistics* and *Job Best Practices*.

-   On the overview page of each schedule, look for the cards *Execution Success Rate* and *Recent Run Errors*.


In selected regions where the service is available, the *Service Instance Overview* page displays the latest schedules in an error state. You can review these issues with two clicks.

> ### Note:  
> Experimental features aren't part of the officially delivered scope that SAP guarantees for future releases. For more information, see [Important Disclaimers and Legal Information](https://help.sap.com/viewer/disclaimer).

Use these new insights to better monitor job performance, identify errors, and optimize configurations.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

Beta

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2026-02-16

</td>
<td valign="top">

2026-02-19

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Streamlined Dashboard UI for Faster Navigation

</td>
<td valign="top">

The SAP Job Scheduling service dashboard interface is redesigned to reduce navigation steps. Several pages are now merged into their corresponding parent pages:

-   The *Configurations* page is merged into the *Service Instance Overview* page.

-   The *Jobs* \> *Schedules* page is merged into the overview page of each job.

-   The *Schedules* \> *Run Logs* page is merged into the overview page of each schedule.


This improved layout helps you access key information more efficiently with fewer clicks.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Changed

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2026-02-16

</td>
<td valign="top">

2026-02-19

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Service Plan Free Now Available for Enterprise Accounts

</td>
<td valign="top">

Service plan `free` is now available for enterprise accounts.

The `free` plan provides the same functionality as the `standard` plan but has usage restrictions and doesn't include support. See [SAP Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/job-scheduling-service?tab=service_plan&region=all).

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2026-02-05

</td>
<td valign="top">

2026-02-05

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Service Plan Free Now Available on SAP BTP Trial

</td>
<td valign="top">

Service plan `free` is now available for trial accounts.

As an alternative to service plan `standard`, you can use service plan `free` on SAP BTP Trial to try out the features provided by SAP Job Scheduling service.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2026-01-22

</td>
<td valign="top">

2026-01-22

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Service Plan Lite Deprecated on SAP BTP Trial

</td>
<td valign="top">

Starting 22 January 2026, service plan `lite` is deprecated on SAP BTP Trial.

As of 19 February 2026, you can no longer create new instances using service plan `lite`. Existing instances with plan `lite` will be removed.

Action: We recommend that you use service plan `free` on SAP BTP Trial instead, which offers more capabilities and works like service plan `standard`.

</td>
<td valign="top">

Recommended

</td>
<td valign="top">

Deprecated

</td>
<td valign="top">

Announcement

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2026-01-22

</td>
<td valign="top">

2026-01-22

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Sharing Job Scheduling Service Instances Across Spaces

</td>
<td valign="top">

You can now share a SAP Job Scheduling service instance with applications across multiple spaces within the same subaccount. This approach streamlines data exchange, reduces costs, and simplifies resource management.

See [Share Service Instances](https://help.sap.com/docs/job-scheduling/sap-job-scheduling-service/share-service-instances).

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Changed

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2025-12-08

</td>
<td valign="top">

2025-12-11

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Belize Themes Removed from the Dashboard UI

</td>
<td valign="top">

The Belize themes are removed from the user interface of the Job Scheduling service dashboard.

You can choose from the following themes:

-   Morning Horizon \(Default\)

-   Evening Horizon

-   Horizon High Contrast Black

-   Horizon High Contrast White

    If you've been using one of the Belize themes, the system automatically switches to Horizon.


> ### Note:  
> Belize is deprecated as of SAPUI5 1.120. SAP recommends switching to the current Horizon theme. See [Deprecated Themes and Libraries](https://sapui5.hana.ondemand.com/#/topic/a87ca843bcee469f82a9072927a7dcdb).



</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Changed

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2025-08-18

</td>
<td valign="top">

2025-08-21

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

New Resource Tags for Job Execution and Task Execution Service Events

</td>
<td valign="top">

The following new resource tags and their respective values are added to the list of event properties that can be matched by SAP Alert Notification service for SAP BTP:

-   `runStatus`

-   `runState`

-   `scheduleDescription`


See:

-   [SAP Job Scheduling Service Job Execution](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/jobscheduler-job-execution)

-   [SAP Job Scheduling Service Task Execution](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/jobscheduler-task-execution)




</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Changed

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2025-07-24

</td>
<td valign="top">

2025-07-24

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

New Default UI Theme

</td>
<td valign="top">

*Morning Horizon* replaces *Belize* as the default UI theme of the Job Scheduling service dashboard.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Changed

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2025-06-09

</td>
<td valign="top">

2025-06-12

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

New Horizon Themes in the Job Scheduling Service Dashboard

</td>
<td valign="top">

You can now switch to new Horizon themes in the user interface of the Job Scheduling service dashboard:

-   Morning Horizon

-   Evening Horizon

-   Horizon High Contrast White

-   Horizon High Contrast Black




</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Changed

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2025-05-29

</td>
<td valign="top">

2025-05-29

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Integration with SAP Cloud ALM

</td>
<td valign="top">

You can now integrate SAP Job Scheduling service with SAP Cloud ALM. This integration allows you to track the status of your job processes directly from the interface of SAP Cloud ALM.

See [Integration with SAP Cloud ALM](https://help.sap.com/docs/job-scheduling/sap-job-scheduling-service/integration-with-sap-cloud-alm).

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2025-05-29

</td>
<td valign="top">

2025-05-29

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Deletion of One-Time Schedules Not Run Within Last 30 Days

</td>
<td valign="top">

As of May 29, 2025, one-time schedules will be deleted if they have not been run within the last 30 days.

Action: Instead of using one-time schedules, you can run recurring schedules. See [Recurring Schedules](https://help.sap.com/docs/job-scheduling/sap-job-scheduling-service/schedule-types?version=Cloud#recurring-schedules).

</td>
<td valign="top">

Recommended

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Changed

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2025-05-15

</td>
<td valign="top">

2025-05-29

</td>
</tr>
<tr>
<td valign="top">

Job Scheduling Service

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Updated Procedure for Creating a Service Instance

</td>
<td valign="top">

You no longer need to specify the `enable-xsuaa-support: true` property when creating a service instance using the SAP BTP cockpit or the CF CLI. It is now set by default.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Changed

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2024-11-14

</td>
<td valign="top">

2024-11-14

</td>
</tr>
</table>

