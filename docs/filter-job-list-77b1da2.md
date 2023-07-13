<!-- loio77b1da2bf13c4a299e79af66ad1227d7 -->

# Filter Job List



Querying jobs can make use of the "filter" query option.

The "filter" query option currently can make use of the following settings:

\- possible properties: name, subDomain, tenantId

\- boolean operators: and, or

\- function "contains"

Examples:

a. Using query option "contains":

GET /scheduler/jobs?filter=contains\(name, 'my\_job'\)

GET /scheduler/jobs?filter=contains\(subDomain, 'my\_subdomain'\)

GET /scheduler/jobs?filter=contains\(tenantId, 'e2c896e9'\)

b. Using query option "eq":

GET /scheduler/jobs?filter=name eq 'my\_job'

GET /scheduler/jobs?filter=subDomain eq 'my\_subdomain'

GET /scheduler/jobs?filter=tenantId eq 'e2c896e9-243b-4047-bf90-d4483f537786'

c. Using combinations:

GET scheduler/jobs?filter=contains\(name, 'my\_test'\) and subDomain eq 'my\_domain' and tenantId eq 'e2c896e9-243b-4047-bf90-d4483f537786'

GET scheduler/jobs?filter=name eq 'my\_test' and subDomain eq 'my\_domain' or tenantId eq 'e2c896e9-243b-4047-bf90-d4483f537786'

> ### Note:  
> -   • Defining specific orders of processing the filter's boolean terms via brackets are currently \*NOT\* supported.
> 
>     For the order of boolean term processing, the processing logic follows the Postgres Database SQL processing logic:
> 
>     "and"-operator takes "precedence" over "or"-operator.
> 
> -   Searching for single quotes as part of a search string, you need to double any single quote in a search string \(likewise given in the OData V 4.0x specification\).
> 
>     Example:
> 
>     filter=contains\(name, ’my\_job\(’’part one’’\)’\)
> 
>     This search is looking up for this pattern in the name property’s value: my\_job\(’part one’\)
> 
> -   Beside the filter option, there is \(implemented in previous versions of the REST API\) the query option “tenantId” existing.
> 
>     If this option is specified in addition to the filter option, the filter option has precedence over that single query option.

