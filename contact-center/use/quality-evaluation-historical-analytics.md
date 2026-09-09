---
title: Use the quality evaluation historical analytics dashboards
description: Quality evaluation historical analytics helps you track quality performance, spot trends, and understand evaluation outcomes. Learn how to enable and use the dashboard.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.date: 09/09/2026
ms.custom: bap-template
---


# Use the quality evaluation historical analytics dashboards

Use the quality evaluation historical analytics dashboards to review quality performance, analyze trends, and explore the factors that influence evaluation outcomes.

## Prerequisites

Your administrator has enabled the [quality evaluation historical analytics dashboard](../administer/manage-quality-evaluation-historical-analytics.md#manage-the-quality-evaluation-historical-analytics-dashboard).

## Access the dashboards

To access the dashboards:

1. In Copilot Service workspace, go to the **All evaluations** page.
1. Select **View Historical Analytics**. The quality evaluation agent historical analytics dashboards appear.

## Dashboards

You can access historical analytics for up to two years, and dashboard data refreshes every 24 hours. Role-based access controls ensure that users can access evaluations associated with their designated business unit only.

Historical analytics is available for the following dashboards:

- **Summary**: The **Summary** dashboard provides an overview of evaluation volume and quality performance. Use the available filters to analyze evaluation results across different channels, owners, evaluation methods, business units, and critical-question outcomes. The dashboard aggregates results based on the selected filters and helps you monitor quality trends over time.

- **Evaluation criteria**: The **Evaluation Criteria** dashboard helps you analyze performance across evaluation criteria and the individual sections within each criteria. The dashboard aggregates scores and evaluation volume based on the selected filters, allowing you to identify trends and areas that influence overall quality outcomes.

## Filter dashboard data

Use filters individually or in combination to analyze quality performance across different dimensions. You can also edit the dashboard to create your own visualizations and filters. Learn more in [Customize visual display](/dynamics365/customer-service/use/customize-reports).

| Filter | Description |
|---|---|
| Duration | Specify the period in which evaluations were completed, such as a month, quarter, or custom date range. |
| Channel | Filter evaluations by channel, such as case, conversation, or email. |
| Owner | Filter evaluations by evaluation owner. |
| Evaluation method | Filter by how evaluations were performed, such as AI agent, AI-assisted, or manual. |
| Business unit | Filter evaluations by the business unit associated with the evaluation owner. |
| Critical questions | Filter evaluations based on whether critical questions are included and whether the questions passed or failed. |

Use the **Evaluator Status** filter in the side filter pane to filter by the evaluator status.

## Metrics

The following metrics are common to both the **Summary** and **Evaluation criteria** dashboard.

- **Total Evaluations**: Displays the total number of evaluations that match the selected filters.
- **% of evaluations below threshold**: Displays the percentage of evaluations with scores below the configured threshold value.
- **Avg. quality score**: Displays the average quality score across all evaluations that match the selected filters.
- **% of evaluations with critical question failures**: The percentage of completed evaluations where at least one critical question was answered with a fail option. A failed critical question occurs when a question marked as **Critical** receives a response configured as **Fail**, causing the entire evaluation to fail regardless of its overall score.

## Summary metrics

Use the following charts to compare evaluation volume and quality scores across channels:

- **Total evaluations by channel**: Shows the number of evaluations completed for each channel. The chart categorizes evaluations by evaluation method, such as AI agent, AI-assisted, or manual.
- **Avg. quality score by channel**: Shows the average quality score for each channel. Use this chart to compare quality performance across case, email, and conversation channels.
- **Total evaluations by channel over time**: Shows changes in the number of evaluations completed for each channel over the selected period.
- **Avg. quality score by channel over time**: Shows changes in the average quality score for each channel over the selected period.

## Evaluation criteria metrics

Use the following key metrics to view a breakdown of evaluation performance by criteria and section.

- **Evaluation criteria**: Displays the evaluation criteria and the sections within each criteria. Expand or collapse a criteria to view section-level details.
- **Score**: Displays the aggregated score for the criteria or section.
- **Evaluation Volume**: Displays the number of evaluations included in the calculation.
- **% Above Threshold**: Displays the percentage of evaluations whose scores meet or exceed the configured threshold.
- **Weekly score columns**: Display the aggregated score for each reporting period, helping you track performance trends over time.

### Add a custom dashboard to sort records by the lowest score

To sort records based on their evaluation scores:

1. Edit the dashboard and add a new page.
1. Add a table visual, and then from the **FactEvaluationEntityName** table, add the following columns to the visual:
    - **EntityName**
    - **EntityRecordID**
1. Add **EvaluationScore** from the **FactEvaluationsExtension** table to the same visual.
1. Set the aggregation for **EvaluationScore** to **Average** because a single record can have multiple evaluation scores.
1. Select the **Average of EvaluationScore** column, and sort the records in ascending or descending order.

## Related information

[Manage the quality evaluation historical analytics dashboard](../administer/manage-quality-evaluation-historical-analytics.md)