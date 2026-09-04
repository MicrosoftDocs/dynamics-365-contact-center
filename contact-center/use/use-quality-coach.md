---
title: Use quality and coaching skills
description: Use quality and coaching skills to monitor conversation scores, review evaluations, and provide representatives with real-time guidance.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 09/03/2026
ms.custom: bap-template
---

# Use quality and coaching skills

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

Quality and coaching skills help improve service interactions by providing real-time guidance to customer service representatives (service representatives or representatives) and post-conversation insights for supervisors. These skills enable organizations to monitor quality, encourage consistent service behaviors, and take corrective action during and after customer interactions.

> [!IMPORTANT]
> - This feature is intended to help customer service managers or supervisors enhance their team’s performance and improve customer satisfaction. This feature isn't intended for use in making—and shouldn't be used to make—decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and monitoring, recording, and storing communications with end users. This responsibility also includes adequately notifying end users that their communications with representatives might be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Customers are also encouraged to have a mechanism in place to inform their representatives that their communications with end users might be monitored, recorded, or stored.
> - Customers should avoid using the system to infer or make conclusions about emotional or psychological states of employees or customers, such as stress levels, intent, or sentiment beyond supported signals. The system doesn't reliably detect mental or emotional conditions.

## Manage quality and coaching skills as a supervisor

Quality and coaching skills enable supervisors to monitor, evaluate, and improve conversation quality through notifications, scoring insights, and detailed evaluations. The feature supports real-time monitoring and post-conversation analysis.

- **Configure and receive quality notifications**: Receive notifications when configured quality conditions are met. For example, receive an alert when a conversation quality score drops below a defined threshold.

- **Monitor conversations**: View ongoing conversations to track live interactions and closed conversations to review completed sessions. Use the score column to identify conversations that require attention.

To view evaluated conversations:

1. In the site map of Copilot Service workspace, select **Conversations**.
1. In the view selector, select **Closed QAA conversations** or **Ongoing QAA conversations**.

:::image type="content" source="../media/quality-coaching-closed.png" alt-text="Closed QAA conversations view with conversation details and quality scores." lightbox="../media/quality-coaching-closed.png":::

The **Closed QAA conversations** page shows closed conversations and includes the subject, customer, channel, active representative, creation date, status reason, and score.

Select a score to open a side pane that shows the quality score trend, AI-generated summary, quality indicators, and evaluation description.

Open a closed conversation to view its details. In addition to the quality score trend, the conversation transcript includes coaching nudges for context about how representative actions affected the quality results.

The **Ongoing QAA conversations** page shows similar information for active conversations.

## Manage quality and coaching skills as a service representative

Quality and coaching skills provide real-time guidance to help service representatives improve customer interactions as they occur in Copilot Service workspace. The feature enables representatives to receive contextual recommendations and adjust their responses during live conversations.

- Coaching nudges appear inline in the conversation when predefined conditions are triggered. Use these nudges to improve responses or follow recommended practices during customer interactions.

- Use the **Consult** pane to view all coaching nudges generated during the conversation without leaving the active conversation.

:::image type="content" source="../media/quality-coaching-representative-experience.png" alt-text="Active conversation with an inline coaching nudge and guidance in the Consult pane." lightbox="../media/quality-coaching-representative-experience.png":::

## Related information

[Configure quality and coaching skills](../administer/configure-quality-coach.md)  

[Use the Quality Assurance Agent dashboard](../use/quality-assurance-agent-dashboard.md)

[Responsible AI FAQ for AI agents](../implement/faq-rai-ai-agents.md)
