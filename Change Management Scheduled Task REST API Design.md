Change Management Scheduled Task REST API Design
================================================

Change Management Scheduled Task Introduction:

-   Scheduled Task Status List: Waiting/Running/Executed

-   Scheduler is the requestor user name.

-   Scheduled Task can only be added to an APPROVED Network Change.

-   Scheduled Task : Network Change is 1 : 1.

-   Running/Executed Scheduled Task cannot be updated/deleted.

POST /V1/CMDB/CM/Tasks/ScheduledTask
------------------------------------

Call this API to create a Scheduled Task (ST) for an APPROVED Network Change
(NC).

Note:

-   Only 1 ST can be created on each NC. If there is an existing ST, create
    request is not allowed.

-   ST can only be added to APPROVED NC, so that ST is restricted to be created
    on unapproved NC.

-   APPROVED NC with executed ST doesn’t allow ST creation request.

-   Follow NetBrain system user privileges

Detail Information
------------------

\| Title: Change Management Scheduled Task API

\| Version: 09/30/2019

\| API Server URL: http(s)://IP Address of NetBrain Web API
Server/ServicesAPI/API/V1/CMDB/CM/Tasks/ScheduledTask

\| Authentication:

| **Type**              | **In**  | **Name**             |
|-----------------------|---------|----------------------|
| Bearer Authentication | Headers | Authentication token |

Request body (\*required)
-------------------------

| **Name**               | **Type** | **Description** |
|------------------------|----------|-----------------|
| network_change\*       | string   | Name of NC      |
| execution_time\*       | date     | ST start time   |
| do_not_execute_after\* | date     | ST end time     |

Query Parameters (\*required)
-----------------------------

\| No parameters required.

Headers
-------

\| Data Format Headers

| **Name**     | **Type** | **Description**            |
|--------------|----------|----------------------------|
| Content-Type | String   | Support “application/json” |
| Accept       | String   | Support “application/json” |

\| Authorization Headers

| **Name** | **Type** | **Description**                           |
|----------|----------|-------------------------------------------|
| Token    | String   | Authentication token, get from login API. |

Response
--------

| **Name**              | **Type** | **Description**                                |
|-----------------------|----------|------------------------------------------------|
| network_change        | String   | Name of NC                                     |
| scheduled_task_id     | String   | ID of the created scheduled task               |
| scheduler             | String   | User name of the scheduler                     |
| scheduled_task_status | String   | Status of the created scheduled task           |
| statusCode            | Integer  | The returned status code of executing the API. |
| statusDescription     | String   | The explanation of the status code.            |

\| *Example*

GET /V1/CMDB/CM/Tasks/ScheduledTask
-----------------------------------

Call this API to get a Scheduled Task (ST) of an APPROVED Network Change (NC).

Note:

-   ST can only be added to APPROVED NC, so that unapproved NC doesn’t have an
    ST. Return NC status and error message in response.

-   Follow NetBrain system user privileges

Detail Information
------------------

\| Title: Change Management Scheduled Task API

\| Version: 09/30/2019

\| API Server URL: http(s)://IP Address of NetBrain Web API
Server/ServicesAPI/API/V1/CMDB/CM/Tasks/ScheduledTask

\| Authentication:

| **Type**              | **In**  | **Name**             |
|-----------------------|---------|----------------------|
| Bearer Authentication | Headers | Authentication token |

Request body (\*required)
-------------------------

\| No parameters required.

Query Parameters (\*required)
-----------------------------

| **Name**             | **Type** | **Description**            |
|----------------------|----------|----------------------------|
| network_change       | string   | Name of NC                 |
| status               | String   | Status of scheduled task   |
| scheduler            | String   | User name of the scheduler |
| execution_time       | date     | ST start time              |
| do_not_execute_after | date     | ST end time                |
| last_activity_date   | date     | ST execution end time      |

Headers
-------

\| Data Format Headers

| **Name**     | **Type** | **Description**            |
|--------------|----------|----------------------------|
| Content-Type | String   | Support “application/json” |
| Accept       | String   | Support “application/json” |

\| Authorization Headers

| **Name** | **Type** | **Description**                           |
|----------|----------|-------------------------------------------|
| Token    | String   | Authentication token, get from login API. |

Response
--------

