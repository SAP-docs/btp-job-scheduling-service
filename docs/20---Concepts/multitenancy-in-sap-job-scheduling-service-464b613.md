<!-- loio464b6130857c4bc98af21a0b528cd35a -->

# Multitenancy in SAP Job Scheduling Service

The SAP Job Scheduling service allows invocation of job actions in the context of Platform-as-a-Service \(PaaS\) or Software-as-a-Service \(SaaS\) tenants.

This means that a deployed multitenant application can create, view, edit, and delete jobs in the context of tenants, which have subscribed to it.



<a name="loio464b6130857c4bc98af21a0b528cd35a__section_gzb_qrd_r2c"/>

## Prerequisites

To support a multitenancy scenario, you must:

1.  Deploy a multitenant application to a provider subaccount.

2.  Bind the deployed application to an instance of the SAP Job Scheduling service and to one of the following:

    -   For XSUAA authentication \(default\): SAP SaaS Provisioning service
    -   For authentication with Identity Authentication service: Subscription Management service and an SAP Cloud Identity Services - Identity Authentication service instance


3.  Define the SAP Job Scheduling service as a dependency.




<a name="loio464b6130857c4bc98af21a0b528cd35a__section_l51_r1r_c5b"/>

## Additional Resources for Creating a Multitenancy Scenario



### General understanding and concepts of multitenancy:

-   [SAP Help: Developing Multitenant Applications in the Cloud Foundry Environment](https://help.sap.com/docs/BTP/65de2977205c403bbc107264b8eccf4b/5e8a2b74e4f2442b8257c850ed912f48.html)

-   [Using SaaS Provisioning Service to develop Multitenant application on SAP Business Technology Platform, Cloud Foundry Environment](https://blogs.sap.com/2018/10/25/using-saas-registry-to-develop-multitenant-application-on-sap-cloud-platform-cloud-foundry-environment)




### SAP Job Scheduling service-specific resources:

-   [Job Scheduler in SAP Business Technology Platform: Overview](https://blogs.sap.com/2021/06/30/job-scheduler-in-sap-business-technology-platform-overview-of-blog-posts/)

-   [Using Job Scheduler in SAP Business Technology Platform: Multitenancy](https://blogs.sap.com/2021/07/29/using-job-scheduler-in-sap-btp-7-multitenancy-0-intro/)




<a name="loio464b6130857c4bc98af21a0b528cd35a__section_xl1_yvv_y2b"/>

## Subscriptions and Service Behavior

The SAP Job Scheduling service provides an administration dashboard that you can access with space developer permissions. The administration dashboard shows the jobs of all subscribed SaaS tenants as well jobs created with the tenant of the multitenant application. A tenant-specific dashboard can be implemented by the multitenant application using the REST API of the SAP Job Scheduling service.

When a single instance of the SAP Job Scheduling service is used by one multitenant application, and the SaaS tenant unsubscribes from that application, all corresponding jobs and schedules are deleted.

When a single instance of the SAP Job Scheduling service is used by multiple multitenant applications, and one SaaS tenant subscribes to more than one of these multitenant applications:

-   The data is shared among the applications the SaaS tenant has subscribed to.

-   If you delete a subscription to one of these applications, the data in the SAP Job Scheduling service remains intact until all subscriptions are deleted.




## Set Up Authentication Using Identity Authentication Service

When using authentication with Identity Authentication service for a multitenant scenario, the setup differs from authentication with SAP Authorization and Trust Management service \(XSUAA\):

1.  Create an Identity Authentication service instance with `multi-tenant: true` and specify the SAP Job Scheduling service in `consumed-services`.

    Example for Identity Authentication service configuration for a multitenant scenario:

    > ### Sample Code:  
    > ```
    > {
    >     "display-name": "Multi-Tenant Application",
    >     "multi-tenant": true,
    >     "consumed-services": [
    >         {
    >             "service-instance-name": "<jobscheduler-instance-name>"
    >         }
    >     ]
    > }
    > ```

2.  Create a Subscription Management service instance with the Identity Authentication service reference.

    Example for Subsription Management service configuration:

    > ### Sample Code:  
    > ```
    >    {
    >       "iasServiceInstanceName": "<identity-service-instance-name>",
    >       "applicationType": "application",
    >       "displayName": "Multi-Tenant Application",
    >       "appName": "<app-name>",
    >       "appCallbacks": {
    >          "subscriptionCallbacks": {
    >             "url": "https://<app-url>/subscription_manager_callbacks/tenants/{app_tid}"
    >          }
    >       }
    >    }
    > ```

    For information on making API calls on behalf of subscriber tenants, see [Authentication](../40---Using-JOB-SCHDULR-TITLE/authentication-5dca60b.md).




<a name="loio464b6130857c4bc98af21a0b528cd35a__section_znr_fxv_y2b"/>

## Rules

-   Jobs and schedules created by the multitenant application for a SaaS tenant aren't accessible by other SaaS tenants.

-   Credentials bound to a SaaS tenant could be used to access SaaS tenant bound data only.

-   Credentials bound to the PaaS tenant are bound to the SAP Job Scheduling service instance. This means that the provider of the multitenant application is allowed to create, read, edit, and delete all jobs and schedules for the bound SAP Job Scheduling service instance without any restrictions of SaaS tenants.


**Related Information**  


[SAP Job Scheduling Service REST APIs](../40---Using-JOB-SCHDULR-TITLE/sap-job-scheduling-service-rest-apis-c513d2d.md "Use SAP Job Scheduling service REST APIs to create, manage, and monitor jobs and job schedules.")

