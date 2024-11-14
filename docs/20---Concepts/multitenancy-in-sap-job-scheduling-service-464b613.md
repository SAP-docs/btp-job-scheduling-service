<!-- loio464b6130857c4bc98af21a0b528cd35a -->

# Multitenancy in SAP Job Scheduling Service

The SAP Job Scheduling service allows invocation of job actions in the context of Platform-as-a-Service \(PaaS\) or Software-as-a-Service \(SaaS\) tenants.

This means that a deployed multitenant application can create/view/edit/delete jobs in the context of tenants, which have subscribed to it. To support a multitenancy scenario, a multitenancy provider application must be deployed and bound to instances of both the SAP SaaS Provisioning service and the SAP Job Scheduling service and define the SAP Job Scheduling service as a dependency.



<a name="loio464b6130857c4bc98af21a0b528cd35a__section_l51_r1r_c5b"/>

## Additional resources how to create a multitenancy scenario:



### General understanding and concepts of Multitenancy:

-   [SAP Help: Developing Multitenant Applications in the Cloud Foundry Environment](https://help.sap.com/docs/BTP/65de2977205c403bbc107264b8eccf4b/5e8a2b74e4f2442b8257c850ed912f48.html)

-   [Using SaaS Provisioning Service to develop Multitenant application on SAP Business Technology Platform, Cloud Foundry Environment](https://blogs.sap.com/2018/10/25/using-saas-registry-to-develop-multitenant-application-on-sap-cloud-platform-cloud-foundry-environment)




### SAP Job Scheduling service-specific:

-   [Job Scheduler in SAP Business Technology Platform: Overview](https://blogs.sap.com/2021/06/30/job-scheduler-in-sap-business-technology-platform-overview-of-blog-posts/)

-   [Using Job Scheduler in SAP Business Technology Platform: Multitenancy](https://blogs.sap.com/2021/07/29/using-job-scheduler-in-sap-btp-7-multitenancy-0-intro/)




<a name="loio464b6130857c4bc98af21a0b528cd35a__section_xl1_yvv_y2b"/>

## Subscriptions and Service Behavior

If a SaaS tenant unsubscribes from the provided service which consumes the SAP Job Scheduling service, all corresponding jobs and schedules are deleted.

The SAP Job Scheduling service provides an administration dashboard that you can access with space developer permissions. The administration dashboard shows the jobs of all subscribed SaaS tenants as well jobs created with the tenant of the multitenancy application. A tenant-specific dashboard can be implemented by the multitenancy application using the REST API of the SAP Job Scheduling service.



<a name="loio464b6130857c4bc98af21a0b528cd35a__section_znr_fxv_y2b"/>

## Rules

-   Jobs and schedules created by the multitenant application for a SaaS tenant aren't accessible by other SaaS tenants.

-   Credentials bound to a SaaS tenant could be used to access SaaS tenant bound data only.

-   Credentials bound to the PaaS tenant are bound to the SAP Job Scheduling service instance. This means that the multitenancy provider application is allowed to create/read/edit/delete all jobs and schedules for the bound SAP Job Scheduling service instance without any restrictions of SaaS tenants.


**Related Information**  


[SAP Job Scheduling Service REST APIs](../40---Using-JOB-SCHDULR-TITLE/sap-job-scheduling-service-rest-apis-c513d2d.md "Use SAP Job Scheduling service REST APIs to create, manage, and monitor jobs and job schedules.")

