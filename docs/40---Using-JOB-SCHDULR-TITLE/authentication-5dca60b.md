<!-- loio5dca60bd7b8a4670ab524fcfcb65aafc -->

# Authentication

This section describes how the application accesses the SAP Job Scheduling service REST APIs. The access method depends on the service plan and authentication method you use.

For the `standard` and `free` service plans, you can choose between two authentication methods when creating the service instance:

-   XSUAA \(default\): Uses the SAP Authorization and Trust Management service \(XSUAA\) with OAuth 2.0 authentication.
-   SAP Cloud Identity Services - Identity Authentication: Uses the Identity Authentication service with OAuth 2.0 authentication.



<a name="loio5dca60bd7b8a4670ab524fcfcb65aafc__section_c4y_t43_gvb"/>

## Service Plan `lite`

> ### Note:  
> Starting 22 January 2026, service plan `lite` is deprecated on SAP BTP Trial. As an alternative, you can use service plan `free`.

The SAP Job Scheduling service REST APIs are guarded by HTTP Basic authentication, which requires a user name and a password. Both are fetched from the `VCAP_SERVICES` section of the application environment after binding it to the SAP Job Scheduling service.

Use the following command to view the `VCAP_SERVICES` content:

```
$ cf env <application-name>
{
    "VCAP_SERVICES": {
        "jobscheduler": [
            {
                "credentials": {
                    "clientid": "PRIVATE_DATA_HIDDEN",
                    "identityzone": "PRIVATE_DATA_HIDDEN",
                    "password": "PRIVATE_DATA_HIDDEN",
                    "url": "https://jobscheduler-rest.cfapps.stagingaws.hanavlab.ondemand.com",
                    "user": "PRIVATE_DATA_HIDDEN",
                    "xsappname": "PRIVATE_DATA_HIDDEN"
                },
                "label": "jobscheduler",
                "name": "js-instance",
                "plan": "default",
                "provider": null,
                "syslog_drain_url": null,
                "tags": [
                    "jobscheduler"
                ]
            }
        ]
    }
}
```

All APIs are accessed through HTTPS.

> ### Note:  
> All data is sent and received in the JSON format. When sending data through API requests, make sure that the HTTP header `Content-type` is set to `application/json`.



<a name="loio5dca60bd7b8a4670ab524fcfcb65aafc__section_spd_543_gvb"/>

## Service Plan `standard` with XSUAA Authentication

You can access the REST API for a `standard` instance by providing an OAuth token.

You can use app bindings and service keys to generate credentials for a service instance in Cloud Foundry.

If you've bound the service instance to an application, you find the following section in the `VCAP_SERVICES` of your application:

```
{
    "jobscheduler": [
        {
            "..": "..",
            "credentials": {
                "uaa": {
                    "apiurl": "<apiurl>",
                    "clientid": "<clientid>",
                    "clientsecret": "<clientsecret>",
                    "identityzone": "<identityzone>",
                    "identityzoneid": "<identityzoneid>",
                    "sburl": "<sburl>",
                    "tenantid": "<tenantid>",
                    "tenantmode": "dedicated",
                    "uaadomain": "<uaadomain>",
                    "url": "<url>",
                    "verificationkey": "<key>",
                    "xsappname": "<xsappname>"
                },
                "url": "https://jobscheduler-rest.<landscape-domain>"
            },
            "...": "..."
        }
    ]
}
```

> ### Note:  
> If you use binding with certificates, the binding looks different. The binding has fields that are named differently or that are missing, for example, `certificate` and `key` instead of `clientsecret`.

Alternatively, you can create a service key using `cf create-service-key` *<jobscheduler-instance-name\>**<key-name\>* and view the credentials using `cf service-key` *<jobscheduler-instance-name\>* *<key-name\>*.

Service keys also allow the same parameters as bindings, for example, if you're using binding with certificates:

`cf create-service-key` *<jobscheduler-instance-name\>* *<key-name\>* -c parameters.json with parameters.json as:

```
{
"credential-type": "x509",
  "x509": {
    "key-length": 2048,
    "validity": 7,
    "validity-type": "DAYS"
  }
}
```

