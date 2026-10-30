---
title: Choose your Contact Center analytics reporting journey
description: Choose between built-in reports, visual customization, Power BI data model customization, and Microsoft Fabric for Dynamics 365 Contact Center analytics.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.date: 10/30/2026
ms.topic: overview
ms.custom: bap-template
---

# Choose your Contact Center analytics reporting journey

Dynamics 365 Contact Center provides built-in historical analytics and multiple ways to extend the reporting experience. The approach depends on whether you want to change only report presentation, build on Microsoft-defined analytics semantics, or work directly with data in Microsoft Fabric.

Start with the least complex option that meets your requirements. The options are independent; you don't need to complete each one.

| If you want to... | Choose this option | What you start with |
|---|---|---|
| Monitor standard contact center performance | [Use built-in analytics](#use-built-in-analytics) | Default reports and metrics |
| Change report pages, visuals, filters, themes, or layouts | [Customize report visuals](#customize-report-visuals) | A supported built-in report |
| Create measures, add data, or build reports while retaining default relationships and measures | [Customize the Power BI data model](#customize-the-power-bi-data-model) | Out-of-the-box semantic model and editable report copies |
| Use processed analytics tables for engineering, data science, SQL, notebooks, or a customer-owned model | [Extend analytics with Microsoft Fabric](#extend-analytics-with-microsoft-fabric) | Supported Delta tables exposed through a separately configured shortcut |

> [!IMPORTANT]
> Power BI data model customization and Fabric shortcuts are separate capabilities. Enabling or provisioning Power BI data model customization doesn't create a Fabric lakehouse, shortcut, connection, or permission to the underlying storage.

## Prepare Contact Center analytics

Before using any reporting option, you must [enable Contact Center historical analytics](enable-contact-center-analytics.md) and give users the required access. Analytics data can take up to 24 hours to become available after the feature is enabled.

## Use built-in analytics

Built-in reports provide default visualizations and metrics without requiring your organization to develop or maintain a reporting solution.

| Analysis goal | Report | Metric reference |
|---|---|---|
| Review interaction volume, engagement, outcomes, and service performance | [Conversation dashboard](../use/conversation-dashboard.md) | [Conversation metrics](../use/conversation-metrics.md) |
| Examine queue entries, transfers, wait time, handling, and abandonment | [Queue dashboard](../use/queue-segments-dashboard.md) | [Queue metrics](../use/queue-segment-metrics.md)|
| Review representative performance, availability, and capacity | [Agent dashboard](../use/contact-center-agent-dashboard.md) | [Session metrics](../use/session-metrics-dashboard.md), [availability metrics](../use/availability-metrics.md), and [capacity metrics](../use/capacity-metrics-dashboard.md) |
| Analyze voice operations and call-specific insights | [Voice dashboard](../use/voice-dashboard.md) | [Voice insight metrics](../use/voice-insight-metrics.md) |

A conversation can contain multiple sessions and queue segments. Use conversation metrics for the complete interaction, session metrics for individual participation or handling stages, and queue segment metrics for movement through queues.

Choose another option only when the built-in presentation or model doesn't meet your requirements.

## Customize report visuals

Choose visual customization when the existing data and metrics meet your needs, but you want to change how they're presented. For supported reports, users with the **Analytics Report Author** security role can use the embedded Power BI editor to customize:

- Charts and other visualizations.
- Page layouts, themes, and formatting.
- Filters and slicers.
- Report pages and navigation.

Visual customization doesn't add a data source or change the underlying metric calculations. Published changes apply to users across the organization.

For supported reports, limitations, publishing instructions, and reset behavior, see [Customize visual display of analytics reports](/dynamics365/customer-service/use/customize-reports).

If you need a new measure, another data source, a new report, or lifecycle control in your own workspace, choose Power BI data model customization.

## Customize the Power BI data model

Customizing the Contact Center historical data model provides a supported Power BI extensibility path. After an administrator explicitly enables and configures the feature, the provisioning process:

1. Creates or reuses the required service-managed workspaces.
1. Deploys the default contact center semantic model.
1. Creates or uses the customer-selected workspace.
1. Deploys editable copies of the available Conversation, Agent, Queue, and Voice reports.
1. Configures refresh for the managed artifacts.

The default semantic model contains predefined relationships and measures over processed contact center analytics data. Report authors can use the model to:

- Create organization-specific DAX measures and reports.
- Change report pages, visuals, filters, and formatting.
- Add Dataverse or external data through a downstream composite model.
- Publish reports to the configured customer workspace.
- Register supported reports for the Dynamics 365 **Customized Reports** experience.

> [!NOTE]
> Availability of the customization option doesn't mean that it's already enabled or provisioned. Enable the Contact Center historical data model customization feature, select a workspace, and complete the required Power BI and Fabric configuration.

### Prepare for Power BI customization

Before you build custom reports:

1. Review the [unified analytics data model](../extend/overview-data-model.md) to understand the dimensions, facts, aggregates, and metric definitions.
1. Review [how Power BI data model customization works](/dynamics365/customer-service/use/datamodel-overview).
1. Confirm that at least one applicable Contact Center analytics feature is enabled and successfully provisioned.
1. Confirm the required [licenses, permissions, Microsoft Entra security group, Fabric capacity, and tenant settings](/dynamics365/customer-service/administer/model-customize-reports).
1. Give report authors access to the customer workspace and Build permission on the managed semantic model.
1. Use a separate customer workspace for each Dynamics 365 environment. Don't link the same workspace to multiple environments.
1. Follow [Use the Power BI data model to create custom reports](/dynamics365/customer-service/use/use-datamodel) to create measures, add data, and build reports.

Keep custom measures, tables, relationships, and reports in the downstream customer model and customer workspace. Treat the default semantic model and service-managed workspaces as read-only.

Your organization owns the lifecycle of report customization. Manage access, capacity, refresh, testing, deployment, and updates. Microsoft can update the managed semantic model.

When moving a report between environments, repoint it to the destination environment's managed semantic model before publishing it to the destination customer workspace. Use lineage view to verify that each customer model and report connects to the correct managed model.

For schema and field details, see the [Contact center analytics data model](../extend/overview-data-model.md).

## Extend analytics with Microsoft Fabric

Choose Microsoft Fabric when data engineers and analytics teams need supported processed Contact center tables for cross-domain analysis, data engineering, data science, SQL, notebooks, or a fully customer-owned semantic model.

A Fabric shortcut exposes data in OneLake without copying the source files. Unlike Power BI data model customization, a shortcut provides access to selected data tables, not a ready-made contact center reporting solution.

| Capability | Power BI data model customization | Fabric shortcut |
|---|---|---|
| Starting point | Out-of-the-box semantic model and editable report copies | Selected Delta tables or folders |
| Microsoft-defined relationships and measures | Included | Not included |
| Conversation, Agent, Queue, and Voice report copies | Included when the corresponding packages are available | Not included |
| Dynamics 365 **Customized Reports** integration | Supported for reports in the configured customer workspace | Not automatic |
| Typical tools | Power BI and composite models | Lakehouse, Spark, SQL, notebooks, and customer-owned semantic models |
| Provisioning | Performed through the contact center customization setup | Configured separately by the customer |
| Ownership | Microsoft manages the base model; the customer manages custom artifacts | The customer manages the complete downstream solution |

> [!IMPORTANT]
> A Fabric shortcut isn't created by Contact center historical data model customization. Shortcut use requires separate product entitlement or onboarding, a customer-owned Fabric workspace and lakehouse, a supported data location, a connection identity, and permission to read the target.

### Connect to processed Contact center analytics tables

If your organization is entitled and onboarded for access to processed contact center analytics data:

1. Review [OneLake shortcuts](/fabric/onelake/onelake-shortcuts) and [OneLake shortcut security](/fabric/onelake/onelake-shortcut-security).
1. Prepare a customer-owned Fabric workspace and lakehouse with the required capacity, tenant settings, and access controls.
1. Obtain the supported tenant-specific data location and authentication method through the product onboarding or administration experience. Don't connect to service-owned staging or internal data.
1. Create shortcuts only for documented customer-visible tables. Use the [Contact center analytics data model](../extend/overview-data-model.md) to identify the tables you need and confirm their availability.
1. Treat shortcut-backed source data as read-only. Store transformations, curated data, and cross-domain joins in separate customer-owned tables or schemas.
1. Build and secure a customer-owned semantic model. Reimplement and validate required business calculations because the default model's relationships and measures aren't supplied with the shortcut.
1. Validate table grain, relationships, totals, freshness, schema changes, downstream queries, security, and capacity consumption before publishing production assets.

Deleting a shortcut doesn't delete its target data. However, source schema changes can flow through the shortcut and affect downstream solutions. Plan for compatibility testing and change management.

### Connect to source Dataverse tables

Use a Dataverse shortcut when you need source Dataverse tables in the same Fabric solution. This connection is separate from a processed contact center analytics shortcut and doesn't provide processed analytics tables, the default semantic model, or its measures.

The Dataverse tables must be available in Dataverse Managed Lake. You must configure an application identity, authorize it in each Dataverse environment, and use its credentials to create the Fabric connection.

Learn more about prerequisites, security guidance, and the complete procedure in [Connect Microsoft Fabric to Dataverse by using a service principal](../extend/connect-dataverse-shortcut.md).

Fabric-built reports aren't automatically added to Dynamics 365. Distribute them through Fabric or Power BI unless they use the configured customer workspace and are supported by the Dynamics 365 report-registration experience.
