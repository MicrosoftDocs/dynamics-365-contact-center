---
title: Use CCaaS_CreateProactiveVoiceDelivery API
description: Learn about the CCaaS_CreateProactiveVoiceDelivery API, which enables organizations to initiate proactive outbound voice calls to customers.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: reference
ms.date: 06/02/2025
ms.collection: 
ms.custom: bap-template 
---

# Use CCaaS_CreateProactiveVoiceDelivery API

You can use the `CCaaS_CreateProactiveVoiceDelivery` API to initiate proactive outbound voice calls to customers or allow customers to schedule callbacks through the Proactive Engagement Service.

> [!IMPORTANT]
> If an organization is using the `CCaaS_CreateProactiveVoiceDelivery` API to initiate an outbound voice call, the organization is responsible for consent management, including the manual updating of "do not call lists" for setting quiet hours for customer contact. Make sure that the following conditions are met:
> - Proper consent is obtained before contacting customers
> - Customers are contacted during permitted hours only.

## Prerequisites

- You must have the Omnichannel Agent or Omnichannel Supervisor role to call this API.
- Proactive engagement is configured. Learn more in [Configure proactive engagement (preview)](../../administer/configure-proactive-engagement.md).

## Initiate proactive outbound calls

Proactive engagement enables organizations to enhance customer interactions by initiating outbound communications through the voice channel. You can configure proactive engagement using a Customer Insights journey or the `CCaaS_CreateProactiveVoiceDelivery`.

 The `CCaaS_CreateProactiveVoiceDelivery` API enables organizations to initiate proactive outbound voice calls to customers through the Proactive Engagement Service. The API triggers outbound voice calls through the Voice Runtime system. Calls are placed according to the configured dial mode either immediately (if no time windows are specified) or during the designated time windows you provide.

This API allows contact centers to reach out to customers at the right time with relevant information, reminders, or notifications, enhancing customer experience while optimizing operational efficiency.

### Request Details

- **URL**: `https://<orgurl>/api/data/v9.2/CCaaS_CreateProactiveVoiceDelivery`
- **Method**: POST
- **Version**: 1.0
- **OData Operation**: Action
- **OData Type**: Unbounded
- **Request Authorization**: Required. Must contain a valid Azure AD Bearer token for the user making the API call. This token must be issued from the same Azure AD tenant as the Customer Service instance.

### Request headers

| Key                          | Type                              | Description                                                                                                                                                                                                 |
|------------------------------|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ApiVersion                   | String                           | The CCaaS API version.                                                                                                                                                                         |
| ProactiveEngagementConfigId  | String                           | Id of the Proactive Engagement Configuration to use. This specifies dial mode type, workstream, and outbound profile to use. To get this ID, do the following: <ol><li> Go to [Power Apps](https://make.preview.powerapps.com) and select the required environment.</li><li> Select **Tables** > **Proactive Engagement Configuration**</li><li> Select the ID of the required record.</li></ul>       |
| DestinationPhoneNumber       | String                           | Phone number of the customer to call.|
| ContactId                    | String                           |  Id of the customer contact in Dynamics CRM.|
| Windows                      | JSON array of Window objects     | Specifies the valid time periods when the outbound call may be placed. If not provided, the system defaults to a 24-hour window starting immediately (from current time until 24 hours later).                           |
| InputAttributes              | JSON object of key-value strings | Optional. Variables that can be referenced within Copilot agent flows to customize behavior, drive conditional logic, or retrieve personalized information from Dataverse records. |

### Windows object

| Key   | Type   | Description                                                                                   |
|-------|--------|-----------------------------------------------------------------------------------------------|
| Start | String | The beginning timestamp for this window. Must be specified in UTC in the `yyyy-MM-ddTHH:mm:ss.fffZ` format.           |
| End   | String | The end timestamp for this window. Must be specified in UTC in the `yyyy-MM-ddTHH:mm:ss.fffZ` format.                |


### Sample request

```

{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "cbbac510-3e66-ef11-a671-6045bd03d9d8",
  "DestinationPhoneNumber": "+123456798",
  "ContactId": "761e062f-c734-ef11-8e4f-00224808a166",
  "Windows": [
    {
      "Start": "2024-09-10T13:00:00.000Z",
      "End": "2024-09-10T15:59:59.999Z"
    },
    {
      "Start": "2024-09-11T13:00:00.000Z",
      "End": "2024-09-11T15:59:59.999Z"
    }
  ],
  "InputAttributes": {
    "orderNumber": "ORD123456789",
    "type": "callback",
    "isFinalAttempt": "false"
  }
}

```

### Response details

If successful, this method returns `DeliveryId`. Delivery ID is a unique identifier assigned to each proactive engagement request that is accepted through the API and is stored in the msdyn_proactive_delivery table.

The sample response is as follows:

```

{
	"@odata.context": "[Organization URI]api/data/v9.2/$metadata#Microsoft.Dynamics.CRM.CCaaS_CreateProactiveVoiceDeliveryResponse",
	"DeliveryId": "9838deee-0b4e-4116-bf73-ecb80474568d"
}

``` 

## Schedule callbacks from any platform

You can use the Proactive Engagement solution to schedule callbacks from various platforms including web, mobile applications, voice and chat agents. You can do this in the following ways:

- Create a Power Automate flow from the Copilot Studio agent.
- Integrate the schedule callback API with your website.


### Create a Power Automate flow from the Copilot agent

You can create a Power Automate flow from the Copilot agent to schedule callbacks. Perform the following steps:

1. Do the steps in [Create a flow you can use with an agent](/microsoft-copilot-studio/advanced-flow-create#create-a-flow-you-can-use-with-an-agent) with the following parameters:
  - Specify **Perform an unbound action** as the action.
  - Select **CCaaS_CreateProactiveVoiceDelivery** as the **Action Name**.
  - In **Advanced parameters**, specify the following mandatory fields:
      - **Item/DestinationPhoneNumber**: Phone number of the customer to call.
      - **Item/ProactiveEngagementConfigId**: Id of the proactive engagement configuration to use. This indicates the dial mode type, workstream, and outbound profile to use when contacting the customer. You can copy this ID from Power Apps > **Tables** > **Proactive Engagement Configuration** table.
      - **Item/ApiVersion**: 1.0
      - **Item/ContactId**: Id of the customer contact in Dynamics CRM.
      - Optionally, you can specify **Item/InputAttributes**. This field should contain a JSON object which is used by the Copilot agent. For example, `{ "msdyn_CaseTitle" : "Vitre cassée", "msdyn_CustomerName" : "Sarah", "msdyn_CustomerPhone" : "+1234567890", "msdyn_CustomerId" : "cfaa617b-2fc1-ef11-b8e8-000d3a5bcd16" }`.

### Use the API to schedule callbacks

Integrate the `CCaaS_CreateProactiveVoiceDelivery` API with your website to allow customers to request assistance at times most convenient for them.

**Sample Request**

```
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "cbbac510-3e66-ef11-a671-6045bd03d9d8",
  "DestinationPhoneNumber": "+123456798",
  "ContactId": "761e062f-c734-ef11-8e4f-00224808a166",
  "Windows": [
    {
      "Start": "2024-09-10T13:00:00.000Z",
      "End": "2024-09-10T15:59:59.999Z"
    },
    {
      "Start": "2024-09-11T13:00:00.000Z",
      "End": "2024-09-11T15:59:59.999Z"
    }
  ],
  "InputAttributes": {
     "type": "callback"
    "isLastAttempt": "false"
  }
}

```

### Related information

[Use proactive engagement tables for reporting](proactive-engagement-tables.md)