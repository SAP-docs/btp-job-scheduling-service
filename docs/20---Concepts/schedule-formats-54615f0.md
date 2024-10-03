<!-- loio54615f087cca45c48f81ce4967c6f7f3 -->

# Schedule Formats

The SAP Job Scheduling service supports several scheduling formats.

<a name="loio37af46344c4d46a9b8695d2c9775c34f"/>

<!-- loio37af46344c4d46a9b8695d2c9775c34f -->

## Cron Format

The cron format enables you to define the job run schedule.



The format is like the standard Linux cron but provides more functional flexibility for scheduling application-based jobs. The following table explains the order of fields used in the cron and lists the permitted values for each field:


<table>
<tr>
<th valign="top">

Cron field \(Left to right\)

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Year

</td>
<td valign="top">

4-digit representation for year. Example: 2015

</td>
</tr>
<tr>
<td valign="top">

Month

</td>
<td valign="top">

Numeric representation for a month. Permitted values are 1 to 12.

</td>
</tr>
<tr>
<td valign="top">

Day

</td>
<td valign="top">

Numeric representation for day of the month with values permitted from -31 to 31. Negative values are calculated from the end of the month.

</td>
</tr>
<tr>
<td valign="top">

DayOfWeek

</td>
<td valign="top">

3-letter representation for day of the week. Example: mon, tue, and so on.

</td>
</tr>
<tr>
<td valign="top">

Hour

</td>
<td valign="top">

Numeric representation for an hour. Permitted values are 0 to 23.

</td>
</tr>
<tr>
<td valign="top">

Minute

</td>
<td valign="top">

Numeric representation for a minute. Permitted values are 0 to 59.

</td>
</tr>
<tr>
<td valign="top">

Second

</td>
<td valign="top">

Numeric representation for a second. Permitted values are 0 to 59.

</td>
</tr>
</table>

The table below displays the syntax allowed to define cron expressions:


<table>
<tr>
<th valign="top">

Expression

</th>
<th valign="top">

Usage

</th>
<th valign="top">

Value

</th>
</tr>
<tr>
<td valign="top">

\*

</td>
<td valign="top">

anywhere

</td>
<td valign="top">

any value

</td>
</tr>
<tr>
<td valign="top">

\*/a

</td>
<td valign="top">

anywhere

</td>
<td valign="top">

any a-th value

</td>
</tr>
<tr>
<td valign="top">

a:b

</td>
<td valign="top">

anywhere

</td>
<td valign="top">

Values in the range a to b.

</td>
</tr>
<tr>
<td valign="top">

a:b/c

</td>
<td valign="top">

anywhere

</td>
<td valign="top">

Every c-th value between a and b.

</td>
</tr>
<tr>
<td valign="top">

a.y

</td>
<td valign="top">

Day of the week

</td>
<td valign="top">

On the a-th occurrence of the weekday y \(a = -5 to 5\)

</td>
</tr>
<tr>
<td valign="top">

a,b,c

</td>
<td valign="top">

anywhere

</td>
<td valign="top">

a or b or c

</td>
</tr>
</table>

> ### Example:  
> The table below displays the crontab expression with its description:
> 
> 
> <table>
> <tr>
> <th valign="top">
> 
> Expression
> 
> </th>
> <th valign="top">
> 
> Description
> 
> </th>
> </tr>
> <tr>
> <td valign="top">
> 
> \* \* \* 10:12 \*/30 0
> 
> </td>
> <td valign="top">
> 
> Run the schedule every day between 10:00 and 12:00, every 30 minutes. The schedule is executed at 10:00, 10:30, 11:00, 11:30, 12:00, 12:30, and the next day it starts again at 10:00.
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> 2015 \* \* fri 12 0 0
> 
> </td>
> <td valign="top">
> 
> Run the schedule every Friday in 2015 at 12:00.
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> \* \* 3:-2 \* 12:14 0 0
> 
> </td>
> <td valign="top">
> 
> Run every hour between 12:00 and 14:00 every day between the third and second-to-last day of the month.
> 
> </td>
> </tr>
> <tr>
> <td valign="top">
> 
> \* \* \* -1.sun 9 0 0
> 
> </td>
> <td valign="top">
> 
> Run the schedule on the last Sunday of every month at 09:00.
> 
> </td>
> </tr>
> </table>

