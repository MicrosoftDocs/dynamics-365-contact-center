---
title: Responsible AI FAQ for AI Agents (preview)
description: This FAQ provides information about the AI Agents in Dynamics 365 Contact Center and Dynamics 365 Customer Service. This FAQ also includes key considerations and details about how AI is used, how it was tested and evaluated, and any specific limitations.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: faq
ms.collection: bap-ai-copilot
ms.date: 06/04/2025
ms.custom: 
- bap-template
- responsible-ai-faq
---
# Responsible AI FAQ for AI Agents (preview)

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

This FAQ article describe the AI impact of AI Agents in Customer Service and Dynamics 365 Contact Center.

## What are AI Agents?

AI Agents are intelligent tools designed to enhance customer service efficiency and effectiveness in Dynamics 365 Contact Center and Dynamics 365 Customer Service. With generative AI, they improve customer intent discovery and real-time knowledge management, supporting self-service and assisted scenarios.

## What are the systems capabilities of AI Agents?

### Customer Intent Agent

The Customer Intent Agent uses generative AI to autonomously discover customer intents by analyzing past interactions in your customer relationship management (CRM) system. It builds an intent library to:

- **Improve dynamic conversations**: Service representatives quickly understand customer needs, guide interactions with relevant follow-up questions, and offer real-time tailored solutions.

- **Assist service representatives**: A curated list of questions and suggested solutions appear in the chat response box, enhancing efficiency and reducing typing effort.

- **Enhance self-service capabilities**: The agent generates follow-up questions and queries knowledge sources based on collected information, resulting in higher deflection rates and allowing service representatives to focus on complex cases.

### Customer Knowledge Management Agent

The Customer Knowledge Management Agent helps create and manage customer knowledge in real time. After a case is closed, the Knowledge Management Agent:

- **Analyzes case details and related information**: Includes notes, conversations, and emails to draft a knowledge article.

- **Fills knowledge gaps**: Identifies whether the new article is necessary by comparing the case against the existing Dynamics 365 knowledge base, avoiding duplicates.

- **Ensures compliance**: Sensitive data is scrubbed automatically, and organizations can extend compliance checks with custom automation.

### Case Management Agent

> [!NOTE]
> Case Management Agent is available in Customer Service only.

The Case Management Agent helps automate case handling, saving time service representatives spend on manually filling case details. Administrators can customize the agent's behavior by configuring rules per the organization's requirements.
 
The capabilities of the Case Management Agent include:

 - **Autonomous case creation and update**: Creates and updates cases from live chats and updates cases from emails automatically. The agent uses AI to predict and populate relevant fields.

- **Automated follow-up and closure**: Sends follow-up emails and resolves cases based on predefined rules, streamlining the case closure process. 

## What is the system’s intended use?

These AI agents are designed to:

- Enhance organizational knowledge management by automating the creation and refinement of knowledge articles while ensuring a comprehensive and accurate intent library that aligns with business needs. This system can work autonomously to ensure content is always kept up to date.

- By leveraging autonomously managed and updated intent library and knowledge base, organizations can address customer inquiries more effectively and provide accurate, timely solutions, enhancing both service representative efficiency and self-help resolution rates.

- Automatically extract and populate the relevant case and related entity fields from customer emails and chats to reduce manual data entry for customer service representatives. This ensures that the case information is complete right from case creation.


## How is AI Agent evaluated? What metrics are used to measure performance?

Performance is evaluated using Microsoft's internal support data and through ongoing pilots within Microsoft Customer Service and Support (CSS). The Customer Intent Agent is assessed based on the accuracy of extracted intents against manually identified ground truth derived from internal support data. Similarly, the Knowledge Management Agent is evaluated for the quality and relevance of its generated knowledge articles, to make sure that they align with the established ground truth and avoid duplication. The Case Management Agent is evaluated based on the quality and relevance of its predictions for the configured fields, generated from the specified context sources.

Additionally, evaluation datasets are run to assess performance against potential personally identifiable information (PII) leaks, reflecting Microsoft's commitment to protecting customer privacy. Privacy and compliance is a critical focus of these evaluations.

## What are the limitations of AI Agent? How can users minimize the impact of agent limitations?

AI Agents have the following limitations:

- **Supports English only** The system currently supports the English language only.

- **Usage limits**: This capability might be subject to usage limits or capacity throttling.

- **Dependence on data quality**: The effectiveness of the system relies on the quality and completeness of CRM data. A more diverse range of conversations around different intents help create a more complete and accurate intent library.

- **Customization requirements**: Users need to actively review the AI-generated intent library and knowledge articles to make sure of accuracy. Customization efforts, such as overrides and tweaks, are necessary to refine and align the output with business needs.

## What data do AI Agents collect? How is the data used?

The AI Agents generate intents and knowledge articles based on the data that already exists in your Dataverse instance. They do not collect any additional data beyond basic telemetry and any feedback you provide. The data within your CRM system is analyzed to create intent libraries and draft knowledge articles.

## What operational factors and settings allow for effective and responsible use of the system?

- AI Agents can operate in both autonomous and supervised modes. While the system is designed to function autonomously and ensure it's always kept up to date, administrators can adjust settings to align with organizational requirements. This includes leveraging autonomous management to improve efficiency in customer service activities, such as maintaining an accurate intent library and knowledge base. However, when autonomous approval is enabled, there's a heightened risk of inadvertently exposing unintended information, including PII. Organizations should therefore carefully review and monitor system outputs to minimize these risks and safeguard sensitive data.

- Administrators have the ability to remove or discard generated intents and knowledge articles as needed, supporting the creation of a well-curated intent library and knowledge base.

- AI Agents also apply content moderation policies on all generative AI requests to protect users against offensive or harmful content. These content moderation policies also extend to malicious attempts at jailbreaking, prompt injection, prompt exfiltration, and copyright infringement.

- As a best practice, users are encouraged to inform all stakeholders who have been exposed to the AI system that they have interacted with an AI system.

### Related information

[Responsible AI FAQ for Copilot in Customer Service](/dynamics365/customer-service/implement/faq-responsible-ai-copilot?context=/dynamics365/contact-center/context/implement-context)  