Depending on the type of credentials you obtain, proceed as follows:

1.  To fetch an OAuth token from xsuaa, use one of the following options:

    1.  Use the provided `clientid` and `clientsecret`:

        ```
        Method: POST
        Url: <value from credentials.uaa.url>/oauth/token
        Header:
            Content-Type: application/x-www-form-urlencoded
            Authorization: Basic <Base64 encoded clientid:clientsecret>
            Cache-Control: no-cache
        Body:
            grant_type=client_credentials
        ```

        The response should look as follows:

        ```
        {
            "access_token": "<token>",
            "token_type": "bearer",
            "expires_in": 43199,
            "scope": "<scope(s)>",
            "jti": "<hidden>"
        }
        ```

    2.  Use the provided `clientid` and `certificates`:

        Extract the value of the fields `certificate` and `key` to files named `cert.pem` and `key.pem` of the application environment in `VCAP_SERVICES`.

        > ### Note:  
        > The certificate and key string in the environment contain new line escape sequences \\n, which have to be replaced by actual line breaks of your OS if used in `cert.pem` and `key.pem`.

        > ### Example:  
        > Example using curl to retrieve the access token:
        > 
        > ```
        > 
        > curl --cert cert.pem --key key.pem -XPOST <certurl>/oauth/token -d 'grant_type=client_credentials&client_id=<clientid>'
        > 
        > ```


    For more information, see [Create a Service Instance Using CF CLI](../create-a-service-instance-using-cf-cli-cb56f9e.md).

2.  Use the `access_token` in your request to the SAP Job Scheduling service REST API:

    ```
    ...
    Url: <value from credentials.url>/scheduler/
    Header:
        Authorization: Bearer <access_token>
    ...
    ```




## Service Plan `standard` with Identity Authentication

If you created your service instance with `authentication: "ias"`, you access the REST API using OAuth tokens obtained from your Identity Authentication service tenant.



### Prerequisites

-   An SAP Job Scheduling service instance created with `authentication: "ias"`

-   An Identity Authentication service instance with the SAP Job Scheduling service specified in `consumed-services`

-   The Identity Authentication service instance is bound to your application.




### Setup

1.  Create an Identity Authentication service instance with the SAP Job Scheduling service as a consumed service in the configuration JSON file:
    1.  > ### Sample Code:  
        > ```
        > {
        >    "display-name": "My Application",
        >    "consumed-services": [
        >       {
        >          "service-instance-name": "<jobscheduler-instance-name>"
        >       }
        >    ]
        > }
        > ```

    2.  > ### Sample Code:  
        > ```
        > cf create-service identity application identity-instance -c <ias-config>.json
        > ```


2.  Bind the Identity Authentication service instance to your application:

    > ### Sample Code:  
    > ```
    > cf bind-service <app-name> identity-instance
    > ```

    > ### Note:  
    > For multitenant applications, use X.509 certificate credentials:
    > 
    > 1.  > ### Sample Code:  
    >     > ```
    >     > {
    >     >    "credential-type": "X509_GENERATED",
    >     >    "key-length": 2048,
    >     >    "validity": 365,
    >     >    "validity-type": "DAYS",
    >     >    "app-identifier": "<your-app-name>"
    >     > }
    >     > ```
    > 
    > 2.  > ### Sample Code:  
    >     > ```
    >     > cf bind-service <app-name> identity-instance -c <binding-parameters>.json
    >     > ```




### Fetch an OAuth Token

Retrieve credentials from your Identity Authentication service binding and use them to obtain an access token. Use one of the following methods:

-   Using client credentials

    > ### Sample Code:  
    > ```
    > curl -X POST "https://<ias-tenant>/oauth2/token" \
    > -H "Content-Type: application/x-www-form-urlencoded" \
    > -d "grant_type=client_credentials" \
    > -d "client_id=<client-id>" \
    > -d "client_secret=<client-secret>"
    > ```

