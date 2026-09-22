---
title: Workforce Engagement Management app (preview)
description: Learn about the Workforce Engagement Management app, its capabilities, prerequisites, and role-based access for workforce and quality management.
ms.date: 09/18/2026
ms.topic: overview
author: lalexms
ms.author: laalexan
ms.custom:
  - bap-template
---

# Workforce Engagement Management app (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

The Workforce Engagement Management app brings workforce management and quality management together in a standalone Dynamics 365 app. Workforce planners, schedulers, intraday analysts, quality managers, and customer service representatives (service representatives or representatives) can complete their daily work in one place.

This article describes the app's capabilities, how it relates to Copilot Service workspace, and what users need to open it.

## Relationship to Copilot Service workspace

The Workforce Engagement Management app provides another way to use existing capabilities. It doesn't replace Copilot Service workspace or change your current deployment.

In Copilot Service workspace, the Omnichannel supervisor role grants workforce management capabilities together. The Workforce Engagement Management app introduces dedicated roles for each workforce management function. You can assign the access each user needs without granting broad supervisory access.

For example, a forecaster can work with forecast scenarios and capacity plans without permission to publish schedules. An intraday analyst can monitor adherence and performance with read-only access to plans. You can assign multiple roles to users whose responsibilities span more than one function.

| Consideration | Copilot Service workspace | Workforce Engagement Management app |
| --- | --- | --- |
| Availability | Generally available | Preview |
| Security roles | Omnichannel supervisor and Omnichannel agent for workforce management; Quality Admin, Quality Manager, and Quality Evaluator for quality management. | WFM Administrator, WFM Forecaster, WFM Scheduler, WFM Intraday Analyst, and WFM Service Rep for workforce management; Quality Admin, Quality Manager, and Quality Evaluator for quality management. |
| Access granularity | A single supervisory role grants workforce management capabilities together. | Roles grant capabilities by function. |
| Feature configuration | Copilot Service admin center | **Admin settings** in the app, or Copilot Service admin center |
| Action for existing deployments | None. Your current configuration continues to work. | Assign users a role that makes the app visible. |

Existing workforce management and quality management articles describe procedures in the Copilot Service workspace site map. The same capabilities appear under equivalent nodes in the Workforce Engagement Management app, and the procedures are unchanged. When an article names a Copilot Service workspace location, go to the corresponding node in the app.

## Prerequisites

