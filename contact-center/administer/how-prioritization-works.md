---
title: How Prioritization Works in Dynamics 365 Contact Center
description: Dynamics 365 Contact Center playbooks allow you to automate priority increases. Find out how to handle representative availability overflow.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 04/21/2026
ms.topic: how-to
ms.collection: bap-ai-copilot
---

# How prioritization works in assignment methods


## Prerequisites

- Unified routing is enabled
- Conversation orchestration is configured

## Dynamic prioritization

Dynamic Prioritization is an AI-led approach to increase the priority of conversations based on:

- **Increasing wait time**: Priority escalates as customers wait longer
- **Conversation transfers**: Priority boost when conversations move between queues

### Priority score system

The priority score conversation attribute works as follows:

- Holds the dynamically increasing priority value of conversations
- Cumulatively adds incremental values to maintain a running priority score
- Initial/base priority score can be set using classification rules
- Priority increment logic is authored through prompt templates in the Conversation orchestration playbook
- Any queues which have a priority escalation or update playbook enabled, should not have any custom prioritization rules configured.
- Priority scores range from 0 to 100,000
- Minimum wait time interval is 30 seconds
- Tie-breaking: When priority scores are equal, FIFO (First-In-First-Out) is used



## Scenario: Dynamic prioritization - Wait time escalation

This scenario automatically increases the priority of conversations based on how long customers wait in the queue.

**Trigger event**: Conversation is waiting in queue

**How it works:**

1. When a conversation enters the queue, the playbook evaluates the configured conditions.
1. Based on matching context variable values, the system increases the priority score at the specified time interval.
1. The system offers higher priority conversations to representatives first than the lower priority ones.

**Example:**

| Customer segment | Priority increase | Time interval |
|------------------|-------------------|---------------|
| VIP customers | 20 | Every 30 seconds |
| Gold tier customers | 15 | Every 30 seconds |
| All other customers | 5 | Every 30 seconds |

## Scenario: Dynamic prioritization - Queue transfer escalation

This scenario increases conversation priority when a conversation is transferred to a specific queue.

**Trigger event**: Conversation is transferred to queue

**How it works:**

1. When you transfer a conversation to a queue where this playbook is active, the priority increases immediately.
1. The priority increase is a one-time adjustment based on the configured conditions.
1. Transferred conversations receive appropriate attention based on your business rules.

**Example:**

| Customer segment | Priority increase |
|------------------|-------------------|
| VIP customers | 50 |
| Escalation transfers | 30 |
| All other transfers | 10 |

## Scenario: Representative availability based overflow

This scenario triggers overflow actions when no representatives are available to handle conversations.

**Trigger event**: Conversation is waiting in queue and no representative is available.

**How it works:**

1. When a conversation enters the queue, the system checks for availability of representatives.
1. If no representatives are available based on presence, capacity, and skills, the overflow action triggers immediately.
1. You can configure different actions based on customer attributes.

**Available overflow actions:**

| Action | Description |
|--------|-------------|
| **Transfer to queue** | Route the conversation to a different queue |
| **Direct callback** | Offer the customer a callback option |
| **Voicemail** | Route to voicemail for later follow-up |
| **End conversation** | End the conversation with a message |

**Example:**

| Customer segment | Overflow action |
|------------------|-----------------|
| VIP customers | Transfer to VIP Overflow Queue |
| After-hours calls | Route to voicemail |
| All other customers | Offer direct callback |



