<!-- loiod9fd81ccabe2410f8b2434311d43c733 -->

# Asynchronous Mode

The SAP Job Scheduling service executes jobs that support action endpoints in a synchronous mode or in an asynchronous \(or batch\) mode.



<a name="loiod9fd81ccabe2410f8b2434311d43c733__section_hbf_b2p_d4b"/>

## Synchronous Mode

Synchronous requests are used if the SAP Job Scheduling service calls the action endpoint of the application and the application logic is executed in a short span of time.

> ### Example:  
> The exchange rate application fetches the latest currency exchange rates frequently using scheduled jobs.

> ### Note:  
> -   When the scheduler invokes the endpoint, the application must return the response with an appropriate HTTP status code, indicating success or failure.
> 
> -   To indicate success, the application must use a suitable standard status code between 200 and 399, except 202-ACCEPTED.
> 
> -   To indicate an execution failure, the application must use one of the server error codes as outlined in the HTTP protocol specification.



<a name="loiod9fd81ccabe2410f8b2434311d43c733__section_hnn_b2p_d4b"/>

## Asynchronous or Batch Mode

Asynchronous requests are used for job runs with a large span of time.

> ### Example:  
> Action endpoints that trigger long-running processes
> 
> SAP Job Scheduling service operates in asynchronous mode if your application contains a module that synchronizes database tables, which are long-running tasks.

> ### Note:  
> -   When the scheduler invokes the endpoint, it passes the request headers values “x-sap-job-id”, “x-sap-job-schedule-id”, “x-sap-job-run-id”, and “x-sap-scheduler-host” for the Job ID, Job Schedule ID, Job Run ID, and the SAP Job Scheduling service Host URI, respectively. The application must extract the header values and store them using a suitable mechanism, such as in-memory storage that uses caches or libraries, or persistent storage that uses a database.
> 
> -   The application must return an acknowledgement response with the HTTP status code 202-ACCEPTED. The response indicates to the scheduler that the application has accepted and is processing the request. If the application returns a server error code, the scheduler interprets it as a failure of the job run.
> 
> -   After the application completes the job processing, it must invoke the Update of Job Run Log API to indicate success or failure and \(optionally\) create log text for the job run. For information about this API, see [Update Job Run Log](../40---Using-JOB-SCHDULR-TITLE/update-job-run-log-e85da40.md). The path parameters for the Update of Job Run Log API call must be the values of the headers as described above.
> 
> -   If the application doesn't invoke the Update of Job Run Log API, the scheduler isn't notified of the status of the job run and, after a configurable time interval, reverts the job to the status UNKNOWN.

> ### Note:  
> Cloud Foundry tasks always run asynchronously.

**Related Information**  


[About Cloud Foundry Tasks](https://docs.cloudfoundry.org/devguide/using-tasks.html)

