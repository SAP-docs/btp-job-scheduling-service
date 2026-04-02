<!-- loiocb56f9efa8814a3f8276076614e8373a -->

# Create a Service Instance Using CF CLI

To use the SAP Job Scheduling service with action endpoints in your application or with Cloud Foundry tasks, you create an instance of the SAP Job Scheduling service with the service plan `standard` using the Cloud Foundry Command Line Interface \(CF CLI\) and bind the service instance to your application.



<a name="loiocb56f9efa8814a3f8276076614e8373a__prereq_hfb_gfr_5z"/>

## Prerequisites

-   Install CF CLI on your system. For more information, see [Download and Install the Cloud Foundry Command Line Interface](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/4ef907afb1254e8286882a2bdef0edf4.html "Download and set up the Cloud Foundry Command Line Interface (cf CLI) to start working with the Cloud Foundry environment.") :arrow_upper_right:.
-   Deploy the application that requires the SAP Job Scheduling service to the cloud platform. For more information, see [Deploy Business Applications in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/4946ea5421374924963ce8575a5f3d05.html "When an application for the Cloud Foundry environment resides in a folder on your local machine, you can deploy it and start it by executing the command line interface (CLI) command push. To deploy business applications bundled in a multitarget application archive, you have to use the command deploy-mta.") :arrow_upper_right:.



<a name="loiocb56f9efa8814a3f8276076614e8373a__context_a5k_d4t_fsb"/>

## Context

We recommend that you use the service plan `standard` with certificates to bind the service instance to your application. This allows you to enable your application to authentication with a X.509 client certificate.

> ### Note:  
> It's also possible to use the service plan `standard` without certificates.



## Procedure

1.  Open the Cloud Foundry console client.

2.  Check the Service Marketplace to verify that the SAP Job Scheduling service service is listed: `cf marketplace`

3.  Create an instance of the service: `cf create-service jobscheduler` `standard` *<instance name\>*.

    > ### Note:  
    > If you want to use service plan `free` instead, run `cf create-service jobscheduler` `free` *<instance name\>*.

    1.  Optionally, you can provide a `parameters.json` to specify the authentication method:

        -   For SAP Authorization and Trust Management service \(XSUAA\) authentication \(default\): No parameters needed, or explicitly specify in the `parameters.json` file:

            > ### Sample Code:  
            > ```
            > {
            >    "authentication": "xsuaa"
            > }
            > ```

        -   For authentication using Identity Authentication service:

            > ### Sample Code:  
            > ```
            > {
            >    "authentication": "ias"
            > }
            > ```


    2.  Then create the instance with:

        ```
        cf create-service jobscheduler standard <instance name> -c parameters.json
        ```

        **Available Parameters**


        <table>
        <tr>
        <th valign="top">

        Parameter
        
        </th>
        <th valign="top">

        Type
        
        </th>
        <th valign="top">

        Default
        
        </th>
        <th valign="top">

        Description
        
        </th>
        </tr>
        <tr>
        <td valign="top">
        
        `authentication` 
        
        </td>
        <td valign="top">
        
        string
        
        </td>
        <td valign="top">
        
        `"xsuaa"` 
        
        </td>
        <td valign="top">
        
        The authentication method to use.

        Valid values: `"xsuaa"` \(default\) or `"ias"`
        
        </td>
        </tr>
        </table>
        
        > ### Caution:  
        > The authentication method can't be changed after you create the service instance.

        > ### Note:  
        > For authentication using Identity Authentication service, make sure that you've established trust between your subaccount and your SAP Cloud Identity Services tenant using OpenID Connect \(OIDC\). If trust isn't established, the service instance can't be created. For more information, see [Establish Trust and Federation Between SAP Authorization and Trust Management Service and SAP Cloud Identity Services](https://help.sap.com/docs/btp/sap-business-technology-platform/establish-trust-and-federation-between-uaa-and-identity-authentication).


