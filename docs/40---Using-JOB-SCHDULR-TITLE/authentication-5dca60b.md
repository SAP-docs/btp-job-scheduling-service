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

In the `VCAP_SERVICES` of your application, you can find the following section:

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
> If you're using binding with certificates, the binding looks different. The binding has fields that are named differently or that are missing, for example, `certificate` and `key` instead of `clientsecret`.

Depending on which binding you choose, proceed as follows:

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


    For more information, see [Create a Service Instance Using CF CLI](../30---Getting-Started/create-a-service-instance-using-cf-cli-cb56f9e.md).

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

