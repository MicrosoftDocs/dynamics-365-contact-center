---
title: Responsible AI FAQ for conversation orchestration
description: This FAQ provides information about conversation orchestration in Dynamics 365 Contact Center. This FAQ also includes key considerations and details about how AI is used, how it was tested and evaluated, and any specific limitations.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: faq
ms.collection: bap-ai-copilot
ms.date: 10/30/2026
ms.update-cycle: 180-days
ms.custom: 
- bap-template
- responsible-ai-faq
ai-usage: ai-assisted
---

# Responsible AI FAQ for conversation orchestration

[!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

This FAQ article describes the AI impact of conversation orchestration in Dynamics 365 Contact Center.

## What is conversation orchestration?

Conversation orchestration is a capability in Dynamics 365 Contact Center that manages how conversations are handled. It responds to events across the conversation lifecycle and dynamically determines the next best action using an "event-condition-action" framework.

Administrators describe their orchestration logic in natural language using playbooks. When you publish a playbook, the system uses a language model to convert it into a structured runtime format that the system then uses to perform playbook actions.

By evaluating customer context, conversation signals, and real-time operational conditions according to playbook rules, conversation orchestration determines the next best action, such as prioritization, overflow handling, messaging, or assignment. This approach reduces administrative complexity, shortens wait times, optimizes handling time, and helps deliver more consistent and resilient customer experiences at scale, even under fluctuating demand.

## What can conversation orchestration do?

Conversation orchestration in Dynamics 365 Contact Center manages how conversations are handled. It responds to events across the conversation lifecycle and dynamically determines the next best action using an "event-condition-action" framework.

- **Event**: A conversation enters, progresses, or changes state, such as arrival, waiting in queue, transfer, agent availability change, or prolonged wait time.

- **Condition**: The system evaluates customer context, conversation signals, historical interactions, and real-time operational factors such as capacity, expertise availability, time of day, or service priorities.

- **Action**: Based on the various conditions and triggers, conversation orchestration runs relevant configured actions as determined by the published playbooks, including prioritization changes, overflow handling, and escalation strategies.

Administrators define these behaviors using natural language playbooks. This approach allows organizations to manage complex distribution scenarios while maintaining consistent customer experiences as conditions evolve. Some of the key conversation orchestration capabilities include the following features:

- **Overflow handling**: Applies real-time overflow actions when a queue is outside operating hours, all representatives are signed out, no representatives are available, wait times are high, or queue demand is high. For direct inbound calls, applies fallback actions when the target representative is unavailable, rejects the call, or doesn't respond before the notification times out.

- **Dynamic prioritization**: Increases or resets conversation priority based on wait time, queue transfers, or queue consults. You can tailor priority by context variables, such as customer tier or product ownership. Dynamic prioritization works with existing overflow rules, assignment rules, and other conversation orchestration playbooks, but doesn't apply to queues with custom prioritization rules. Use classification rules to set the initial conversation priority score.

- **Assignment to a preferred expert or previously engaged representative**: Routes conversations to a preferred expert mapped to the contact or to a representative who previously interacted with the customer, with fallback to the next best available expert. For returning asynchronous chats, keeps the same expert when representative affinity is enabled and the expert meets the presence and active conversation limit requirements.

- **Bullseye routing through user groups**: Starts assignment with a targeted Level 0 user group, then progressively expands to additional user groups as wait time increases. Earlier groups remain active and take priority over later groups, without transferring the conversation to another queue.

## What is the intended use of conversation orchestration?

Use conversation orchestration to author and configure dynamic routing and assignment criteria through natural language playbooks. When you publish a playbook, the system uses a language model to convert it into a structured runtime format. Published playbooks use this format to perform actions without consuming Copilot credits or AI tokens at runtime.

## How is conversation orchestration evaluated? What metrics were used to measure performance?

- Evaluations were run on the playbook conversions to match the intended routing and assignment criteria, how accurately the playbook was converted, including the conditions, scope of queues, and actions mentioned in the playbooks. Also, functional tests were done to evaluate the accuracy of runtime reliability of the system.
- Performance was evaluated using Microsoft internal support data by simulating scale runs close to production-level traffic volumes.

## What are the limitations of conversation orchestration? How can users minimize the impact of conversation orchestration’s limitations when using the system?

The feature has the following limitations:

- **Support English only**: The system currently supports the English language only.
- **Playbooks**: This capability supports playbooks with editable sections only to select information from drop down lists and edit information according to validations in place. Administrators can refer to the warning and error messages to update and publish playbooks with relevant information.
- Because the system uses a language model to convert natural language playbooks into a structured runtime format, the converted output might not fully capture the intended logic. You can identify any deviations only during runtime. Administrators should test and monitor runtime behavior and revise the playbook if orchestration doesn't work as intended.

## What operational factors and settings allow for effective and responsible use of conversation orchestration?

- End users can select one of the prompt templates to edit and publish playbooks that describe their orchestration and assignment logic.
- The system is designed with playbook-level validations that it checks when saving and publishing the playbook. If any validations are missed or failed, end users can refer to the warning and error messages.
- Microsoft will introduce a human review step that allows administrators to review the converted output of their playbooks before it takes effect, helping catch conversion errors before publication.

## How do I provide feedback on conversation orchestration?

Administrators of Dynamics 365 Contact Center can delete any saved or published playbooks, disable the feature toggle to turn off the feature, and log a service request with Microsoft if they need to provide feedback.

## Related information

[Configure conversation orchestration using AI-driven playbooks](../administer/configure-conversation-orchestration.md)    
