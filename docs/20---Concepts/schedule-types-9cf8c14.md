<!-- loio9cf8c14da0144c84aac628dc56b00ffd -->

# Schedule Types

SAP Job Scheduling service runs one-time and recurring jobs or Cloud Foundry tasks.



<a name="loio9cf8c14da0144c84aac628dc56b00ffd__section_wr3_p3p_d4b"/>

## **One-Time Schedules**

Schedules that run only once. You can create one-time schedules using any one of the following options:

-   **Human-readable text:** A human-readable text, denoting the specified execution time. For more information see, [Human-Readable Date Formats](schedule-formats-54615f0.md#loioa323f2d365904499a83a1b60f473bb78).

    > ### Example:  
    > 10 hours from now, 3.30pm
    > 
    > Friday at 2am

-   **Date String Formats :**

    A valid date representations in the ISO-8601 or IETF-compliant RFC 2822 format.

    > ### Example:  
    > 1994-11-05T08:15:30-05:00




<a name="loio9cf8c14da0144c84aac628dc56b00ffd__section_fsb_5hp_d4b"/>

## Recurring Schedules

Schedules that run periodically at specified times, dates, or intervals. You can create recurring schedules using any one of the following options:

-   **repeatInterval:** Denotes the interval between schedules in a human-readable text format \(for example, 5 minutes\).

    The next execution is based on the start time of the previous execution. If the start is delayed for some reason, the next executions are also affected.

    > ### Example:  
    > A schedule is planned to start at 10.00am with a `repeatInterval` of 1 hour. The start is delayed and executed at 10.02am. As a result, the start time of the next executions changes to 11.02am, 12.02pm, 13.02pm, and so on.

    If a job runs longer than expected, the next job starts on time as scheduled.

    > ### Example:  
    > Let's assume that you have a recurring schedule with a `repeatInterval` of 5 minutes and the first job starts at 6.00pm, the second job starts at 6.05pm., and so on. If the first job ends at 6.07pm, the second job is still going to start at 6.05pm as planned.

    For more information, see [Human-Readable Date Formats](schedule-formats-54615f0.md#loioa323f2d365904499a83a1b60f473bb78).

    > ### Example:  
    > -   "10 hours"
    > -   "2 days"
    > -   "5 minutes"

    > ### Note:  
    > The SAP Job Scheduling service assumes that all months are 30 days long and a year consists of 365 days. If you need a job to run on the same day every month or every few months, you can use the cron format.

-   **cron:** Denotes a crontab expression, which represents a set of times, that determines when the job is executed.

    For more information, see [Cron Format](schedule-formats-54615f0.md#loio37af46344c4d46a9b8695d2c9775c34f).

-   **repeatAt:** Denotes an exact time, every day, when a job is executed. This field can be specified using Human-Readable Time Format and Date String Formats \(ISO-8601 or IETF-compliant RFC-2822\).

    > ### Example:  
    > "4.40pm"
    > 
    > "18.40"
    > 
    > "6.20am"


**Related Information**  


[Schedule Lifecycle](schedule-lifecycle-e1805f2.md "A schedule passes through three lifecycle states for each run.")

[Service Behavior](../40---Using-JOB-SCHDULR-TITLE/service-behavior-d09664b.md#loiod09664b7ae9d453e8b8a3a6e09449916 "This topic helps you understand and analyze the behavior of the SAP Job Scheduling service under specific situations.")

