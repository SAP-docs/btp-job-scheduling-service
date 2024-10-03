<!-- loio224a49afe3fc40848f94bbf4cf4747b1 -->

# Create a Service Instance in the Kyma Dashboard

To use the SAP Job Scheduling service with action endpoints in your application, you create an instance of the SAP Job Scheduling service using the SAP BTP cockpit and bind the service instance to your application.



<a name="loio224a49afe3fc40848f94bbf4cf4747b1__prereq_kbr_wzt_vz"/>

## Prerequisites

You've logged on to the SAP BTP cockpit. For more information, see [Navigate in the Cockpit](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/0874895f1f78459f9517da55a11ffebd.html "Learn how to navigate to your global accounts, directories, and subaccounts in the SAP BTP cockpit.") :arrow_upper_right:.



## Procedure

1.  Navigate to the subaccount in which the Kyma runtime is enabled.

2.  Click on the link to access the dashboard.

3.  Select your Kyma namespace.

4.  In the navigation area, choose *Service Instances*.

5.  Choose *Create Service Instances*.

6.  Provide the required details.

    > ### Note:  
    > For productive usage of the SAP Job Scheduling service, use the service name `jobscheduler` and plan `standard`.

7.  Choose *Create* and verify the instance details.

    You've created a service instance in your Kyma namespace that's now available in the service instances section.

8.  In the navigation area, choose *Service Bindings*.

9.  Provide the required details.

10. Choose *Create* and verify the binding details.




<a name="loio224a49afe3fc40848f94bbf4cf4747b1__result_oy1_1gp_n4b"/>

## Results

Your service now has a service binding. To use it, it must be mounted within your application. For more information, see [Using SAP BTP Services in the Kyma Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/ea4dd81e49254dd482d32e3c20f4477a.html#loioea4dd81e49254dd482d32e3c20f4477a "With the Kyma environment, you can connect SAP BTP services to your cluster and manage them using SAP BTP Service Operator.") :arrow_upper_right:.

**Related Information**  


[Development in the Kyma Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/606ec610ee4746c09d5d2bef5a85a124.html "Learn more about developing applications in SAP BTP, Kyma runtime.") :arrow_upper_right:

