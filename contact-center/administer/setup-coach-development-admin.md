---
title: Set up coaching and development (preview)
description: Configure coaching and development for your organization. Enable scorecards, training assignments, and real-time coaching tips for customer service representatives.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 11/17/2026
ms.custom: bap-template
---

# Set up coaching and development (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Configure the connections and flows required for coaching and development. Enable coaching tips, scorecards, and training for your organization and make real-time coaching available through representative experience profiles.

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

Before you begin, ensure that:

- You have the **Quality Administrator** security role. Supervisors who configure and use coaching have the **Quality Manager** role. Learn more in [Assign roles and enable users](/dynamics365/customer-service/implement/add-users-assign-roles).
- [Microsoft Copilot credits are set up](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- **Enable AI agents** is turned on for the Dynamics 365 environment in Power Platform admin center. Learn more in [Copilot adoption in the Power Platform](/power-platform/admin/copilot/copilot-hub).
- Your organization provided consent for potential data movement across regions. For optimal performance, the system might route service calls outside your regional boundary if local capacity is temporarily unavailable. To participate, you need to provide consent for potential data movement across regions. Learn more in [Move data across regions for Copilots and generative AI features](/power-platform/admin/geographical-availability-copilot).
- (Optional) Quality evaluation is configured if you want scorecards to use completed evaluations.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Security roles and privileges

| Persona | Security role | Privileges |
|---|---|---|
| Administrator | Quality Administrator | - Configure connection references and enable the **Agent Coach CSR Insights** flow. <br> - Turn on scorecards, and training assignment and creation.   |
| Supervisor | Quality Manager | - Assign scorecards to business units and configure scorecard settings in coaching setup. <br> - Review, edit, and publish scorecards, and use the coaching dashboard to obtain coaching insights. <br> - Create, generate, publish, and assign training, and track assignments on the **Training** tab.<br> - View coaching and training impact on the **Impact** tab. |
| Representative | Customer Service Representative | - Review, acknowledge, and comment on scorecards. <br> - Open and complete assigned training in **My training**.  |

## Configure connection references and enable flows

When you go to the **Coaching** page in the Workforce Engagement Management (preview) app, the **Prerequisites** section shows whether connection references and flows are set up. Configure connection references and turn on the **Agent Coach CSR Insights** flow. These connections link the flow to data sources such as Microsoft Dataverse and Copilot Studio.

1. In the Workforce Engagement Management (preview) app, go to **Admin settings** > **Quality management**.
1. On the **Quality management** page, for **Coaching (preview)**, select **Manage**. 
1. On the **Coaching (preview)** page, in **Prerequisites**, check the status of **Step 1: Connection References** and **Step 2: Power Automate Flows**.
    1. If **Step 1: Connection References** shows as **In progress** or **Incomplete**, select **Manage connections**. In the **Configure Connections** dialog box, select **Update connection references to use your connector** to complete connection references.
    1. If **Step 2: Power Automate Flows** shows as **Not Started**, select **Enable** to enable the **Agent Coach CSR Insights** flow. If the flow is turned off, use the navigation link to open the flow in Power Automate and enable it.

1. When all tiles show as **Ready**, the prerequisites are complete.

After configuration is complete, refresh your browser if the status doesn't update. If you have problems configuring connection references from the **Coaching (preview)** page, you can do a manual setup. Follow the steps provided in connection references for [coaching and development](/dynamics365/customer-service/administer/admin-km-agent-connections?context=/dynamics365/contact-center/context/administer-context#set-up-connection-references-for-coaching-and-development).

## Enable coaching and development capabilities

1. In the Workforce Engagement Management (preview) app, go to **Admin settings** > **Quality management**.
1. On the **Quality management** page, for **Coaching (preview)**, select **Manage**.
1. Make sure that all prerequisites show as **Ready**.
1. To enable scorecards, select the **Turn on scorecards for your organization** toggle.
1. To let supervisors create and assign training, select the **Turn on Training Assignment and Creation for your organization** toggle.
1. Select **Save**.

> [!NOTE]
> Enabling a capability at the organization level doesn't complete supervisor configuration. Supervisors must configure coaching instructions and scorecards, and must create, publish, and assign training.

## Related information

[Overview of coaching and development (preview)](../use/overview-coach-development.md)  
[Use coaching and development (preview)](../use/use-coach-development-representative.md)  
[Manage coaching and development (preview)](../use/manage-coach-development-supervisor.md)