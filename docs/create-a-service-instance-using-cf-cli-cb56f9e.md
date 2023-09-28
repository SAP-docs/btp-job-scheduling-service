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

3.  Create an instance of the service: `cf create-service jobscheduler` `standard` *<instance name\>* `-c '{"enable-xsuaa-support": true}'` .

    > ### Note:  
    > Enable xsuaa by specifying the `enable-xsuaa-support` parameter as true.

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

    If you're using the node client library `@sap/jobs-client`, please make sure to use a version \>= 1.6.3.

5.  Restage the application using the command : `cf restage` *<application name\>*

6.  Verify that the instance is successfully bound to the application using the command: `cf env` *<application name\>*

    > ### Note:  
    > If the instance is successfully bound, you see SAP Job Scheduling service details and credentials in the `VCAP_SERVICES` environment variable.

    ```json
    A sample VCAP_Services environment variable for standard plan with certificates appears as below:
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
    A sample VCAP_Services environment variable appears as below:
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


