---
title: Synchronize agent presence status across multiple systems
description: How-to synchronize agent presence status across multiple systems.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: 
ms.date: 11/15/2024
ms.custom: bap-template 
---

# Synchronize agent presence status across multiple systems

 Presence APIs provide methods to access and update agent availability information across multiple systems. You can synchronize agents' presence status to avoid overbooking and ensure synchronization across platforms.

## Prerequisites

Before you start, make sure you have the following:

- A license for Dynamics 365 Contact Center.
- Omnichannel agent or Omnichannel Supervisor role for the agents whose presence status you want to sync.
- A third-party application that you want to integrate with, such as Teams. The application must be allowlisted in Dataverse to access APIs and entities.
- A middleware system that can pass messages between Dynamics 365 Contact Center, Dynamics 365 Customer Service and the other application.
- An agent dictionary in the middleware that maps the agents' IDs in both systems.

## Set up a webhook for agent presence changes

A webhook allows an external service to start a particular runbook in Azure Automation through a single HTTP request. To get notified of agent presence changes or new agents, you can set up a webhook for the **msdyn_agentstatus** entity, which stores the agent's status updates.

1. [Create and register a webhook](/power-apps/developer/data-platform/register-web-hook) using the plug-in registration tool.
1. [Register a step for the WebHook](/power-apps/developer/data-platform/register-web-hook#register-a-step-for-a-webhook) for updating an agent's presence status or adding a new agent with the following parameters: 
      - **Primary Entity**: msdyn_agentstatus
      - **Execution Mode**: Synchronous
      - **Deployment**: Server
   > [!NOTE]
   > If you want to capture only presence changes, we recommend that you set **Filtering attributes** to current presence to improve performance.


## Use the webhook

When the agent's presence status changes or a new agent is added in the application, the webhook sends a notification to the external service with the updated information. You can use this information to sync the agent's presence status in the other system. From the webhook response, you can get the **msdyn_agentid** for which the presence changed to **msdyn_currentpresenceid**.

By default, the out-of-the-box presence statuses mapped to the following presence id.

| Presence Status | Presence Id                          |
|-----------------|--------------------------------------|
| Available       | f523f628-c07a-e811-8162-000d3aa11f50 |
| Busy            | efdeb843-c07a-e811-8162-000d3aa11f50 |
| Busy DND        | 08971864-c07a-e811-8162-000d3aa11f50 |
| Offline         | 70139190-c07a-e811-8162-000d3aa11f50 |
| Away            | 3dacae76-c07a-e811-8162-000d3aa11f50 |

The following sections provide examples of the JSON payload for when the agent presence is modified and when a new agent is added. 


 ### [Modify agent presence](#tab/modifyagentpresence)

```json
{
   "BusinessUnitId":"a3c20b02-4e38-ef11-a315-000d3a5a54dc",
   "CorrelationId":"e1bcd028-ae87-4ca6-af27-a17ee680dbc9",
   "Depth":1,
   "InitiatingUserAgent":"Microsoft.CCaaS.AssignmentEngineVNext.AssignmentEngineVNext (DataverseSvcClient:1.1.0.11)",
   "InitiatingUserAzureActiveDirectoryObjectId":"00000000-0000-0000-0000-000000000000",
   "InitiatingUserId":"d89254ff-9438-ef11-a315-000d3a5a54dc",
   "InputParameters":[
      {
         "key":"Target",
         "value":{
            "__type":"Entity:http://schemas.microsoft.com/xrm/2011/Contracts",
            "Attributes":[
               {
                  "key":"modifiedby",
                  "value":{
                     "__type":"EntityReference:http://schemas.microsoft.com/xrm/2011/Contracts",
                     "Id":"d89254ff-9438-ef11-a315-000d3a5a54dc",
                     "KeyAttributes":[

                     ],
                     "LogicalName":"systemuser",
                     "Name":null,
                     "RowVersion":null
                  }
               },
               {
                  "key":"msdyn_isagentloggedin",
                  "value":true
               },
               {
                  "key":"msdyn_currentpresenceid",
                  "value":{
                     "__type":"EntityReference:http://schemas.microsoft.com/xrm/2011/Contracts",
                     "Id":"efdeb843-c07a-e811-8162-000d3aa11f50",
                     "KeyAttributes":[

                     ],
                     "LogicalName":"msdyn_presence",
                     "Name":null,
                     "RowVersion":null
                  }
               },
               {
                  "key":"modifiedon",
                  "value":"\/Date(1722582039000)\/"
               },
               {
                  "key":"modifiedonbehalfby",
                  "value":null
               },
               {
                  "key":"msdyn_availableunitscapacity",
                  "value":100
               },
               {
                  "key":"msdyn_agentstatusid",
                  "value":"3d1feef9-604d-ef11-bfe3-6045bd03d9d8"
               },
               {
                  "key":"msdyn_capacitymodifiedon",
                  "value":"\/Date(1722581814000)\/"
               },
               {
                  "key":"msdyn_presencemodifiedon",
                  "value":"\/Date(1722582038000)\/"
               },
               {
                  "key":"msdyn_isblockedbysomeprofile",
                  "value":false
               },
               {
                  "key":"msdyn_presencemodifiedby",
                  "value":"AGENT"
               },
               {
                  "key":"msdyn_agentid",
                  "value":{
                     "__type":"EntityReference:http://schemas.microsoft.com/xrm/2011/Contracts",
                     "Id":"97c90b02-4e38-ef11-a315-000d3a5a54dc",
                     "KeyAttributes":[

                     ],
                     "LogicalName":"systemuser",
                     "Name":null,
                     "RowVersion":null
                  }
               },
               {
                  "key":"timezoneruleversionnumber",
                  "value":4
               }
            ],
            "EntityState":null,
            "FormattedValues":[

            ],
            "Id":"3d1feef9-604d-ef11-bfe3-6045bd03d9d8",
            "KeyAttributes":[

            ],
            "LogicalName":"msdyn_agentstatus",
            "RelatedEntities":[

            ],
            "RowVersion":"5948260"
         }
      }
   ],
   "IsExecutingOffline":false,
   "IsInTransaction":false,
   "IsOfflinePlayback":false,
   "IsolationMode":1,
   "MessageName":"Update",
   "Mode":1,
   "OperationCreatedOn":"\/Date(1722582039000+0000)\/",
   "OperationId":"1a14c3ec-9c50-ef11-bfe3-00224802dbb1",
   "OrganizationId":"6042beb1-a93a-ef11-8e4b-00224802c699",
   "OrganizationName":"unq6042beb1a93aef118e4b00224802c",
   "OutputParameters":[

   ],
   "OwningExtension":{
      "Id":"8ff4bda5-9d4e-ef11-bfe3-00224802dbb1",
      "KeyAttributes":[

      ],
      "LogicalName":"sdkmessageprocessingstep",
      "Name":null,
      "RowVersion":null
   },
   "ParentContext":{
      "BusinessUnitId":"a3c20b02-4e38-ef11-a315-000d3a5a54dc",
      "CorrelationId":"e1bcd028-ae87-4ca6-af27-a17ee680dbc9",
      "Depth":1,
      "InitiatingUserAgent":"Microsoft.CCaaS.AssignmentEngineVNext.AssignmentEngineVNext (DataverseSvcClient:1.1.0.11)",
      "InitiatingUserAzureActiveDirectoryObjectId":"00000000-0000-0000-0000-000000000000",
      "InitiatingUserId":"d89254ff-9438-ef11-a315-000d3a5a54dc",
      "InputParameters":[
         {
            "key":"Target",
            "value":{
               "__type":"Entity:http://schemas.microsoft.com/xrm/2011/Contracts",
               "Attributes":[
                  {
                     "key":"msdyn_agentstatusid",
                     "value":"3d1feef9-604d-ef11-bfe3-6045bd03d9d8"
                  },
                  {
                     "key":"msdyn_availableunitscapacity",
                     "value":100
                  },
                  {
                     "key":"msdyn_currentpresenceid",
                     "value":{
                        "__type":"EntityReference:http://schemas.microsoft.com/xrm/2011/Contracts",
                        "Id":"efdeb843-c07a-e811-8162-000d3aa11f50",
                        "KeyAttributes":[

                        ],
                        "LogicalName":"msdyn_presence",
                        "Name":null,
                        "RowVersion":null
                     }
                  },
                  {
                     "key":"msdyn_capacitymodifiedon",
                     "value":"\/Date(1722581814000)\/"
                  },
                  {
                     "key":"msdyn_presencemodifiedby",
                     "value":"AGENT"
                  },
                  {
                     "key":"msdyn_presencemodifiedon",
                     "value":"\/Date(1722582038000)\/"
                  },
                  {
                     "key":"msdyn_isblockedbysomeprofile",
                     "value":false
                  },
                  {
                     "key":"msdyn_isagentloggedin",
                     "value":true
                  },
                  {
                     "key":"msdyn_agentid",
                     "value":{
                        "__type":"EntityReference:http://schemas.microsoft.com/xrm/2011/Contracts",
                        "Id":"97c90b02-4e38-ef11-a315-000d3a5a54dc",
                        "KeyAttributes":[

                        ],
                        "LogicalName":"systemuser",
                        "Name":null,
                        "RowVersion":null
                     }
                  }
               ],
               "EntityState":null,
               "FormattedValues":[

               ],
               "Id":"3d1feef9-604d-ef11-bfe3-6045bd03d9d8",
               "KeyAttributes":[

               ],
               "LogicalName":"msdyn_agentstatus",
               "RelatedEntities":[

               ],
               "RowVersion":"5948260"
            }
         }
      ],
      "IsExecutingOffline":false,
      "IsInTransaction":false,
      "IsOfflinePlayback":false,
      "IsolationMode":1,
      "MessageName":"Update",
      "Mode":1,
      "OperationCreatedOn":"\/Date(1722582039000+0000)\/",
      "OperationId":"1a14c3ec-9c50-ef11-bfe3-00224802dbb1",
      "OrganizationId":"6042beb1-a93a-ef11-8e4b-00224802c699",
      "OrganizationName":"unq6042beb1a93aef118e4b00224802c",
      "OutputParameters":[

      ],
      "OwningExtension":{
         "Id":"8ff4bda5-9d4e-ef11-bfe3-00224802dbb1",
         "KeyAttributes":[

         ],
         "LogicalName":"sdkmessageprocessingstep",
         "Name":null,
         "RowVersion":null
      },
      "ParentContext":null,
      "PostEntityImages":[

      ],
      "PreEntityImages":[

      ],
      "PrimaryEntityId":"3d1feef9-604d-ef11-bfe3-6045bd03d9d8",
      "PrimaryEntityName":"msdyn_agentstatus",
      "RequestId":"84d03007-6a8f-41da-aeae-7b6460bb7a04",
      "SecondaryEntityName":"none",
      "SharedVariables":[
         {
            "key":"IsAutoTransact",
            "value":true
         },
         {
            "key":"AcceptLang",
            "value":""
         }
      ],
      "Stage":30,
      "UserAzureActiveDirectoryObjectId":"00000000-0000-0000-0000-000000000000",
      "UserId":"d89254ff-9438-ef11-a315-000d3a5a54dc"
   },
   "PostEntityImages":[
      {
         "key":"AsynchronousStepPrimaryName",
         "value":{
            "Attributes":[
               {
                  "key":"msdyn_agentstatusid",
                  "value":"3d1feef9-604d-ef11-bfe3-6045bd03d9d8"
               }
            ],
            "EntityState":null,
            "FormattedValues":[

            ],
            "Id":"3d1feef9-604d-ef11-bfe3-6045bd03d9d8",
            "KeyAttributes":[

            ],
            "LogicalName":"msdyn_agentstatus",
            "RelatedEntities":[

            ],
            "RowVersion":null
         }
      }
   ],
   "PreEntityImages":[

   ],
   "PrimaryEntityId":"3d1feef9-604d-ef11-bfe3-6045bd03d9d8",
   "PrimaryEntityName":"msdyn_agentstatus",
   "RequestId":"84d03007-6a8f-41da-aeae-7b6460bb7a04",
   "SecondaryEntityName":"none",
   "SharedVariables":[
      {
         "key":"IsAutoTransact",
         "value":true
      },
      {
         "key":"AcceptLang",
         "value":""
      }
   ],
   "Stage":40,
   "UserAzureActiveDirectoryObjectId":"00000000-0000-0000-0000-000000000000",
   "UserId":"d89254ff-9438-ef11-a315-000d3a5a54dc"
}

```

 ### [Add new agent](#tab/addnewagent)

```json
{
  "BusinessUnitId":"e95e91cf-7b10-ef11-9f8a-6045bdd4c6be",
    "CorrelationId":"58dc9af0-fe25-4f81-b3f3-c4cb147c2ec4",
    "Depth":1,
    "InitiatingUserAgent":"",
    "InitiatingUserAzureActiveDirectoryObjectId":"00000000-0000-0000-0000-000000000000",
    "InitiatingUserId":"09eb2446-db10-ef11-9f8a-6045bdd4c6be",
    "InputParameters":[
      {
         "key":"Target",
         "value":{
            "__type":"Entity:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
            "Attributes":[
               {
                  "key":"msdyn_capacitymodifiedon",
                  "value":"\/Date(1721809601000)\/"
               },
               {
                  "key":"msdyn_agentstatusid",
                  "value":"4b1e3d75-a749-ef11-acce-00224802d26d"
               },
               {
                  "key":"owningbusinessunit",
                  "value":{
                     "__type":"EntityReference:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                     "Id":"e95e91cf-7b10-ef11-9f8a-6045bdd4c6be",
                     "KeyAttributes":[
                        
                     ],
                     "LogicalName":"businessunit",
                     "Name":null,
                     "RowVersion":null
                  }
               },
               {
                  "key":"modifiedon",
                  "value":"\/Date(1721816905000)\/"
               },
               {
                  "key":"modifiedonbehalfby",
                  "value":null
               },
               {
                  "key":"msdyn_presencemodifiedby",
                  "value":"SYSTEM"
               },
               {
                  "key":"msdyn_currentpresenceid",
                  "value":{
                     "__type":"EntityReference:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                     "Id":"70139190-c07a-e811-8162-000d3aa11f50",
                     "KeyAttributes":[
                        
                     ],
                     "LogicalName":"msdyn_presence",
                     "Name":null,
                     "RowVersion":null
                  }
               },
               {
                  "key":"msdyn_presencemodifiedon",
                  "value":"\/Date(1721816904000)\/"
               },
               {
                  "key":"statecode",
                  "value":{
                     "__type":"OptionSetValue:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                     "Value":0
                  }
               },
               {
                  "key":"statuscode",
                  "value":{
                     "__type":"OptionSetValue:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                     "Value":1
                  }
               },
               {
                  "key":"msdyn_isagentloggedin",
                  "value":false
               },
               {
                  "key":"createdby",
                  "value":{
                     "__type":"EntityReference:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                     "Id":"09eb2446-db10-ef11-9f8a-6045bdd4c6be",
                     "KeyAttributes":[
                        
                     ],
                     "LogicalName":"systemuser",
                     "Name":null,
                     "RowVersion":null
                  }
               },
               {
                  "key":"timezoneruleversionnumber",
                  "value":4
               },
               {
                  "key":"msdyn_agentid",
                  "value":{
                     "__type":"EntityReference:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                     "Id":"a7f9a9ed-b311-ef11-9f89-000d3a544b4c",
                     "KeyAttributes":[
                        
                     ],
                     "LogicalName":"systemuser",
                     "Name":null,
                     "RowVersion":null
                  }
               },
               {
                  "key":"ownerid",
                  "value":{
                     "__type":"EntityReference:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                     "Id":"09eb2446-db10-ef11-9f8a-6045bdd4c6be",
                     "KeyAttributes":[
                        
                     ],
                     "LogicalName":"systemuser",
                     "Name":null,
                     "RowVersion":null
                  }
               },
               {
                  "key":"msdyn_availableunitscapacity",
                  "value":100
               },
               {
                  "key":"msdyn_isblockedbysomeprofile",
                  "value":false
               },
               {
                  "key":"owninguser",
                  "value":{
                     "__type":"EntityReference:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                     "Id":"09eb2446-db10-ef11-9f8a-6045bdd4c6be",
                     "KeyAttributes":[
                        
                     ],
                     "LogicalName":"systemuser",
                     "Name":null,
                     "RowVersion":null
                  }
               },
               {
                  "key":"modifiedby",
                  "value":{
                     "__type":"EntityReference:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                     "Id":"09eb2446-db10-ef11-9f8a-6045bdd4c6be",
                     "KeyAttributes":[
                        
                     ],
                     "LogicalName":"systemuser",
                     "Name":null,
                     "RowVersion":null
                  }
               },
               {
                  "key":"createdon",
                  "value":"\/Date(1721816905000)\/"
               }
            ],
            "EntityState":null,
            "FormattedValues":[
               {
                  "key":"msdyn_capacitymodifiedon",
                  "value":"2024-07-24T08:26:41-00:00"
               },
               {
                  "key":"modifiedon",
                  "value":"2024-07-24T10:28:25-00:00"
               },
               {
                  "key":"msdyn_presencemodifiedon",
                  "value":"2024-07-24T10:28:24-00:00"
               },
               {
                  "key":"statecode",
                  "value":"Active"
               },
               {
                  "key":"statuscode",
                  "value":"Active"
               },
               {
                  "key":"msdyn_isagentloggedin",
                  "value":"No"
               },
               {
                  "key":"timezoneruleversionnumber",
                  "value":"4"
               },
               {
                  "key":"msdyn_availableunitscapacity",
                  "value":"100"
               },
               {
                  "key":"msdyn_isblockedbysomeprofile",
                  "value":"No"
               },
               {
                  "key":"createdon",
                  "value":"2024-07-24T10:28:25-00:00"
               }
            ],
            "Id":"4b1e3d75-a749-ef11-acce-00224802d26d",
            "KeyAttributes":[
               
            ],
            "LogicalName":"msdyn_agentstatus",
            "RelatedEntities":[
               
            ],
            "RowVersion":null
         }
      }
   ],
   "IsExecutingOffline":false,
   "IsInTransaction":true,
   "IsOfflinePlayback":false,
   "IsolationMode":1,
   "MessageName":"Create",
   "Mode":0,
   "OperationCreatedOn":"\/Date(1721816905786)\/",
   "OperationId":"09097f27-6123-4c61-b463-af00adb2e082",
   "OrganizationId":"c09254de-a911-ef11-9f83-000d3a9d3b76",
   "OrganizationName":"unqc09254dea911ef119f83000d3a9d3",
   "OutputParameters":[
      {
         "key":"id",
         "value":"4b1e3d75-a749-ef11-acce-00224802d26d"
      }
   ],
   "OwningExtension":{
      "Id":"58378ec8-a649-ef11-acce-6045bd03d9d8",
      "KeyAttributes":[
         
      ],
      "LogicalName":"sdkmessageprocessingstep",
      "Name":"Bhanu_Update: Create of msdyn_agentstatus",
      "RowVersion":null
   },
   "ParentContext":{
      "BusinessUnitId":"e95e91cf-7b10-ef11-9f8a-6045bdd4c6be",
      "CorrelationId":"58dc9af0-fe25-4f81-b3f3-c4cb147c2ec4",
      "Depth":1,
      "InitiatingUserAgent":"",
      "InitiatingUserAzureActiveDirectoryObjectId":"00000000-0000-0000-0000-000000000000",
      "InitiatingUserId":"09eb2446-db10-ef11-9f8a-6045bdd4c6be",
      "InputParameters":[
         {
            "key":"Target",
            "value":{
               "__type":"Entity:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
               "Attributes":[
                  {
                     "key":"msdyn_agentid",
                     "value":{
                        "__type":"EntityReference:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                        "Id":"a7f9a9ed-b311-ef11-9f89-000d3a544b4c",
                        "KeyAttributes":[
                           
                        ],
                        "LogicalName":"systemuser",
                        "Name":null,
                        "RowVersion":null
                     }
                  },
                  {
                     "key":"msdyn_currentpresenceid",
                     "value":{
                        "__type":"EntityReference:http:\/\/schemas.microsoft.com\/xrm\/2011\/Contracts",
                        "Id":"70139190-c07a-e811-8162-000d3aa11f50",
                        "KeyAttributes":[
                           
                        ],
                        "LogicalName":"msdyn_presence",
                        "Name":null,
                        "RowVersion":null
                     }
                  },
                  {
                     "key":"msdyn_availableunitscapacity",
                     "value":100
                  },
                  {
                     "key":"msdyn_capacitymodifiedon",
                     "value":"\/Date(1721809601096+0000)\/"
                  },
                  {
                     "key":"msdyn_presencemodifiedby",
                     "value":"SYSTEM"
                  },
                  {
                     "key":"msdyn_presencemodifiedon",
                     "value":"\/Date(1721816904678)\/"
                  },
                  {
                     "key":"msdyn_isblockedbysomeprofile",
                     "value":false
                  },
                  {
                     "key":"msdyn_isagentloggedin",
                     "value":false
                  },
                  {
                     "key":"msdyn_agentstatusid",
                     "value":"4b1e3d75-a749-ef11-acce-00224802d26d"
                  }
               ],
               "EntityState":null,
               "FormattedValues":[
                  
               ],
               "Id":"4b1e3d75-a749-ef11-acce-00224802d26d",
               "KeyAttributes":[
                  
               ],
               "LogicalName":"msdyn_agentstatus",
               "RelatedEntities":[
                  
               ],
               "RowVersion":null
            }
         }
      ],
      "IsExecutingOffline":false,
      "IsInTransaction":true,
      "IsOfflinePlayback":false,
      "IsolationMode":1,
      "MessageName":"Create",
      "Mode":0,
      "OperationCreatedOn":"\/Date(1721816905739)\/",
      "OperationId":"09097f27-6123-4c61-b463-af00adb2e082",
      "OrganizationId":"c09254de-a911-ef11-9f83-000d3a9d3b76",
      "OrganizationName":"unqc09254dea911ef119f83000d3a9d3",
      "OutputParameters":[
         
      ],
      "OwningExtension":{
         "Id":"b7a297bf-d810-ef11-9f8a-6045bdd4c6be",
         "KeyAttributes":[
            
         ],
         "LogicalName":"sdkmessageprocessingstep",
         "Name":"ObjectModel Implementation",
         "RowVersion":null
      },
      "ParentContext":null,
      "PostEntityImages":[
         
      ],
      "PreEntityImages":[
         
      ],
      "PrimaryEntityId":"4b1e3d75-a749-ef11-acce-00224802d26d",
      "PrimaryEntityName":"msdyn_agentstatus",
      "RequestId":"09097f27-6123-4c61-b463-af00adb2e082",
      "SecondaryEntityName":"none",
      "SharedVariables":[
         {
            "key":"IsAutoTransact",
            "value":true
         },
         {
            "key":"AcceptLang",
            "value":""
         },
         {
            "key":"DefaultsAddedFlag",
            "value":true
         }
      ],
      "Stage":30,
      "UserAzureActiveDirectoryObjectId":"00000000-0000-0000-0000-000000000000",
      "UserId":"09eb2446-db10-ef11-9f8a-6045bdd4c6be"
   },
   "PostEntityImages":[
      
   ],
   "PreEntityImages":[
      
   ],
   "PrimaryEntityId":"4b1e3d75-a749-ef11-acce-00224802d26d",
   "PrimaryEntityName":"msdyn_agentstatus",
   "RequestId":"09097f27-6123-4c61-b463-af00adb2e082",
   "SecondaryEntityName":"none",
   "SharedVariables":[
      {
         "key":"IsAutoTransact",
         "value":true
      },
      {
         "key":"AcceptLang",
         "value":""
      },
      {
         "key":"DefaultsAddedFlag",
         "value":true
      }
   ],
   "Stage":40,
   "UserAzureActiveDirectoryObjectId":"00000000-0000-0000-0000-000000000000",
   "UserId":"09eb2446-db10-ef11-9f8a-6045bdd4c6be"
}

```
---

## Use APIs to get or modify presence status

 You can use custom APIs to get or modify the agent's presence status. Do the following steps to use these APIs:

1. Generate tokens using in certificate based authentication using your application ID. Learn more in [Use OAuth authentication with Microsoft Dataverse](/power-apps/developer/data-platform/authenticate-oauth).
1. Assign impersonation privileges to the application. Learn more in [Impersonate another user using the Web API](/power-apps/developer/data-platform/webapi/impersonate-another-user-web-api).
1. Perform the required API calls as follows:
     - [CCaaS_GetPresence](api/ccaas_getpresence.md) to get the agent's presence status.
     - [CCaaS_ModifyAgentPresence](api/ccaas_modifyagentpresence.md) to update the agent's presence status.
     