<!-- loio7b3f01449dd14529b902711dffb17cfa -->

# Best Practices

Learn best practices to optimize the way you use the SAP Job Scheduling service before delving into more specific topics.



<a name="loio7b3f01449dd14529b902711dffb17cfa__section_v33_zrt_lgc"/>

## Scheduling Time

When you use the SAP Job Scheduling service, schedule your executions efficiently to minimize delays and keep operations running smoothly. The service lets you execute jobs or tasks at any time during a 24-hour period. To optimize performance and reduce potential start delays, follow these recommendations:



### Avoid Peak Seconds

Do not schedule jobs or tasks to start at the 0th or 30th second of any minute \(for example, 00:00:00, 00:00:30, 00:01:00\). Instead, use less common seconds such as 01:12:17, 01:38:37, or 01:52:53.



### Avoid Peak Minutes

Some times within an hour are more likely to experience delays due to high demand. Specifically:

-   Do not schedule jobs or tasks to start at the 0th or 30th minute of any hour \(for example, 00:00, 00:30, 1:00\). Many schedules initiate at these times.

-   Avoid scheduling jobs or tasks at multiples of five minutes within any hour \(for example, 00:05, 00:10, 00:15\). These times are also frequently requested, though not as busy as the 0th or 30th minute.




### Avoid the Top of the Hour

The start of each hour is often particularly busy, which increases the likelihood of delays. Avoid scheduling at the top of the hour \(for example, 00:00, 01:00, 02:00\). Midnight \(12:00 a.m. UTC\) is usually the busiest time due to daily updates and overnight jobs. Do not schedule jobs during this period.



<a name="loio7b3f01449dd14529b902711dffb17cfa__section_ylx_l5t_lgc"/>

## One-Time Schedules

Use one-time schedules for testing and validation. For repeating schedules, use other types such as cron.



<a name="loio7b3f01449dd14529b902711dffb17cfa__section_gbh_45t_lgc"/>

## Run Log Update

For long-running asynchronous executions, send a 202 Accepted response. Then call the Update Run Logs REST endpoint of the SAP Job Scheduling service. Send only one request that includes all execution logs and the status of the execution.