- An administrator must [install the Workforce Management for Customer Service package](../administer/workforce-management-package-installation.md) in the Power Platform admin center.
- Each user must have a security role that makes the app visible. Review [Security roles and app visibility](#security-roles-and-app-visibility).

## Workforce management capabilities

The **Workforce management** area contains the following features. The nodes available to a user depend on their assigned roles.

| Group | Feature | Description or related article |
| --- | --- | --- |
| Not grouped | **Getting started** | Get links to help you start working in the app. |
| **Planning** | **Planning groups** | Group queues and channels for planning and analysis as a single unit. Read [Use planning groups](workforce-management-use-planning-groups.md). |
| **Planning** | **Operation calendars** | Define working hours and operating patterns for planning. |
| **Planning** | **Forecasting** | [Create and manage forecast scenarios](workforce-management-forecast-scenarios.md). |
| **Planning** | **Capacity planning** | [Create and manage capacity plans](workforce-management-capacity-planning.md). |
| **Planning** | **Manage external data** | [Import historical interaction data](workforce-management-import-historical-data.md) from an external system for forecast scenarios. |
| **Scheduling** | **Schedule workforce** | [Manage workforce schedules](workforce-management-schedule-workforce.md). |
| **Scheduling** | **Shift planning** | [Create and schedule a shift plan](workforce-management-shift-plan.md). |
| **Scheduling** | **Shift rotations** | [Create and manage shift rotation policies](workforce-management-shift-rotation-policies.md). |
| **Scheduling** | **Shift bookings** | View bookings assigned to representatives. |
| **Scheduling** | **Requests management** | [Review and act on time-off requests](workforce-management-view-time-off-requests.md). |
| **Scheduling** | **Schedule calendar** | [Use the schedule calendar](/dynamics365/customer-service/use/use-agent-calendar). |
| **Monitoring** | **Shift summary** | View a representative's scheduled shifts and activities. |
| **Monitoring** | **Adherence tracker** | [Use the adherence tracker](workforce-management-adherence-tracker.md). |
| **Monitoring** | **Intraday performance** | Compare daily performance against the forecast at the interval level. |
| **Monitoring** | **Adherence historical analytics** | [Use the adherence history report](workforce-management-use-adherence-history-report.md). |

## Quality management capabilities

The **Quality management** area contains the following features.

| Group | Feature | Description |
| --- | --- | --- |
| **Evaluation** | **Evaluations** | Create, assign, and complete evaluations of service interactions. |
| **Evaluation** | **Evaluation criteria** | Define the criteria used to score evaluations. |
| **Evaluation** | **Evaluation plan** | Define which interactions to evaluate and how often. |
| **Governance** | **Policies** | Define governance policies and review policy violations. |
| **Screen recordings** | **Screen recordings** | Review screen recordings captured during service interactions. |

## Administration

Administrators can configure workforce management and quality management without leaving the app.

1. At the bottom of the site map, select **Admin settings**.
1. Select the area to configure.

### Workforce management settings

The **Workforce management** page contains the following settings.

| Group | Setting | Description |
| --- | --- | --- |
| **Workforce setup** | **User management** | Manage representatives and their skills, capacity, and roles. Select **View** to open user management in Copilot Service admin center. |
| **Forecasting** | **Forecast volume** | Manage your organization's forecast volume. |
| **Forecasting** | **Capacity planning** | Plan your organization's capacity. |
| **Shift and schedule management** | **Shift activity types** | Manage activity types used in shifts. |
| **Shift and schedule management** | **Schedule management** | Allow administrators to manage shift plans and schedules. |
| **Shift and schedule management** | **Shift-based routing** | Allow unified routing to assign conversations and cases based on representative shift schedules. |
| **Shift and schedule management** | **Shift rotations** | Turn on shift rotations for your workforce. |
| **Time management** | **Representative calendar** | Give representatives access to their schedules and activities, such as support, training, and breaks. |
| **Time management** | **Time-off request types** | Manage the types of time off that representatives can request. |
| **Time management** | **Bidding** | Manage shift bidding. |
| **Time management** | **Swapping** | Manage shift swapping. |
| **Reporting** | **Adherence historical analytics** | Analyze representative schedule adherence over time. |
| **Reporting** | **Intraday performance** | Analyze representative performance metrics throughout the day. |
| **Intraday management** | **Workforce alerts (preview)** | Manage the types of workforce alerts that supervisors can create. |

### Quality management settings

The **Quality management** page contains the following settings.

| Setting | Description |
| --- | --- |
| **Quality evaluation** | Manage how AI is used for quality evaluations. |
| **Governance** | Manage how AI delivers customer responses with built-in governance, compliance, and quality controls. |
| **Enable screen and call recording** | Configure recording of representative activity for training and quality purposes. |

## Security roles and app visibility

The app is visible only to users assigned a role that grants access to it. Users without one of these roles don't have the app in their list of apps.

Within the app, site map visibility depends on the user's assigned roles. Workforce management and quality management use separate sets of roles. Assign a role from each set to a user who needs access to both areas.

### Workforce management roles

Five dedicated roles cover administration, forecasting, scheduling, intraday analysis, and representative self-service. These roles are in preview and apply only within the Workforce Engagement Management app.

Learn about role descriptions, privileges, and assignment guidance in [Workforce management security roles](../administer/workforce-management-security-roles.md).

### Quality management roles

The Quality Admin, Quality Manager, and Quality Evaluator roles govern quality management access in the app.

Learn about role descriptions, privileges, and assignment guidance in [Quality management security roles](../administer/workforce-management-quality-management-security-roles.md).

## Known limitations

During preview, the app runs as a single-session app. Multisession experiences aren't supported.

## Related information

- [Install the Workforce Management for Customer Service package](../administer/workforce-management-package-installation.md)
- [Overview of workforce management](/dynamics365/customer-service/use/workforce-management-overview)
- [Workforce management security roles](../administer/workforce-management-security-roles.md)
- [Quality management security roles](../administer/workforce-management-quality-management-security-roles.md)
