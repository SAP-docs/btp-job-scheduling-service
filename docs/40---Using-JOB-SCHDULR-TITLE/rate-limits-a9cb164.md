<!-- loioa9cb164c26f64b7980ca1bc4377dd87f -->

# Rate Limits

When you use the SAP Job Scheduling service REST API, rate limits are used to limit the number of requests against the REST API. Requests can be throttled \(delayed\), and if there is a very high load also denied.



A retry header is provided. If requests are denied, you can use a retry header to retry the request. After less than one minute, you can execute the request again.

The following limits are available:

**Absolute Limit**

-   If this limit is **almost exceeded**, the service throttles the response. The throttling of the response increases with the number of requests until the limit is fully exceeded. A 'throttling' \(custom\) header is in place.

-   If this limit is **fully exceeded**, the service responds with '503 - Service Unavailable'.

    > ### Note:  
    > A 'throttling'-header is provided. This is the number of milliseconds by which the response was delayed by the server.

-   This limit counts and effects all requests regardless of the client, tenant, or service instance.


**Client Limit**

-   If this limit is **almost exceeded**, the service throttles the response. The throttling of the response increases with the number of requests until the limit is fully exceeded. A 'throttling' header is in place.

-   If this limit is **fully exceeded**, the service responds with '429 - Too many requests'. A retry header is in place.

    > ### Note:  
    > A 'retry-after'-header is provided. This is the number of seconds after which the same request should be executed again. See [https://httpwg.org/specs/rfc7231.html\#header.retry-after](https://httpwg.org/specs/rfc7231.html#header.retry-after).


A client can be seen as a tenant.

All of the limits and response effects are stacking, that means absolute limit and client limit add up.

> ### Example:  
> **GET request handling with absolute and client limit setting when request is throttled**
> 
> Both limits \(absolute and client\) have different thresholds in the following example. The numbers used are just examples.
> 
> A higher request counter per minute results in a higher response delay or even in a denial of a request.
> 
> -   For the absolute limit, the current internal request counter value is set to **512**.
> 
> -   The absolute limit has a threshold value of **400**. If this value is exceeded, throttling is done. In this case, a request-header 'throttling' is in place providing the number of milliseconds of how long the response was throttled, e.g. **1000** ms.
> 
> -   If the counter of client limit is **51** and the client limit has a threshold value of 50, exceeding the threshold results in a throttling for **250** ms, for example.
> 
> -   Both limits are stacking, that means throttling adds up to **1250** ms in total. The 'throttling' header has a value of **1250**.

> ### Example:  
> **GET request handling with absolute and client limit setting when request is denied**
> 
> Both limits \(absolute and client\) have different thresholds in the following example. The numbers used are just examples.
> 
> A higher request counter per minute results in a higher response delay or even in a denial of a request.
> 
> -   For the absolute limit, the current internal request counter value is set to **2156**.
> 
> -   The absolute limit has a threshold value of **2000**. If this value is exceeded, throttling is done. In this case, a request-header 'throttling' is in place providing the number of milliseconds of how long the response was throttled, **5000** ms, for example.
> 
> -   If the counter of client limit is **341** and the client limit has a threshold value of **300**, exceeding the threshold results in a deny of the request.
> 
> -   Both limits are stacking, that means throttled adds up to **5000** ms in total. The 'throttling' header has a value of**5000**. After the throttling is done, the request is denied with '429 - Too many requests'.
> 
> 
> If the "deny" client limit threshold is reached, the HTTP response is '429 - Too many requests'. If the "deny" absolute limit is reached, the HTTP response is '503 - Service Unavailable'. All the limits have different threshold values, which could lead to different throttling values or even a request deny.

**Related Information**  


[Understanding Offset and Cursor Pagination](understanding-offset-and-cursor-pagination-96ebd22.md "Pagination helps you manage large data sets by breaking them into smaller, more manageable chunks of data. When you retrieve job run logs, you can use two types of pagination: offset pagination and cursor pagination.")

[Authentication](authentication-5dca60b.md "This section describes different ways how the application accesses the SAP Job Scheduling service REST APIs depending on the service plan you use.")

[REST APIs](rest-apis-3dcd04a.md "SAP Job Scheduling service REST APIs")

