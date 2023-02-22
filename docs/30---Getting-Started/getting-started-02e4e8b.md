<!-- loio02e4e8bbcd7c4d5ea154f5d9aa2f46ac -->

# Getting Started

Once you've completed the initial setup for SAP Job Scheduling service, to use the service you create a service instance and bind it to your application.

In the Cloud Foundry environment, you enable services by creating a service instance using either the SAP BTP cockpit or the Cloud Foundry command line interface \(CLI\), and binding that instance to your application. A service instance is a single instantiation of a service running on SAP BTP. For more information, see [About Services](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/d1d0fc8e78474494a59caad02259ec7e.html).

Determine how to proceed based on whether you're using a new application or an existing application that is already bound to an xsuaa service instance:

> ### Remember:  
> You must perform the following steps in the given order for the SAP Job Scheduling service to work.

**Using a New Application:**

If you're using a new app, proceed as follows:

1.  Create an instance of the SAP Job Scheduling service.

2.  Create an xsuaa service instance.

    > ### Note:  
    > If you already have an xsuaa service instance, remember to update it first with the updated `xs-security.json` file.
    > 
    > This is necessary as the content in the `xs-security.json` in which the scope is granted to the SAP Job Scheduling service with the `grant-as-authority-to-apps` has changed.

3.  Deploy the application.

    > ### Tip:  
    > When you deploy an application to a space and want to use the SAP Job Scheduling service, you must first create a SAP Job Scheduling service instance in the space you're working in. Then, when you push \(or upload\) your application, you can bind your application to the SAP Job Scheduling service instance.
    > 
    > For more information, see [Binding Service Instances to Applications](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/e98280a71f17413088f8a10838a1e4cc.html).

4.  Bind the xsuaa service instance to your application.

5.  Bind the SAP Job Scheduling service instance to your application.

    > ### Note:  
    > If you don't bind your application to the SAP Job Scheduling service instance, you can't call the SAP Job Scheduling service from your own application.


**Using an Existing Application:**

If you're using an existing app, proceed as follows:

1.  Create an instance of the SAP Job Scheduling service.

2.  Update your xsuaa service instance.

    > ### Note:  
    > This is necessary as the content in the `xs-security.json` where the scope is granted to the SAP Job Scheduling service with the `grant-as-authority-to-apps` has changed.

3.  Bind the SAP Job Scheduling service instance to your application.




**Related Information**  


[Create a Service Instance in SAP BTP Cockpit](create-a-service-instance-in-sap-btp-cockpit-e267ab6.md "To use the SAP Job Scheduling service with action endpoints in your application or with Cloud Foundry tasks, you create an instance of the SAP Job Scheduling service using the SAP BTP cockpit and bind the service instance to your application.")

[Create a Service Instance Using CF CLI](create-a-service-instance-using-cf-cli-cb56f9e.md "To use the SAP Job Scheduling service with action endpoints in your application or with Cloud Foundry tasks, you create an instance of the SAP Job Scheduling service with the service plan standard using the Cloud Foundry Command Line Interface (CF CLI) and bind the service instance to your application.")

[Define and Grant Scopes to SAP Job Scheduling Service](../50---Security/define-and-grant-scopes-to-sap-job-scheduling-service-08933d3.md "Create and grant a scope to SAP Job Scheduling service.")

[Update a Service Instance](https://help.sap.com/viewer/ae8e8427ecdf407790d96dad93b5f723/Validation/en-US/7f926eb79a7746fd996363118cd2c2aa.html "You can update a service instance from the xsuaa service using the service broker.") :arrow_upper_right:

[Initial Setup](../initial-setup-0adb655.md "You can get started with the SAP Job Scheduling service using the standard procedures for the Cloud Foundry environment.")