4.  Bind the service instance to the application using the command: `cf bind-service` *<application name\>* *<instance name\>*

    Optionally, you can provide a `parameters.json` to get a binding with certificates:

    > ### Sample Code:  
    > ```
    > {
    >  "credential-type": "x509",
    >  "x509": {
    >  "key-length": 2048,
    >  "validity": 7,
    >  "validity-type": "DAYS"
    >  }
    > }
    > ```

    `cf bind-service`*<application name\>**<instance name\>* `-c parameters.json`

    For more information, see [Binding Parameters of X.509 Secrets](https://help.sap.com/viewer/DRAFT/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/3240307e513e4bceaa75e4134d337fab.html).

    If you're using the Node.js client library `@sap/jobs-client`, please make sure to use a version \>= 1.6.3.

5.  Restage the application using the command : `cf restage` *<application name\>*

6.  Verify that the instance is successfully bound to the application using the command: `cf env` *<application name\>*

    > ### Note:  
    > If the instance is successfully bound, you see SAP Job Scheduling service details and credentials in the `VCAP_SERVICES` environment variable.

    ```json
    A sample VCAP_Services environment variable for standard plan with certificates:
    "VCAP_SERVICES" : {
        "jobscheduler": [
            {
                "name": "scheduler-instance",
                "label": "jobscheduler",
                "tags": [
                    "jobscheduler"
                ],
                "plan": "standard",
                "credentials": {
                    "uaa": {
                        "certificate": "-----BEGIN CERTIFICATE-----\n...\n-----END CERTIFICATE-----\n-----BEGIN CERTIFICATE-----\n...\n-----END CERTIFICATE-----\n-----BEGIN CERTIFICATE-----\n...\n-----END CERTIFICATE-----\n",
                        "certurl": "https://<subdomain>.authentication.cert.<landscape-label>",
                        "clientid": "<client-id>",
                        "credential-type": "x509",
                        "key": "-----BEGIN RSA PRIVATE KEY-----\n...\n-----END RSA PRIVATE KEY-----\n",
                        "uaadomain": "authentication.<landscape-label>",
                        "url": "https://<subdomain>.authentication.<landscape-label>",
                        "verificationkey": "-----BEGIN PUBLIC KEY-----...-----END PUBLIC KEY-----",
                        "xsappname": "<xsappname>",
                    },
                    "url": "https://jobscheduler-rest.cfapps.<landscape-label>"
                }
            }
        ]
    }
    ```

    ```json
    A sample VCAP_Services environment variable:
    "VCAP_SERVICES" : {
        "jobscheduler": [
            {
                "name": "scheduler-instance",
                "label": "jobscheduler",
                "tags": [
                    "jobscheduler"
                ],
                "plan": "standard",
                "credentials": {
                    "uaa": {
                        "clientid": "<client-id>",
                        "clientsecret": "<client-secret>",
                        "credential-type": "binding-secret",
                        "url": "https://<subdomain>.authentication.<landscape-label>",
                        "verificationkey": "-----BEGIN PUBLIC KEY-----...-----END PUBLIC KEY-----",
                        "xsappname": "<xsappname>",
                    },
                    "url": "https://jobscheduler-rest.cfapps.<landscape-label>"
                }
            }
        ]
    }
    
    ```

    ```json
    A sample VCAP_Services environment variable for authentication with Identity Authentication service:
    "VCAP_SERVICES": {
       "jobscheduler": [
          {
             "name": "scheduler-instance",
             "label": "jobscheduler",
             "tags": [
                "jobscheduler"
             ],
             "plan": "standard",
             "credentials": {
                "url": "https://jobscheduler-rest.cfapps.<landscape-label>"
             }
          }
       ]
    }
    ```

    > ### Note:  
    > For authentication with Identity Authentication service, the SAP Job Scheduling service binding contains only the REST API URL. Authentication credentials come from your SAP Cloud Identity Services - Identity Authentication service binding, not from the SAP Job Scheduling service binding. For setup details, see [Secure Access](50---Security/secure-access-745ca50.md).


