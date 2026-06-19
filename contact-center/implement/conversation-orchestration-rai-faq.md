---
title: Responsible AI FAQ for conversation orchestration
description: This FAQ provides information about conversation orchestration in Dynamics 365 Contact Center. This FAQ also includes key considerations and details about how AI is used, how it was tested and evaluated, and any specific limitations.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: faq
ms.collection: bap-ai-copilot
ms.date: 06/01/2026
ms.update-cycle: 180-days
ms.custom: 
- bap-template
- responsible-ai-faq
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

- **Overflow handling**: Automatically applies overflow actions, such as offering callbacks or alternate experiences, based on real-time conditions including expert availability, time of day, and service priorities.

- **Dynamic priority escalation across the conversation lifecycle**: Adjusts conversation priority automatically based on lifecycle events such as increasing wait time or transfer into a new queue, ensuring conversations are continuously re-evaluated and progressed without manual intervention.

## What is the intended use of conversation orchestration?

The system is used to author and configure dynamic routing and assignment criteria, using natural language-based playbooks. A language model is used during authoring to convert these natural language playbooks into a structured runtime format before publication.

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


### Related information

[Configure conversation orchestration using AI-driven playbooks](../administer/configure-conversation-orchestration.md)  

