<!-- loio08933d33f5f64db69f93a984516295ce -->

# Define and Grant Scopes to SAP Job Scheduling Service

Create and grant a scope to SAP Job Scheduling service.



<a name="loio08933d33f5f64db69f93a984516295ce__prereq_myy_jqf_wnb"/>

## Prerequisites

You've created an xsuaa service instance and bound it to the application.

For more information, see [Getting Started](../30---Getting-Started/getting-started-02e4e8b.md).



## Context

For the service plan *standard*, SAP Job Scheduling service uses User Account and Authentication \(UAA\) to facilitate the OAuth 2.0 authorization for job action endpoints. The action endpoint is secured via OAuth 2.0 scopes, hence, the application must grant a scope to the SAP Job Scheduling service.

> ### Note:  
> The following steps provide an example.



## Procedure

1.  To grant scopes to SAP Job Scheduling service, open the `xs-security.json` file that is used for the xsuaa service instance bound to the application and add the following to the `scopes` section:

    > ### Sample Code:  
    > Example `xs-security.json` file, **scope** section
    > 
    > ```
    > "scopes": [{
    >     "name": "$XSAPPNAME.JOBSCHEDULER",
    >     "description": "Job Scheduler Scope",
    >     "grant-as-authority-to-apps": ["$XSSERVICENAME(<jobscheduler instance name>)"]
    >     }]
    > ```

2.  Update the xsuaa service instance with the updated `xs-security.json`:

    ```
    cf update-service <xsuaa-instance-name> -c xs-security.json
    ```


**Related Information**  


[Update a Service Instance](https://help.sap.com/viewer/ae8e8427ecdf407790d96dad93b5f723/Validation/en-US/7f926eb79a7746fd996363118cd2c2aa.html "You can update a service instance from the xsuaa service using the service broker.") :arrow_upper_right:

