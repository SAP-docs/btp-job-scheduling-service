<!-- loio9b861273d16a41ecbc77b583c7cad5aa -->

# Node.js Client Library

Directly access Node.js APIs.



For jobs that support action endpoints \(HTTP jobs\), the SAP Job Scheduling service provides an API client library in the Node.js language. This library allows you to directly access Node.js APIs and reduce the code required to consume the service. See [https://registry.npmjs.org](https://registry.npmjs.org).

Use the following code snippet for all API calls:

```
const JobSchedulerClient = require('@sap/jobs-client');
  const scheduler = new JobSchedulerClient.Scheduler();
  let myJob = { /* Refer to the SAP Job Scheduling
                                service documentation for sample JSON Object.  */ };

```

The following table shows all SAP Job Scheduling service APIs together with a Node.js sample code to access the API.

**Node.js Samples for SAP Job Scheduling service APIs**


<table>
<tr>
<th valign="top">

API



</th>
<th valign="top">

Sample Code to Access the API



</th>
</tr>
<tr>
<td valign="top">

 [Create Job](create-job-2c1ecb6.md) 



</td>
<td valign="top">

```
var scJob = { job: myJob };

  scheduler.createJob(scJob, function (error, body) {
    if (error) {
      return logger.log('Error registering new job %s', error);
    }
    // Job successfully created.
    job.id = body._id; 
  });
```



</td>
</tr>
<tr>
<td valign="top">

Update Job



</td>
<td valign="top">

```
var req = {
    jobId: 33, /* Job ID for the job you need to update*/
    job: {
      user : 'John',
      password : 'secret',
      active : 1
    }
  };
  scheduler.updateJob(req, function(err, result) {
    if(err){
      return logger.log('Error updating job: %s', err);
    }
    //job was updated successfully
  });

```



</td>
</tr>
<tr>
<td valign="top">

 [Delete Job](delete-job-cd8feb7.md) 



</td>
<td valign="top">

```
  var req = {
    jobId: 33
  }; 
  scheduler.deleteJob(req, function(err, result) {
    if(err){
      return logger.log('Error deleting job: %s', err);
    }
    //job was deleted successfully
  });

```



</td>
</tr>
<tr>
<td valign="top">

Get Job Details



</td>
<td valign="top">

```
var req = {
    //by Id
    jobId: 33
  }; 
  scheduler.fetchJob(req, function(err, result) {
    if(err){
      return logger.log('Error retrieving job: %s', err);
    }
    //job details retrieved successfully
  });
  var req = {
    //by name
    name: 'my job'
  };
  scheduler.fetchJob(req, function(err, result) {
    if(err){
      return logger.log('Error retrieving job: %s', err);
    }
    //job details retrieved successfully
  });


```



</td>
</tr>
<tr>
<td valign="top">

 [Create Job Schedule](create-job-schedule-66ab3c1.md) 



</td>
<td valign="top">

```
 var mySchedule = { /* according to SAP Job Scheduling
                                service documentation */ }
  var req = {
    jobId: 33,
    schedule: mySchedule
  };
  scheduler.createJobSchedule(req, function(err, result) {
    if(err){
      return logger.log('Error creating job schedule: %s', err);
    }
    //Schedule created successfully
  });
```



</td>
</tr>
<tr>
<td valign="top">

Update Job Schedule



</td>
<td valign="top">

```
  var req = {
    jobId: 33,
    scheduleId: 'ABC-DEF',
    schedule: {
      cron: "* * * * 4"
    }
  };
  scheduler.updateJobSchedule(req, function(err, result) {
    if(err){
      return logger.log('Error updating job schedule: %s', err);
    }
    //Schedule updated successfully
  });
```



</td>
</tr>
<tr>
<td valign="top">

 [Delete Job Schedule](delete-job-schedule-3066b6d.md) 



</td>
<td valign="top">

```
  var req = {
    jobId: 33,
    scheduleId: 'ABC-DEF'
  };
  scheduler.deleteJobSchedule(req, function(err, result) {
    if(err){
      return logger.log('Error deleting schedule: %s', err);
    }
    //Schedule deleted successfully
  });
```



</td>
</tr>
<tr>
<td valign="top">

Get all Jobs



</td>
<td valign="top">

```
  var req = {};
  scheduler.fetchAllJobs(req, function(err, result) {
    if(err){
      return logger.log('Error retrieving jobs: %s', err);
    }
    //Jobs retrieved successfully
  });


```



</td>
</tr>
<tr>
<td valign="top">

Get Job Schedule Details



</td>
<td valign="top">

```
var req = {
    jobId: 33,
    scheduleId: 'ABC-DEF',
    displayLogs: false
  };
  scheduler.fetchJobSchedule(req, function(err, result) {
    if(err){
      return logger.log('Error retrieving schedule: %s', err);
    }
    //Schedule retrieved successfully
  });

```



</td>
</tr>
<tr>
<td valign="top">

Get Schedules of Job



</td>
<td valign="top">

```
  var req = {
    jobId: 33
  };
  scheduler.fetchJobSchedules(req, function(err, result) {
    if(err){
      return logger.log('Error retrieving all schedules: %s', err);
    }
    //All schedules retrieved successfully
  });
```



</td>
</tr>
<tr>
<td valign="top">

Update Run Log of Schedule



</td>
<td valign="top">

```
  var req = {
    jobId: 33,
    scheduleId: 'ABC-DEF',
    runId: 1,
    data: data
  };
  scheduler.updateJobRunLog(req, function(err, result) {
    if(err){
      return logger.log('Error updating run log: %s', err);
    }
    //Run log updated successfully
  });

```



</td>
</tr>
<tr>
<td valign="top">

Get Run Logs of Schedule



</td>
<td valign="top">

```
  var req = {
    jobId: 33,
    scheduleId: 'ABC-DEF'
  };
  scheduler.getRunLogs(req, function(err, result) {
    if(err){
      return logger.log('Error retrieving run logs: %s', err);
    }
    //Run log retrieved successfully
  });
```



</td>
</tr>
<tr>
<td valign="top">

 [Delete All Job Schedules](delete-all-job-schedules-0aab1ab.md) 



</td>
<td valign="top">

```
  var req = {
    jobId: 3
  };
  scheduler.deleteAllJobSchedules(req, function(err, result) {
    if(err){
      return logger.log('Error deleting schedules: %s', err);
    }
    //All schedules deleted successfully
  });

```



</td>
</tr>
<tr>
<td valign="top">

Bulk Activation of Schedules of Job



</td>
<td valign="top">

```
var req = {
    jobId: 3
  };
  scheduler.activateAllSchedules(req, function(err, result) {
    if(err){
      return logger.log('Error activating bulk schedules: %s', err);
    }
    //All schedules activated successfully
  });

```



</td>
</tr>
<tr>
<td valign="top">

Bulk Deactivation of Schedules of Job



</td>
<td valign="top">

```
  var req = {
    jobId: 3
  };
  scheduler.deactivateAllSchedules(req, function(err, result) {
    if(err){
      return logger.log('Error deactivating bulk schedules: %s', err);
    }
    //All schedules deactivated successfully
  });

```



</td>
</tr>
<tr>
<td valign="top">

Get Action Logs of Job



</td>
<td valign="top">

```
  var req = {
    jobId: 3
  };
  scheduler.getJobActionLogs(req, function(err, result) {
    if(err){
      return logger.log('Error retrieving action logs: %s', err);
    }
    //All actionlogs logs retrieved successfully
  });

```



</td>
</tr>
<tr>
<td valign="top">

Get Action Logs of Schedule



</td>
<td valign="top">

```
    var req = {
    jobId: 3,
    scheduleId: "ABC-DEF"
  };
  scheduler.getScheduleActionLogs(req, function(err, result) {
    if(err){
      return logger.log('Error retrieving action logs: %s', err);
    }
    //All actionlogs logs retrieved successfully
  });

```



</td>
</tr>
<tr>
<td valign="top">

Get Active and Inactive Job Count



</td>
<td valign="top">

```
  var req = {
    activeStatus: true // true- for getting active number of jobs and false- for getting inactive number of jobs
  };
  scheduler.getJobCount(req, function(err, result) {
    if(err){
      return logger.log('Error retrieving jobcount: %s', err);
    }
    //Active Job count retrieved successfully
  });

```



</td>
</tr>
</table>

**Related Information**  


[SAP Job Scheduling Service REST APIs](sap-job-scheduling-service-rest-apis-c513d2d.md "Use SAP Job Scheduling service REST APIs to create, manage, and monitor jobs and job schedules.")

