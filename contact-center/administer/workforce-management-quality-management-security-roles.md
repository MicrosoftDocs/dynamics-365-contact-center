---
title: Quality management security roles in the Workforce Engagement Management app (preview)
description: Learn how to choose and assign quality management security roles and compare their privileges in the Workforce Engagement Management app.
ms.date: 09/18/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.custom:
  - bap-template
---

# Quality management security roles in the Workforce Engagement Management app (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

Three security roles govern quality management access in the Workforce Engagement Management app: Quality Admin, Quality Manager, and Quality Evaluator. These roles also govern quality management outside the app. If you already use quality management, your existing role assignments apply in the app.

Use this article to compare privileges, choose a role, and assign it to a user.

> [!IMPORTANT]
> Assigning these roles also affects quality management access outside the Workforce Engagement Management app. Review a role's privileges before you assign it.

## Available roles

| Role | Intended users |
| --- | --- |
| Quality Admin | Administrators who configure quality management and need full access, including screen recording download and deletion. |
| Quality Manager | Quality managers who define evaluation criteria, plans, and governance policies and oversee evaluation outcomes. |
| Quality Evaluator | Evaluators who complete and assign evaluations against defined criteria. |

## Privileges by capability

The following tables list the privileges assigned to each role.

### Screen recording

| Privilege | Quality Admin | Quality Manager | Quality Evaluator |
| --- | --- | --- | --- |
| Create a screen recording | No | No | No |
| Play back a screen recording | Yes | Yes | Yes |
| Download a screen recording | Yes | No | No |
| Delete a screen recording | Yes | No | No |

All three roles can play back screen recordings, but none can create them. Only Quality Admin can download or delete screen recordings. Downloading moves recorded material outside its original context, and deleting removes it permanently.

### Evaluation criteria

| Privilege | Quality Admin | Quality Manager | Quality Evaluator |
| --- | --- | --- | --- |
| Create evaluation criteria | Yes | Yes | No |
| Read evaluation criteria | Yes | Yes | Yes |
| Write evaluation criteria | Yes | Yes | No |
| Delete evaluation criteria | Yes | Yes | No |
| Run a simulation | Yes | Yes | No |
| Extend criteria | Yes | Yes | No |

### Evaluation plans

| Privilege | Quality Admin | Quality Manager | Quality Evaluator |
| --- | --- | --- | --- |
| Create an evaluation plan | Yes | Yes | No |
| Read an evaluation plan | Yes | Yes | No |
| Write an evaluation plan | Yes | Yes | No |
| Delete an evaluation plan | Yes | Yes | No |

### Evaluations

| Privilege | Quality Admin | Quality Manager | Quality Evaluator |
| --- | --- | --- | --- |
| Create an evaluation | Yes | Yes | Yes |
| Read an evaluation | Yes | Yes | Yes |
| Write an evaluation | Yes | Yes | Yes |
| Delete an evaluation | Yes | Yes | No |
| Assign an evaluation | Yes | Yes | Yes |
| Override a submitted evaluation | Yes | Yes | No |
| Inactivate an evaluation | Yes | Yes | No |

Quality Evaluator can create, complete, and assign evaluations, but can't delete them, override submitted evaluations, or inactivate them. Quality Admin and Quality Manager retain those privileges so that completed evaluation records remain auditable.

### Governance

| Privilege | Quality Admin | Quality Manager | Quality Evaluator |
| --- | --- | --- | --- |
| Create a governance policy | Yes | Yes | No |
| Read a governance policy | Yes | Yes | No |
| Write a governance policy | Yes | Yes | No |
| Delete a governance policy | Yes | Yes | No |
| Run a simulation | Yes | Yes | No |
| Read violation logs | Yes | Yes | No |
| Read governance execution status | Yes | Yes | Yes |

Only Quality Admin and Quality Manager can create and review governance policies. All three listed roles can read governance execution status. Quality Evaluator can check whether a policy check ran against an interaction without access to the policy definition or violation logs.

### Administration

Only Quality Admin can open **Admin settings** and configure quality management. Settings cover quality evaluation, governance, and screen and call recording.

## Choose a role

| If the user needs to | Assign this role |
| --- | --- |
| Configure quality management, or download or delete screen recordings | Quality Admin |
| Define evaluation criteria, plans, and governance policies | Quality Manager |
| Complete and assign evaluations against existing criteria | Quality Evaluator |

A user can have multiple roles. Assign a workforce management role as well if the user needs access to both the quality management and workforce management areas of the app. Read [Workforce management security roles](workforce-management-security-roles.md).

## Assign a role to a user

1. Sign in to the Power Platform admin center.
1. In the site map, select **Environments**, and then select your environment.
1. Select **Settings** > **Users + permissions** > **Users**.
1. Select the user to update, and then select **Manage security roles**.
1. Select the quality management role to assign.
1. Select **Save**.

The Workforce Engagement Management app appears in the user's list of apps the next time they sign in.

## How role assignment affects app visibility

Users must have a quality management role listed in this article or a workforce management role to access the app. Users without one of these roles don't have the app in their list of apps.

Learn more in [Workforce Engagement Management app](../use/workforce-management-wem-app-overview.md).

## Related information

- [Workforce Engagement Management app](../use/workforce-management-wem-app-overview.md)
- [Workforce management security roles](workforce-management-security-roles.md)
