---
title: Manage coaching and development (preview)
description: Manage coaching and development in Workforce Engagement Management (preview). Set up scorecards, review AI insights, and assign training to your team. Learn how.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 11/17/2026
ms.custom: bap-template
---

# Manage coaching and development (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Set up coaching and development for your business units on the **Coaching setup** page in the Workforce Engagement Management (preview) app. Define coaching instructions, configure scorecards, review coaching insights, publish scorecards and assign training.

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- An administrator enabled the required coaching and development capabilities.
- You have the **Quality Manager** security role.
- You have access to the business units and representatives that you manage.

You see only the business units that you're authorized to access. Representative visibility and assignment scope depend on the business units and representatives that you manage.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Set up scorecards

1. In the site map of Workforce Engagement Management (preview) app, go to **Coaching setup**, and then select the **Scorecards** tab.
1. In **Scorecard settings**, select **Add business unit**.
1. In the **Manage scorecard settings** dialog box, in **Scorecard details**, select the following settings:
    - **Business unit**: Select one or more business units. Keep the default scorecard settings or edit them.
    - **Schedule**: Select how often scorecards update. **Weekly** scorecards are based on the previous week's conversations and cases. **Monthly** scorecards are based on the previous month's conversations and cases.
    - **Scorecard information**: Select **Quantitative data** to include performance KPIs and metrics, **AI insights** to include AI-generated coaching insights and feedback, or both.

        If you include AI insights, select **Review required** (recommended) so that managers must review AI insights before they share them with representatives, or select **No review** to make AI insights available to representatives right away.
1. Select **Next**.
1. In **Representative selection**, select the representatives who receive scorecards in the business unit.
1. Save the settings.

> [!NOTE]
> Feedback between supervisors and representatives is included in scorecards automatically. Microsoft Copilot credits are consumed when AI insights are generated.

## Use the coaching dashboard

In the site map of Workforce Engagement Management (preview), go to **Coaching & development**, select the **Coaching** tab, and then select a **Business unit** and scorecard period. Use the dashboard to review:

- **Needs your attention**: Scorecards pending your review, lowest scores first, and published scorecards that representatives didn't acknowledge.
- **Team quality scores**: Average quality score by record type, change from the previous period, and target status.
- **Coaching insights**: AI-generated summaries of team trends. Rate an insight as **Helpful** or **Not helpful**.
- **Representatives' scorecards**: Scorecard status, record-type scores, and evaluation counts. Filter by **Returned**, **Pending review**, or **Published**.

> [!NOTE]
> Copilot summarizes trends across the selected business unit for the period. AI-generated content might be incorrect. Ensure AI-generated content is accurate and appropriate before you use it. Scores reflect the interactions a representative took part in and might not be based only on their contributions.

### Review and publish scorecards

If review is required, the system creates scorecards with **Pending review** status. Perform the following steps:

1. Open a representative's scorecard.
1. Review the coaching overview, insights, opportunities for growth, and scores.
1. Edit or remove AI-generated insights as needed.
1. Add comments.
1. Publish the scorecard.

| Scorecard status | Description |
|---|---|
| Pending review | The scorecard is waiting for the supervisor to review and publish. |
| Published | The scorecard is available to the representative and awaits acknowledgment. The status shows as **Awaiting acknowledgment** until the representative acknowledges it. |
| Acknowledged | The representative confirmed that they reviewed the scorecard. Acknowledgment doesn't imply agreement and doesn't complete assigned training. |
| Returned | The representative returned the scorecard with comments for supervisor follow-up. |

## View impact

On the **Coaching & development** page, select the **Impact** tab, and then select a business unit and period. Review the following:

- **Team performance trends**: Daily average quality, with markers for when scorecards were published and training was completed.
- **Before, after, and follow-up**: Quality at baseline (before coaching), after training completion, and at a later follow-up, with the change and its 95% confidence interval.
- **Impact distribution**: How many representatives improved, showed little change, or declined.
- **Representative impact**: Each representative's baseline, follow-up, change, number of evaluations, and the coaching and training they received.
- **Insights and recommended actions**: Copilot-generated observations based on these figures, with suggested next steps.

> [!IMPORTANT]
> The impact view shows observed changes. It doesn't prove that coaching or training caused them.

## Create and assign training

On the **Coaching & development** page, select the **Training** tab. The **Training** page includes **Assignments** and **Training library** views.

You can assign the following training types to representatives, depending on what you want them to learn or practice.

| Training type | Description |
|---|---|
| Knowledge article review | The representative reviews one or more knowledge articles. |
| Knowledge check | A quiz generated from knowledge articles that checks the representative's understanding.  |
| Scenario-based training | An AI coach simulates a customer and provides feedback during practice. |

### Assign training and track progress

Assign published training from a recommended action or **Assignments**.

1. On the **Training** tab, select **Assignments** > **New training assignment**.
1. In **New training assignment**, select the training type and the source material in **Training content**.
1. In **Assignment details**, provide the following information:
    - **Assignment name**: Enter the assignment name.
    - **Assign to**: Select the representative you want to assign the training to.
    - **Requirement**: Set the assignment as **Required** or **Recommended**.
    - **Due date**: Specify a due date. Use **Assignments** to update due dates, edit assignments, cancel assignments, and track progress.
1. Select **Assign training** or **Save draft**.

| Assignment status | Description |
|---|---|
| Not started | The training is assigned, and the representative didn't start it.  |
| In progress | The representative started the training. |
| Overdue | The due date passed before the representative completed the training.  |
| Completed | The representative completed the training. Scenario-based training is marked complete automatically when the representative finishes the practice. Completion is tracked, but scenario-based training isn't scored as pass or fail.  |
| Cancelled | The assignment was withdrawn. It's excluded from overdue counts but remains visible in history. |

Scorecard acknowledgment and training completion are tracked independently. Acknowledging a scorecard doesn't complete training, and completing training doesn't change the scorecard status.

### Create training

1. On the **Training** tab, select **Training library** > **Create training**.
1. In **Source material**, select one or more **Internal knowledge articles**. You can also add **Attachments**. You must add at least one knowledge article or attachment before you can generate training.
1. In **Training details**, enter the following information:
    - **Training type**: Select **Knowledge check** or **Scenario-based training**.
    - **Training name**: Enter a name for the training.
    - **Development focus**: Select the opportunity for growth that the training addresses. Suggestions come from your team's opportunities for growth. Each training has one development focus.
    - **Context & instructions**: Describe the scenario, behaviors, or knowledge that the training should cover.
1. Select **Generate training**. Copilot generates editable training content from your source material. To finish later, select **Save draft**.
1. Review and edit the generated content.
1. Select **Publish**. Published training is available to assign and reuse.

> [!IMPORTANT]
> You can assign only published training. Review AI-generated training for accuracy and appropriateness before publishing it.

## Related information

[Overview of coaching and development (preview)](overview-coach-development.md)  
[Set up coaching and development (preview)](../administer/setup-coach-development-admin.md)  
[Use coaching and development (preview)](use-coach-development-representative.md)
