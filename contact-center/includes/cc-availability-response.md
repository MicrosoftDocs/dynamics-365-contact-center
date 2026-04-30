If successful, this method returns a 200 OK response code. The method also returns the following status codes.

| **HTTP Status** | **Description**                      |
|-----------------|--------------------------------------|
| 400             | Bad Request (Wrong input parameters) |
| 401             | Unauthorized                         |
| 404             | Resource not found                   |
| 429             | Rate limit (Too many requests)       |
| 405             | API not allowed                      |
| 500             | Internal Server Error                |

### Response values

| **Name** | **Type** | **Description** |
|---|---|---|
| queueId | String | The target queue where the request is routed based on routing rule configurations and input data such as entity values and context that are part of the routing rule. |
| isQueueAvailable | Boolean | Displays TRUE if the queue is within operating hours. FALSE if the queue is outside operating hours. |
| StartTimeOfNextOperatingHour | DateTime | The start time (UTC) of operating hours for the queue if it’s currently outside operating hours. Returns 01-01-0001 during operating hours. |
| EndTimeOfNextOperatingHour | DateTime | The time (UTC) when operating hours end for the queue, if it’s currently outside operating hours. Returns 01-01-0001 during operating hours. |
| nexttransitiontime | DateTime | The time (UTC) when the queue is operational again if it's outside operating hours. During operating hours, displays when the queue becomes non-operational. |
| positionInQueue | Number | Position in queue for a customer waiting behind others in the same queue. |
| isAgentAvailable | Boolean | Displays: <ul><li>TRUE if service representatives in the queue are currently available to take requests based on the routing and assignment rules for workstream.</li><li>FALSE if service representatives aren't available to take requests. </li></ul>|
| averageWaitTime | Number | Average wait time in minutes for customers in the target queue. |
| AverageWaitTimeInSeconds | Numbers | Average wait time in seconds for customers in the target queue. |
|NumberOfExpertsAvailableInQueue|Numbers|The number of service representatives currently available to accept conversations in the target queue. |

### Sample response 

```JSON
{  
"@odata.context": "https://<org-url>/api/data/v9.2/\$metadata#Microsoft.Dynamics.CRM.CCaaS_GetRepresentativeAvailabilityForConversationResponse",  
"NextTransitionTime": "9999-12-31T23:59:59Z",
"NumberOfExpertsAvailableInQueue": 5,
"AverageWaitTimeInSeconds": 45  
"PositionInQueue": 1,  
"AverageWaitTime": null,  
"StartTimeOfNextOperatingHour": "0001-01-01T00:00:00Z",  
"EndTimeOfNextOperatingHour": "0001-01-01T00:00:00Z",  
"QueueId": "85e55877-f27a-e911-a81a-000d3a1ca610",  
"IsAgentAvailable": true,  
"IsQueueAvailable": true  
}
```