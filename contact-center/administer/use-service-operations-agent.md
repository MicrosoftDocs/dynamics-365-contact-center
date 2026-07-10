---
title: Use Service Operations Agent in Dynamics 365 Contact Center
description: Learn how to use Service Operations Agent to configure, validate, and troubleshoot Dynamics 365 Contact Center features—start improving admin efficiency today.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 07/09/2026
ms.topic: how-to
ms.collection: bap-ai-agent
ms.update-cycle: 180-days
---

# Use Service Operations Agent

[!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

Service Operations Agent in Dynamics 365 Contact Center is a self-service AI agent that supports administrators with configuration, validation, and troubleshooting tasks. The agent helps streamline onboarding and ongoing maintenance, making administrator workflows more efficient.

Service Operations Agent supports conversational setup of Dataverse tables, such as queues and workstreams.

## Supported capabilities

> [!NOTE]
> Service Operations Agent is available in English only.

**Configure channels**

- Help set up channels and workstreams.
- Sync phone numbers with Azure Communication Services and Teams.
- Provide guidance on best practices for contact center configuration.

**Manage queues**

- Create a queue with one of the out-of-the-box assignment methods. If you don't specify the assignment method, the system assigns a default method.
- Change assignment method. Custom assignment isn't supported.
- Assign users to specific queues.
- Create skills and assign them to users.
- Check queue details.
- Set up operating hours.

**Manage workstreams, route-to-queue rules**

Use natural language instructions to create workstreams and route-to-queue rules.

- You can create multiple rules, but without conditions only.
- Make sure that the workstream and queue are for the same channel.

**Query about capabilities and troubleshoot issues**

- Query the agent about contact center capabilities.
- Ask questions about the environment.
- Provide diagnostics for supported channels.

## Prerequisites

- The Omnichannel administrator role to access Service Operations Agent.
- The  System Administrator role to manage Power Apps connections and Model Context Protocol (MCP) connections.
- The Power Platform [Pay-as-you-go plan](/power-platform/admin/pay-as-you-go-overview) requires the use of an Azure subscription that the system charges when the agent runs. Make sure that you [set up consumption-based billing](/dynamics365/customer-service/administer/setup-pay-as-you-go).
- For Service Operations Agent to troubleshoot issues during setup:
  - [Application Insights is configured](/azure/azure-monitor/app/create-workspace-resource?tabs=portal#create-an-application-insights-resource).
  - [Application Insights is connected with Dynamics 365 Contact Center](/power-platform/admin/conversation-diagnostics-application-insights#set-up-a-connection-with-azure-application-insights).

## Conversational setup

Use natural language to set up your contact center and watch Service Operations Agent run the steps while keeping a human in the loop.

### Steps to access

Service Operations Agent requires a Dataverse connection through the MCP server. This connection enables the agent to access and manage your environment.

Complete the following steps:

1. In Copilot Service admin center, select **Launch** in the **Conversational Setup** tile. The **Service Operations Agent** page appears with a prompt to connect to Dataverse via the MCP server.
1. Select **Allow once**.

If the agent can't perform actions or retrieve information, verify that the connection is configured correctly.

To configure or refresh the connection between Dataverse and the MCP server, follow these steps:

1. Go to [Power Apps](https://make.powerapps.com).
1. Select the correct environment in the upper-right corner.
1. Select **Connections** in the left pane.
1. Locate **D365 Contact Center MCP Connection**, and then delete it.
1. In Copilot Service admin center, open **Admin Copilot**, and then start a new conversation.
1. When the connection card appears, select **Allow** to create a new connection for **D365 Contact Center Admin MCP**.

### Use example prompts

Use clear, detailed prompts, and explicitly specify the relevant channel or topic to reduce the risk of inaccurate or unreliable answers. A few examples of prompts are as follows.

**Configure and set up**

- Can you help me create a voice workstream?
- Please create a voice workstream with the name `<WorkstreamName>` and use the `<QueueName>` queue as the default queue.

**Manage queues**

- Create a queue `<QueueName>` for voice channel and set its assignment method to highest capacity.
- Update the assignment method for `<QueueName>` to round robin.
- Which voice queues are available?
- Which queues aren't connected to workstreams?

**Create rules for route-to-queue**

- Create a route to queue ruleset `<RulesetName>` for workstream `<WorkstreamName>` and add a rule `<RuleName>` to assign the conversations to `<QueueName>`.

**Manage knowledge and troubleshoot**

- Is there an active Azure Communication Services resource in this organization?
- List the phone numbers associated with the Azure Communication Services resource.
- What is my organization ID?

## Configure routing capabilities



### Create and manage workstream

| Operation | Description |
|-----------|-------------|
| **Create** | Create a new workstream. |
| **Update** | Modify advanced settings such as presence options, capacity, and wrap-up time. |
| **Delete** | Delete a workstream by name. |
| **Validate** | Check that a workstream is properly configured and ready. |
| **AssociateChannel** | Link an existing channel configuration to a workstream. |
| **AddQueue** | Set the default and fallback queue for a workstream. |
| **AddBot** | Associate an existing agent with a workstream. |
| **Get** | Retrieve complete workstream details by name. |

### Create and manage queues

| Operation | Description |
|-----------|-------------|
| **Create** | Create an advanced queue with settings for type, priority, assignment strategy, and visibility. |
| **Edit** | Update queue properties without changing the type. |
| **Delete** | Remove a queue. |
| **AddUser** | Add a user as a queue member. |
| **RemoveUser** | Remove a user from a queue. |
| **SetOperatingHours** | Assign or clear queue business hours. |
| **LinkToWorkstream** | Connect a queue to a workstream as fallback queue or through route-to-queue rules. |
| **GetDetails** | Retrieve queue metadata, including type, strategy, priority, hours, workstreams, and member count. |
| **ListUsers** | List all queue members with their name and email. |
| **Update OOB Assignment strategy** | Update the assignment method of the queue.|

### Create and manage routing rules (route-to-queue rules)

| Operation | Description |
|-----------|-------------|
| **CreateRouteToQueueRuleset** | Create a route-to-queue ruleset on a workstream (name and optional description only). |
| **AddRule** | Add a rule that routes work items to a single target queue. |
| **UpdateRule** | Update a rule's name, target queue, and position. |
| **DeleteRule** | Remove a rule from a ruleset. |
| **UpdateRuleset** | Update ruleset name, description, and execution order (StepOrder). |
| **DeleteRuleset** | Delete an entire ruleset. |
| **ReorderRules** | Reorder rules within a ruleset (JSON array of rule names). |
| **SetHitPolicy** | Set hit policy (All or First). |
| **ListRules** | List all rules in a ruleset. |
| **ListRulesets** | List all rulesets for a workstream. |

Classification rulesets, assignment rules, overflow rules (and other ruleset types), percentage-based/multi-queue distribution, and adding or editing **conditions** in rules aren't supported through the tools and must be configured manually in Copilot Service admin center.

### Create operating hours

| Operation | Description |
|-----------|-------------|
| **Create** | Create an operating hours schedule with schedule name, time zone code, start date, work start and end times (HH:mm), recurring days (MO-SU), and optional break period (BreakStart and BreakEnd). |

### Manage capacity profiles

| Operation | Description |
|-----------|-------------|
| **Create** | Create a capacity profile with default max units, reset duration, and block-assignment settings. |
| **Update** | Rename the profile or update the max units and block-assignment flag. |
| **AssignUsers** | Assign one or more users to a profile. |
| **RemoveUsers** | Remove one or more users from a profile. |

### Manage skills

| Operation | Description |
|-----------|-------------|
| **Create** | Create a new skill with an optional description. |
| **Read** | Retrieve all skills assigned to a user. |
| **Update** | Rename a skill or update its description. |
| **Delete** | Delete a skill that has no assignments. |
| **AddToUser** | Assign a skill to a user with an optional proficiency rating. |
| **AddToQueue** | Assign a skill to all members of a queue with an optional rating. |
| **RemoveFromUser** | Remove a skill from a user. |
| **RemoveFromQueue** | Remove skill from all queue members. |

### Manage users

| Operation | Description |
|-----------|-------------|
| **Update** | Modify user details (first/last name, email, title, phone, capacity). |
| **Disable** | Deactivate a user account. |
| **AssignRole** | Grant a security role. |
| **UnassignRole** | Remove a security role. |

### Related information

[Overview of contact center agents](overview-contact-center-agents.md)  
[Responsible AI at Microsoft](https://www.microsoft.com/ai/responsible-ai?msockid=2128a9baf27c62973b80bee0f3bb6398)  
[Responsible AI FAQ for Service Operations Agent](../implement/service-operations-agent-rai-faq.md)  
[Use AI-generated conversations for agentic simulations](configure-simulation-agent.md)  