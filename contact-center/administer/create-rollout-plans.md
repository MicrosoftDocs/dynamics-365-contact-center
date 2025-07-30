---
title: Create rollout plans to manage AI agents (preview)
description: Learn how to use the rollout manager in Dynamics 365 Contact Center and Customer Service to create rollout plans and manage the deployment of AI agents.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: 
ms.date: 08/01/2025
ms.custom: 
- bap-template
- bap-ai-copilot
---

# Create rollout plans to manage AI agents (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

The rollout manager is a wizard that helps AI administrators and supervisors adopt autonomous AI agents in a phased, guided, and controlled manner. It enables organizations to activate features like Customer Intent Agent and Case Management Agent through structured rollout plans that align with business needs and readiness.

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Create rollout plans using rollout manager

The rollout manager guides administrators to existing configurations and enables phased adoption without duplicating controls.You can create individual rollout plans for each autonomous agent or a single rollout plan for multiple agents based on your business needs.

1. In the site map of Copilot Service admin center, select **Home**, and then select **Open** in **Agent hub (Preview)**.

1. On the **Agent hub** page, select **Create a rollout plan**. The **Rollout manager (preview)** page appears.
1. Select **Create**.
1. Use the guided steps to create a rollout plan for the following autonomous agents:
   - **Customer Intent Agent**: This agent helps service representatives by providing them with suggested responses based on customer intent.
   - **Case Management Agent**: This agent helps service representatives by automating case management tasks, such as creating and updating cases.
   - **Customer Knowledge Management Agent**: This agent helps service representatives by providing them with knowledge base articles based on customer queries.

The wizard guides you to customize settings for each autonomous agent, such as select a line of business for Customer Intent Agent, and case update and case closure for Case Management Agent.

### Manage rollout plans

You can do the following actions on the rollout plans after you select a rollout plan from the list:
- **Edit**: Modify the settings or configuration of an existing rollout plan.

- **Deactivate or activate**: Temporarily disable or enable a rollout plan.
- **Delete**: Permanently remove a rollout plan.

### Considerations for rollout plans

The following considerations apply:

- The rollout manager uses the existing settings for the AI agent.

- For each autonomous agent, you can configure the settings on the parent page of the AI agent.
- For Customer Intent Agent and Customer Knowledge Management Agent, when you deactivate or delete a rollout plan, the corresponding autonomous agent setting isn't deactivated or deleted.
- For Case Management Agent only, when you deactivate or delete a rollout plan, the corresponding rules are also deactivated or deleted.

### Related information

[Learn about autonomous service agents](autonomous-agents-overview.md)  