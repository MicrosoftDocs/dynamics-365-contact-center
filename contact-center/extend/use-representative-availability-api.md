---
title: Use representative availability APIs from Copilot Studio
description: Learn how to use the representative availability APIs from Copilot Studio.
ms.date: 04/30/2026
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Use representative availability APIs in a Copilot Studio agent

You can trigger the representative availability APIs from your Copilot Studio agent to retrieve customer service representative and queue availability information before escalating the conversation to a service representative. By determining availability before escalating, you improve the customer experience and reduce queue abandonment.

## Prerequisites
- Ensure that the Copilot Studio agent has the **Omnichannel administrator** role to call the availability APIs.

## Add the APIs to Escalate topic

Do the following steps in Copilot Studio:

1. Go to your AI agent and then select **Topics**.
2. Select the **System** tab to view the default system topics and then select the **Escalate**.
1. In the authoring canvas, select **Add** and then select **Add a tool**
1. In the **Connector** tab, search and select **Perform an unbound action in selected environment**.
1. If no connection is active, do the following:
   - Select **Create new connection**.
   - Select the authentication type as **OAuth**.
   - Select **Create**.
1. Set the **Environment** to **Current**.
2. Select one of the following APIs:
   - `CCaaS_GetRepresentativeAvailabilityForConversation`
   - `CCaaS_GetRepresentativeAvailabilityBeforeConversation`
1. After selecting the action, update the **Advanced Parameters** as required.
2. Add the rules for the AI agent based on the API response. you can use the **Outputs** from this node to create conditional branching logic. For example, if the API returns that no service representatives are available, you can redirect the user to a "Leave a Message" topic instead of escalating the conversation.
1. Save and publish.


## Related information
[Use representative availabilty APIs](representative-availability-overview.md)  
[CCaaS_GetRepresentativeAvailabilityForConversation](./api/ccaas_getrepresentativeavailabilityconversation.md)  
[CCaaS_GetRepresentativeAvailabilityBeforeConversation](./api/ccaas_getrepresentativeavailabilitybeforeconversation.md)  