---
title: 
description: 
author: 
ms.author: 
ms.reviewer: 
ms.topic: how-to
ms.collection: 
ms.date: 05/07/2025
ms.custom: bap-template
---

# Configure proactive engagement

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]



## Prerequisites


- Licenses for Dynamics 365 Contact Center or Dynamics 365 Customer Service premium.
- Voice channel provisioned and configured. For more information, see [Provision channels](../implement/provision-channels.md) and [Install the voice channel](../implement/install-voice-channel.md).
- Dynamics 365 Customer Insights
- Microsoft Copilot Studio

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## How it works

## Configure settings for proactive engagement

You can navigate to the proactive engagement settings in one of the following ways:

- In the site map of Copilot Service admin center, select **Productivity** under **Support experience**. Select **Manage** for **Proactive engagements (preview)**, and then select **New**.
- Create an [outbound type of workstream](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context) for voice, and on the workstream page, select **New proactive engagement**.

1. On **Create new proactive engagement (preview)**, enter the following details in **Engagement details**:
   - **Name**: Enter a name for the proactive engagement.
   - **Description**: Enter a description for the proactive engagement.
   - **Workstream**: Select a workstream.
   - **Channel type**: **Voice** is selected by default and not available for edit.
1. In **Routing details**, enter the following information:
    - **Primary queue**: Select a queue. 
    - **Fallback queue**: Select a fallback queue.
    - **Skills**: Select the skills that are required for the proactive engagement.
1. Select **Next**. The **Dialing modes** page appears
1. Select one of the dialing modes as follows:
   - **Copilot**: The system automatically dials the customer and connects the call to the agent when the customer answers. This mode is used for high-volume outbound calls.
   - **Progressive**: The system starts the call with an agent and the adds a representative after the agent actions are complete.
   - **Preview**: The system add the representative to the call and then dials the customer.
1. Select one of the following priority levels:
   - **Normal**: 
   - **High**: 
   - **Critical**: 
1. Select the number of concurrent calls that can be assigned to the representative in **Maximum calls per representative**. This setting is available for Copilot and progressive dialing modes.
1. Call order: Select one of the following options:
   - **Earliest Scheduled Date**
   - **Last in First Out**
   - **First in, First Out**
1. Under **Operating hours**, select the checkbox if calls can be made outside of queue hours. This setting is available for Copilot and progressive dialing modes.
1. Select the action for how the call be handled if the agent fails during the call.
   - Stop making calls immediately
   - Continue making calls
     - Rate of failure reaches: Select a value from the Percent dropdown list. The default value is one.
1. Optionally, you can define rules in the **Rules** section. Select **Use rules**.
    