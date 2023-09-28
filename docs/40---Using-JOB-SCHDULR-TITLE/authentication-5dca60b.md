<!-- loio5dca60bd7b8a4670ab524fcfcb65aafc -->

# Authentication

This section describes different ways how the application accesses the SAP Job Scheduling service REST APIs depending on the service plan you use.



<a name="loio5dca60bd7b8a4670ab524fcfcb65aafc__section_c4y_t43_gvb"/>

## Service Plan `lite`

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

## Service Plan `standard`

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


**Related Information**  


[Rate Limits](rate-limits-a9cb164.md "When you use the SAP Job Scheduling service REST API, rate limits are used to limit the number of requests against the REST API. Requests can be throttled (delayed), and if there is a very high load also denied.")

[REST APIs](rest-apis-3dcd04a.md "SAP Job Scheduling service REST APIs")

[Create a Service Instance Using CF CLI](../create-a-service-instance-using-cf-cli-cb56f9e.md "To use the SAP Job Scheduling service with action endpoints in your application or with Cloud Foundry tasks, you create an instance of the SAP Job Scheduling service with the service plan standard using the Cloud Foundry Command Line Interface (CF CLI) and bind the service instance to your application.")

[Create Service Keys Using the Cloud Foundry Command Line Interface](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/7de6b314b62748b9b59df5fc09dbe8fb.html "Use the Cloud Foundry Command Line Interface to create a service key.") :arrow_upper_right:

