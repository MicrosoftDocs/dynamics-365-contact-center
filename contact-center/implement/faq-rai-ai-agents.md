---
title: Responsible AI FAQ for AI agents
description: This FAQ provides information about the AI agents in Dynamics 365 Contact Center and Dynamics 365 Customer Service. This FAQ also includes key considerations and details about how AI is used, how it was tested and evaluated, and any specific limitations.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: faq
ms.collection: bap-ai-copilot
ms.date: 06/30/2026
ms.update-cycle: 180-days
ms.custom: 
- bap-template
- responsible-ai-faq
---
# Responsible AI FAQ for AI agents

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]

This FAQ article describes the AI impact of AI agents in Dynamics 365 Customer Service and Dynamics 365 Contact Center.

## What are AI agents?

AI agents are intelligent tools designed to enhance customer service efficiency and effectiveness in Dynamics 365 Contact Center and Dynamics 365 Customer Service. With generative AI, they improve customer intent discovery and real-time knowledge management, supporting self-service and assisted scenarios.

## What are the systems capabilities of AI agents?

### Customer Intent Agent

Customer Intent Agent uses generative AI to autonomously discover customer intents by analyzing past interactions in your customer relationship management (CRM) system. It builds an intent library to:

- **Improve dynamic conversations**: Service representatives quickly understand customer needs, guide interactions with relevant follow-up questions, and offer real-time tailored solutions.

- **Assist service representatives**: A curated list of questions and suggested solutions appear in the chat response box, enhancing efficiency and reducing typing effort.

- **Enhance self-service capabilities**: The agent generates follow-up questions and queries knowledge sources based on collected information. This approach increases deflection rates and lets service representatives focus on complex cases.

Beyond intent discovery, Customer Intent Agent can autonomously lead conversations using business instructions, enterprise functions, and knowledge articles linked to each intent:

- **Follows business instructions**: The instructions defined by the business to make sure of consistent tone, policy compliance, and best‑practice workflows.

- **Invokes enterprise functions**: During a chat or voice session, Customer Intent Agent can call business‑exposed APIs, such as, order lookup, status update, and claim submission to act on the customer’s behalf.

- **Retrieves and synthesizes knowledge**: The agent pulls in relevant knowledge articles and contextual data so every answer is based on accurate and current business content.

- **Generates next best actions**: The agent recommends actions that guide service representatives on the most appropriate next step to take while working on a case.

### Customer Knowledge Management Agent

Customer Knowledge Management Agent helps create and manage customer knowledge in real time. After a case is closed, Customer Knowledge Management Agent:

- **Analyzes case details and related information**: Includes notes, conversations, and emails to draft a knowledge article.

- **Fills knowledge gaps**: Identifies whether the new article is necessary by comparing the case against the existing Dynamics 365 knowledge base, avoiding duplicates.

- **Ensures compliance**: Sensitive data is scrubbed automatically, and organizations can extend compliance checks with custom automation.

### Case Management Agent

> [!NOTE]
> Case Management Agent is available in Customer Service only.

Case Management Agent helps automate case handling, saving time service representatives spend on manually filling case details. Administrators can customize the agent's behavior by configuring rules per the organization's requirements.

The capabilities of Case Management Agent include:

- **Autonomous case creation and update**: Creates and updates cases from live chats and updates cases from emails automatically. The agent uses AI to predict and populate relevant fields.

- **Autonomous case resolution**: Drafts and sends emails based on determined intent from customer queries, using knowledge and custom workflows.
- **Automated follow-up and closure**: Sends follow-up emails and resolves cases based on predefined rules, streamlining the case closure process.

### Quality Evaluation Agent

Quality Evaluation Agent helps organizations make sure that every customer engagement with support&mdash;whether handled by service representatives or AI agents&mdash;is compliant, ethical, and aligned with brand values.

**Customized criteria**: Supervisors set up evaluation criteria, questionnaires, scoring logic, and instructions to define quality. The AI agent uses the criteria to assess customer engagements across different channels and generate scores.

**Actionable insights that drive improvement**: The AI agent provides evaluation summaries, quality scores, and coaching recommendations to help supervisors find gaps, guide representative development, and improve service standards.

**Governance policies**: The AI-powered rule-based system acts as a safeguard layer on top of other AI agents and human-authored communications such as email. The system intercepts outbound email body and attachments, evaluates them against predefined guardrail policies, and then sends the email to the customer if it meets the policy requirements. If the output violates a policy, it can log activity or block the message to prevent noncompliant results from reaching end users based on the policy configured.

### Quality Assurance Agent

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

Quality Assurance Agent delivers real-time quality evaluation, compliance monitoring, and coaching guidance for customer service conversations in Dynamics 365 Contact Center. It analyzes live interactions between customers and service representatives to detect quality problems, identify compliance risks, and provide real-time coaching nudges to improve agent performance.

- Analyze conversation content such as text or chat in real time.

- Evaluate interactions against predefined quality criteria and compliance rules.

- Detect patterns such as policy violations and agent behavior signals. For example, tone, adherence.

- Trigger coaching prompts (nudges) and alerts for compliance concerns.
    
## What is the system’s intended use?

These AI agents are designed to:

- Enhance organizational knowledge management by automating the creation and refinement of knowledge articles while ensuring a comprehensive and accurate intent library that aligns with business needs. This system can work autonomously to ensure content is always kept up to date.

- By using an autonomously managed and updated intent library and knowledge base, organizations can address customer inquiries more effectively and provide accurate, timely solutions. This approach improves service representative efficiency and self-service resolution rates.

- Automatically extract and populate the relevant case and related entity fields from customer emails and chats to reduce manual data entry for customer service representatives. This automation helps ensure that the case information is complete right from case creation.

- Evaluate customer support interactions using your organization’s evaluation criteria. Governance policies enforce guardrail policies on email body and attachments. Supervisors manage these policies. The policies apply to emails sent by Case Management Agent (autonomous flow) and emails composed by customer service representatives. The capability is available with initial support for the email channel, where compliance risk and brand impact are the highest.

- Support quality and compliance in customer interactions. Quality Assurance Agent enables organizations to monitor conversations, provide real-time feedback to agents during live engagements, enforce organizational and regulatory guardrails, and ultimately improve overall customer service outcomes.

## How is AI agent evaluated? What metrics are used to measure performance?

Performance is evaluated using Microsoft's internal support data and through ongoing pilots within Microsoft Customer Service and Support (CSS). Customer Intent Agent is assessed based on the accuracy of extracted intents against manually identified ground truth derived from internal support data. Similarly, Customer Knowledge Management Agent is evaluated for the quality and relevance of generated knowledge articles. It aligns with the established ground truth and avoids duplication. Case Management Agent is evaluated based on the quality and relevance of its predictions for the configured fields, generated from the specified context sources. Quality Evaluation Agent is evaluated for accuracy, quality, and relevance of its outputs.

Key factors include how well customer engagement evaluation outcomes match defined criteria, how clear and useful generated summaries are, and how effective recommendations are for improving support. The Governance policy performance is evaluated based on two dimensions: reliability of policy enforcement (correctly validating violations while avoiding unnecessary blocks on compliant content) and operational efficiency (minimizing added latency). Administrators can use flag-only mode to observe policy performance and calibrate thresholds before activating full enforcement.

Additionally, evaluation datasets are run to assess performance against potential Personally Identifiable Information (PII) leaks, reflecting Microsoft's commitment to protecting customer privacy. Privacy and compliance are a critical focus of these evaluations.

Quality Assurance Agent is assessed using internal tests with different conversation scenarios, checks against defined quality and compliance standards, and continuous monitoring of its behavior and outputs. The evaluation focuses on how accurate the agent is, how often it flags issues correctly or incorrectly, and how consistent its coaching suggestions are.

## What are the limitations of AI agents? How can users minimize the impact of agent limitations?

AI agents have the following limitations:

- **Support English only**: The system currently supports the English language only.

- **Usage limits**: This capability might be subject to usage limits or capacity throttling.

- **Dependence on data quality**: The effectiveness of the system relies on the quality and completeness of CRM data.

    - A more diverse range of conversations around different intents help create a more complete and accurate intent library.
    - Write clear, specific instructions for evaluation questionnaires. To help evaluators make accurate decisions, give guidance that's direct and relevant to the context.

- **Customization requirements**: Users need to actively review the AI-generated intent library and knowledge articles to make sure of accuracy. Customization efforts, such as overrides and tweaks, are necessary to refine and align the output with business needs.

- Quality Assurance Agent might not fully understand complex conversational context or intent. Agent performance depends on the quality of the configured rules, evaluation criteria, and input data (conversation content). In edge cases, the agent might produce incomplete or inaccurate assessments and might not fully capture subtle human nuances, such as sarcasm or cultural context.

- Real-time suggestions are only for guidance and shouldn't replace human judgment.

## What data do AI agents collect? How is the data used?

The AI agents generate intents and knowledge articles based on the data that already exists in your Dataverse instance. They don't collect any other data beyond basic telemetry and any feedback you provide. The data within your CRM system is analyzed to create intent libraries and draft knowledge articles, and governance policies.

Quality Assurance Agent processes customer-agent conversation data, such as chat transcripts and configured business rules, such as quality criteria and compliance guardrails. It doesn't independently generate new training data at runtime. Instead, it evaluates interactions based on pre-defined logic and models.

## What operational factors and settings allow for effective and responsible use of the system?

- AI agents can operate in both autonomous and supervised modes. While the system is designed to function autonomously and keep data up to date, administrators can adjust settings to align with organizational requirements. This approach includes using autonomous management to improve efficiency in customer service activities, such as maintaining an accurate intent library and knowledge base. However, when autonomous approval is enabled, there's a heightened risk of inadvertently exposing unintended information, including PII. Organizations should therefore carefully review and monitor system outputs to minimize these risks and safeguard sensitive data.

- Administrators have the ability to remove or discard generated intents and knowledge articles as needed, supporting the creation of a well-curated intent library and knowledge base.

- AI agents also apply content moderation policies on all generative AI requests to protect users against offensive or harmful content. These content moderation policies also extend to malicious attempts at jailbreaking, prompt injection, prompt exfiltration, and copyright infringement.

- Supervisors can conduct quality evaluations in two modes: fully autonomous mode, where the AI agent completes evaluations without manual intervention, and AI-assisted mode, where the AI agent performs evaluations and the supervisor reviews the results for accuracy and compliance. This flexibility lets supervisors choose complete automation for efficiency or a more controlled approach for oversight and quality assurance.

- Administrators can enable governance with a simple toggle, author policies using natural language, and choose enforcement modes such as **flag-only** and **block** to safely observe behavior before full enforcement. Human oversight is preserved through review workflows, detection logs, and the ability for supervisors to refine policies based on observed outcomes. Auditability and resilience are ensured through persistent logging of all policy evaluations and a fail-open design that prevents platform issues from unintentionally blocking customer communications.

- To mitigate risks, Quality Assurance Agent enables configurable rules and guardrails defined by organizations, human oversight (agents and supervisors review outputs), monitoring and feedback mechanisms to improve performance, and continuous updates based on evaluation and testing insights.

- As a best practice, encourage users to inform all stakeholders who are exposed to the AI system that they have interacted with an AI system.

## How can users provide feedback or report issues?

Users can use the built-in feedback mechanisms (if available) or use support channels to report incorrect or harmful outputs. Feedback helps improve model performance, rule configurations, and the overall system reliability.

### Related information

[Responsible AI FAQ for Copilot in Customer Service](/dynamics365/customer-service/implement/faq-responsible-ai-copilot?context=/dynamics365/contact-center/context/implement-context)  
[Overview of Customer Intent Agent](../administer/overview-customer-intent-agent.md)  