| **Name**              | **Type** | **Description**                                |
|-----------------------|----------|------------------------------------------------|
| network_change        | String   | Name of NC                                     |
| scheduled_task_id     | String   | ID of the created scheduled task               |
| scheduler             | String   | User name of the scheduler                     |
| scheduled_task_status | String   | Status of the created scheduled task           |
| execution_time        | date     | ST start time                                  |
| do_not_execute_after  | date     | ST end time                                    |
| last_activity_date    | date     | ST execution end time                          |
| status                | String   | Status of scheduled task                       |
| statusCode            | Integer  | The returned status code of executing the API. |
| statusDescription     | String   | The explanation of the status code.            |

\| *Example*

PUT /V1/CMDB/CM/Tasks/ScheduledTask
-----------------------------------

Call this API to update a Scheduled Task (ST) of an APPROVED Network Change
(NC).

Note:

-   Use PUT method to update an ST that is on “Waiting” status.

-   If an ST is on “Running” or “Executed” status, update request is not
    allowed.

-   Follow NetBrain system user privileges

Detail Information
------------------

\| Title: Change Management Scheduled Task API

\| Version: 09/30/2019

\| API Server URL: http(s)://IP Address of NetBrain Web API
Server/ServicesAPI/API/V1/CMDB/CM/Tasks/ScheduledTask

\| Authentication:

| **Type**              | **In**  | **Name**             |
|-----------------------|---------|----------------------|
| Bearer Authentication | Headers | Authentication token |

Request body (\*required)
-------------------------

| **Name**               | **Type** | **Description** |
|------------------------|----------|-----------------|
| network_change\*       | string   | Name of NC      |
| execution_time\*       | date     | ST start time   |
| do_not_execute_after\* | date     | ST end time     |

Query Parameters (\*required)
-----------------------------

\| No parameters required.

Headers
-------

\| Data Format Headers

| **Name**     | **Type** | **Description**            |
|--------------|----------|----------------------------|
| Content-Type | String   | Support “application/json” |
| Accept       | String   | Support “application/json” |

\| Authorization Headers

| **Name** | **Type** | **Description**                           |
|----------|----------|-------------------------------------------|
| Token    | String   | Authentication token, get from login API. |

Response
--------

| **Name**              | **Type** | **Description**                                |
|-----------------------|----------|------------------------------------------------|
| network_change        | String   | Name of NC                                     |
| scheduled_task_id     | String   | ID of the created scheduled task               |
| scheduler             | String   | User name of the scheduler                     |
| scheduled_task_status | String   | Status of the created scheduled task           |
| statusCode            | Integer  | The returned status code of executing the API. |
| statusDescription     | String   | The explanation of the status code.            |

\| *Example*

DELETE /V1/CMDB/CM/Tasks/ScheduledTask
--------------------------------------

Call this API to delete a “Waiting” status Scheduled Task (ST) of an APPROVED
Network Change (NC).

Note:

-   ST on “Running” or “Executed” status cannot be deleted.

-   Follow NetBrain system user privileges

-   Stop a “Running” task?

Detail Information
------------------

\| Title: Change Management Scheduled Task API

\| Version: 09/30/2019

\| API Server URL: http(s)://IP Address of NetBrain Web API
Server/ServicesAPI/API/V1/CMDB/CM/Tasks/ScheduledTask

\| Authentication:

| **Type**              | **In**  | **Name**             |
|-----------------------|---------|----------------------|
| Bearer Authentication | Headers | Authentication token |

Request body (\*required)
-------------------------

\| No parameters required.

Query Parameters (\*required)
-----------------------------

| **Name**         | **Type** | **Description** |
|------------------|----------|-----------------|
| network_change\* | string   | Name of NC      |

Headers
-------

\| Data Format Headers

| **Name**     | **Type** | **Description**            |
|--------------|----------|----------------------------|
| Content-Type | String   | Support “application/json” |
| Accept       | String   | Support “application/json” |

\| Authorization Headers

| **Name** | **Type** | **Description**                           |
|----------|----------|-------------------------------------------|
| Token    | String   | Authentication token, get from login API. |

Response
--------

| **Name**          | **Type** | **Description**                                |
|-------------------|----------|------------------------------------------------|
| statusCode        | Integer  | The returned status code of executing the API. |
| statusDescription | String   | The explanation of the status code.            |

\| *Example*