<a name="loio333e7ce070c245d0bb8493cff2e3027b"/>

<!-- loio333e7ce070c245d0bb8493cff2e3027b -->

## Date and Time Format

You can provide date and time parameters such as startTime, endTime, or time for schedules as data type string or object.



## Date Object

-   For an object data type, a mandatory date field denoting the date as a string, and an optional format field denoting a date-time format for correctly parsing the user-provided date value, must be passed. The following constraints apply to object formats:

    -   If you provide only a date field, the string is checked against both IETF-compliant RFC 2822 timestamps and ISO-8601 standards.

        > ### Note:  
        > For dates that are compliant with ISO-8601, calendar dates \(example: 2013-02-08\), week dates \(example: 2013-W06-5\), ordinal dates \(example: 2013-039\), and time-based dates \(example: 2013-02-08 09+07:00\) are all supported. If the date string is of an unknown format, an error is thrown.

    -   If the format of the date string provided in the date field is customized, an optional format string can be passed. The allowed parsing tokens include the following:


        <table>
        <tr>
        <th valign="top">

        Input Token
        
        </th>
        <th valign="top">

        Example
        
        </th>
        <th valign="top">

        Description
        
        </th>
        </tr>
        <tr>
        <td valign="top">
        
        YYYY
        
        </td>
        <td valign="top">
        
        2015
        
        </td>
        <td valign="top">
        
        4-digit year
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        YY
        
        </td>
        <td valign="top">
        
        14
        
        </td>
        <td valign="top">
        
        2-digit year
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        Q
        
        </td>
        <td valign="top">
        
        1-4
        
        </td>
        <td valign="top">
        
        Quarter year. Sets month to first month of the quarter.
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        M MM
        
        </td>
        <td valign="top">
        
        1-12
        
        </td>
        <td valign="top">
        
        Month number
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        MMM MMMM
        
        </td>
        <td valign="top">
        
        January-Dec
        
        </td>
        <td valign="top">
        
        Month name in locale
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        D DD
        
        </td>
        <td valign="top">
        
        1-31
        
        </td>
        <td valign="top">
        
        Day of month
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        Do
        
        </td>
        <td valign="top">
        
        1st - 31st
        
        </td>
        <td valign="top">
        
        Day of month with ordinal
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        DDD DDDD
        
        </td>
        <td valign="top">
        
        1-365
        
        </td>
        <td valign="top">
        
        Day of year
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        X
        
        </td>
        <td valign="top">
        
        1410715640.579
        
        </td>
        <td valign="top">
        
        UNIX timestamp
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        x
        
        </td>
        <td valign="top">
        
        1410715640579
        
        </td>
        <td valign="top">
        
        UNIX timestamp \(ms\)
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        gggg
        
        </td>
        <td valign="top">
        
        2015
        
        </td>
        <td valign="top">
        
        Locale 4-digit week year
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        gg
        
        </td>
        <td valign="top">
        
        15
        
        </td>
        <td valign="top">
        
        Locale 2-digit week year
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        w ww
        
        </td>
        <td valign="top">
        
        1-53
        
        </td>
        <td valign="top">
        
        Locale week of the year
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        e
        
        </td>
        <td valign="top">
        
        1-7
        
        </td>
        <td valign="top">
        
        Locale day of the week
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        GGGG
        
        </td>
        <td valign="top">
        
        2015
        
        </td>
        <td valign="top">
        
        ISO 4-digit week year
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        GG
        
        </td>
        <td valign="top">
        
        15
        
        </td>
        <td valign="top">
        
        ISO 2-digit week year
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        W WW
        
        </td>
        <td valign="top">
        
        1-53
        
        </td>
        <td valign="top">
        
        ISO week of year
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        E
        
        </td>
        <td valign="top">
        
        1-7
        
        </td>
        <td valign="top">
        
        ISO day of week
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        H HH
        
        </td>
        <td valign="top">
        
        0-23
        
        </td>
        <td valign="top">
        
        24-hour time
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        h hh
        
        </td>
        <td valign="top">
        
        1-12
        
        </td>
        <td valign="top">
        
        12-hour time used with "a A"
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        a A
        
        </td>
        <td valign="top">
        
        am pm
        
        </td>
        <td valign="top">
        
        Before or after noon
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        m mm
        
        </td>
        <td valign="top">
        
        0-59
        
        </td>
        <td valign="top">
        
        Minutes
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        s ss
        
        </td>
        <td valign="top">
        
        0-59
        
        </td>
        <td valign="top">
        
        Seconds
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        S
        
        </td>
        <td valign="top">
        
        0-9
        
        </td>
        <td valign="top">
        
        Tenths of a second
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        SS
        
        </td>
        <td valign="top">
        
        0-99
        
        </td>
        <td valign="top">
        
        Hundredths of a second
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        SSS
        
        </td>
        <td valign="top">
        
        0-999
        
        </td>
        <td valign="top">
        
        Thousandths of a second
        
        </td>
        </tr>
        <tr>
        <td valign="top">
        
        Z ZZ
        
        </td>
        <td valign="top">
        
        \+12:00
        
        </td>
        <td valign="top">
        
        Offset from UTC as +-HH:mm, +-HHmm, or Z
        
        </td>
        </tr>
        </table>
        
        > ### Example:  
        > 
        > <table>
        > <tr>
        > <th valign="top">
        > 
        > Format
        > 
        > </th>
        > <th valign="top">
        > 
        > Description
        > 
        > </th>
        > </tr>
        > <tr>
        > <td valign="top">
        > 
        > "startTime": \{"date": "2015-10-20 04:30 +0000", "format": "YYYY-MM-DD HH:mm Z”\}
        > 
        > </td>
        > <td valign="top">
        > 
        > 4.30 UTC on 20th Oct 2015
        > 
        > </td>
        > </tr>
        > <tr>
        > <td valign="top">
        > 
        > "endTime": \{"date": "2015-W06-5"\}
        > 
        > </td>
        > <td valign="top">
        > 
        > Friday, February 06, 2015
        > 
        > </td>
        > </tr>
        > </table>





<a name="loio333e7ce070c245d0bb8493cff2e3027b__section_bzt_11s_1bb"/>

## Date String

For a string data type, the parameters must be a valid date representation in the ISO-8601 or IETF-compliant RFC 2822 format.

> ### Example:  
> 1994-11-05T08:15:30-05:00

<a name="loioa323f2d365904499a83a1b60f473bb78"/>

<!-- loioa323f2d365904499a83a1b60f473bb78 -->

## Human-Readable Date Formats

The SAP Job Scheduling service supports human-readable dates and ranges for configuring both job and task schedules.



These dates and ranges are applicable for the parameters time, repeatAt, and repeatInterval. The SAP Job Scheduling service uses an embedded English language date parser for this facility.



## Specification for Schedule Parameters

-   Time

    The string value should designate a particular timestamp for running a job schedule.

    > ### Note:  
    > If an invalid string is provided, the results can be unpredictable.

    > ### Example:  
    > -   "10 hours from now"
    > -   "20 minutes from now"
    > -   "in 2 hours"
    > -   "tomorrow at 4pm"
    > -   "next week monday at 5am"
    > -   "9pm tonight"
    > -   "3.30pm"

-   RepeatAt

    This parameter represents a convenient way to create daily timestamp-based schedules. The string should designate a particular timestamp for repeatedly running a job schedule. This follows the same pattern as the recommendations for the **time** parameter, with exception: while the text for the time parameter must denote something concrete and in the future, the repeatAt must designate a timestamp, which is valid and constant daily.

    > ### Note:  
    > If an invalid string is used, the scheduler falls back to the current timestamp and runs the schedule immediately.

    > ### Example:  
    > -   "4.40pm"
    > -   "18.40"
    > -   "6.20am"
    > -   "17.20:30"
    > 
    >     > ### Caution:  
    >     > Second-based precision may not always be accurately timed.

-   RepeatInterval

    This parameter should designate an interval for repeating the job execution.

    > ### Note:  
    > Number names to denote numeric values are not supported yet.

    > ### Example:  
    > Instead of “twenty minutes”, use “20 minutes” to denote the interval.

    Supported time-units for this parameter are "years", "months", "weeks", "days", "hours", "minutes", "seconds".

    > ### Example:  
    > -   "10 hours"
    > -   "2 days"
    > -   "5 minutes"