-   Using X.509 certificates \(required for multitenant applications\)

    1.  Extract the `certificate` and `key` fields from your Identity Authentication service binding to files `cert.pem` and `key.pem`.

        > ### Sample Code:  
        > ```
        > curl -X POST "https://<ias-tenant>/oauth2/token" \
        >   --cert cert.pem \
        >   --key key.pem \
        >   -H "Content-Type: application/x-www-form-urlencoded" \
        >   -d "grant_type=client_credentials" \
        >   -d "client_id=<client-id>"
        > ```

        > ### Note:  
        > For multitenancy: When making API calls on behalf of a subscriber tenant, fetch the token from the subscriber's Identity Authentication service tenant and include the `app_tid` parameter.
        > 
        > > ### Sample Code:  
        > > ```
        > > curl -X POST "https://<subscriber-ias-tenant>/oauth2/token" \
        > >   --cert cert.pem \
        > >   --key key.pem \
        > >   -H "Content-Type: application/x-www-form-urlencoded" \
        > >   -d "grant_type=client_credentials" \
        > >   -d "client_id=<client-id>" \
        > >   -d "app_tid=<subscriber-tenant-id>"
        > > ```
        > 
        > For more information, see [Multitenancy in SAP Job Scheduling Service](../20---Concepts/multitenancy-in-sap-job-scheduling-service-464b613.md).

    2.  Use the `access_token` from the response in your request to the SAP Job Scheduling service REST API:

        > ### Sample Code:  
        > ```
        > ...
        > Url: <value from jobscheduler credentials.url>/scheduler/
        > Header:
        >     Authorization: Bearer <access_token>
        > ...
        > ```


    > ### Note:  
    > If your application uses multiple SAP Job Scheduling service instances, specify the target instance using the `x-sap-scheduler-instance-id` request header.




## Service Plan `free`

> ### Note:  
> The `free` plan provides the same functionality as the `standard` plan but has usage restrictions and doesn't include support. For more information, see [SAP Job Scheduling service on SAP Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/job-scheduling-service?region=all&tab=service_plan).

You set up authentication the same way you do for service plan `standard`.

> ### Note:  
> If you upgrade your plan, all executions performed on the same day are charged toward the `standard` plan.

**Related Information**  


[Understanding Offset and Cursor Pagination](understanding-offset-and-cursor-pagination-96ebd22.md "Pagination helps you manage large data sets by breaking them into smaller, more manageable chunks of data. When you retrieve job run logs, you can use two types of pagination: offset pagination and cursor pagination.")

[Pagination Guide for GET /scheduler/jobs](pagination-guide-for-get-scheduler-jobs-9b22bbf.md "Starting 25 June 2026, the GET /scheduler/jobs endpoint enforces pagination on all responses. If you currently call this endpoint without a page_size parameter, your response will be limited to 10 jobs by default instead of returning every job in your service instance.")

[Rate Limits](rate-limits-a9cb164.md "When you use the SAP Job Scheduling service REST API, rate limits are used to limit the number of requests against the REST API. Requests can be throttled (delayed), and if there is a very high load also denied.")

[REST APIs](rest-apis-3dcd04a.md "SAP Job Scheduling service REST APIs")

[SAP Job Scheduling Service REST API](https://api.sap.com/api/sap-btpjss-admin-v1/overview)

[Create a Service Instance Using CF CLI](../create-a-service-instance-using-cf-cli-cb56f9e.md "To use the SAP Job Scheduling service with action endpoints in your application or with Cloud Foundry tasks, you create an instance of the SAP Job Scheduling service with the service plan standard using the Cloud Foundry Command Line Interface (CF CLI) and bind the service instance to your application.")

[Create Service Keys Using the Cloud Foundry Command Line Interface](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/7de6b314b62748b9b59df5fc09dbe8fb.html "Use the Cloud Foundry Command Line Interface to create a service key.") :arrow_upper_right:

[Lite Plan Deprecation: Time to Upgrade to Free! \(SAP Community\)](https://community.sap.com/t5/technology-blog-posts-by-sap/lite-plan-deprecation-time-to-upgrade-to-free-sap-job-scheduling-service/ba-p/14314717)

[SAP Cloud Identity Services](https://help.sap.com/docs/cloud-identity-services)

[Secure Access](../50---Security/secure-access-745ca50.md "The SAP Job Scheduling service provides options to secure job actions with action endpoints as well as to secure Cloud Foundry tasks.")

