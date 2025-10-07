---
title: Configure Quality Evaluation Agent in Dynamics 365
description: Learn how to configure and enable the Quality Evaluation Agent to improve customer engagement and ensure compliance with evaluation standards.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.date: 10/07/2025
ms.topic: how-to
---

# Quality Evaluation Agent


> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and should not be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.


## Introduction

> [!NOTE]
> The Quality Evaluation Agent is an AI agent that assesses customer engagement using an evaluation framework defined by supervisors. The Quality Evaluation Agent autonomously scores cases and conversations, providing insights to help supervisors enhance the quality of case and conversation interactions.
>
> The Quality Evaluation Agent evaluates cases and closed conversations to check if representatives follow required standards. If standards aren't met, the Quality Evaluation Agent provides coaching recommendations or actions to help representatives improve.
>
> The Quality Evaluation Agent includes the evaluation criteria, evaluation plan, and evaluations. These components are essential for the Quality Evaluation Agent to work.

###### Evaluation Criteria:

> Supervisors can create a form with questions, answer choices, scoring
> metrics, and detailed instructions for the Quality Evaluation Agent.
> They can use this form to assess interactions. The Quality Evaluation
> Agent predicts responses and assigns quality scores, giving insights
> into the overall quality score of the contact center.

###### Evaluation Plan:

> Supervisors can set up plans to schedule when to evaluate
> interactions. They can choose interactions based on specific
> conditions and use the right evaluation criteria to review them
> systematically.

###### Evaluations:

> The Quality Evaluation Agent summarizes case and conversation
> evaluations in customer service and highlights action plans and
> recommendations. These insights help AI supervisors improve service
> quality.

## Prerequisites

##### You have the Quality Manager, Quality Evaluator, and the Quality Admin role.

##### You have configured the [<u>connection references</u>.](#_bookmark5)

##### You provided consent for potential data movement across regions. Learn more in [FAQ.](#faq)

## Role and Privileges


| Persona      | Role            | Privileges                                                                 |
|--------------|-----------------|---------------------------------------------------------------------------|
| Administrator| Quality Admin   | Configure Quality Evaluation Agent<br>Create evaluation criteria, evaluation plan<br>Complete or assign an evaluation. |
| Supervisor   | Quality Manager | Create evaluation criteria, evaluation plan<br>Complete or assign an evaluation |
| Supervisor   | Quality Evaluator| Complete or assign an evaluation.                                         |

## Configure connection references

> Configure connection references for the Quality Evaluation Agent flow.
> You need to set the following connection references:

- **QEA On Demand Evaluation Case** for cases.

- **AI Evaluation Flow for Conversation** for conversations.

> Learn more in [<u>Add connection references to a
> solution.</u>](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/create-connection-reference#add-connection-references-to-a-solution)

### Set connection references for Quality Evaluation Agent flow

1.  Sign in to
    [<u>make.powerapps.com</u>](https://make.preview.powerapps.com/) and
    select your environment.

###### Go to Solutions \> Default Solution \> Objects \> Connection References.

3.  Search for the following connection references:

###### For cases: QMA.Incident.DVPluginConnection, Microsoft Copilot Studio (Preview)

###### CaseReviewerFlow and Microsoft Dataverse FlowRunTest-8625a

2.  For conversations: **Microsoft Dataverse CDS Connection for QEA
    Conversation, Microsoft**

> **Copilot Studio (Preview) CaseReviewerFlow** and **Microsoft
> Dataverse FlowRunTest-8625a**

4.  To create a connection for **QMA.Incident.DVPluginConnection**:

    1.  In the **Edit** dialog, select **Connection \> New connection.**

    2.  Search for **Microsoft Dataverse**, select **Create** and sign
        in using the **OAuth connection** type to create a Dataverse
        connection.

    3.  Repeat to create a connection for **Microsoft Copilot Studio
        (preview)**.

    4.  Go back to the **Edit** dialog of
        **QMA.Incident.DVPluginConnection**, search for the new
        connection and save it.

5.  Save your changes.

#### Repeat steps 4-6 for Microsoft Dataverse CDS Connection for QEA Conversation and Microsoft Copilot Studio (Preview) CaseReviewerFlow.

### Turn on the flow

> In [<u>Power Apps</u>,](https://make.preview.powerapps.com/) from
> **Solutions** \> **Default Solution** \> **Objects** \> **Cloud
> flows**, select **QEA On Demand Evaluation Case** and **AI Evaluation
> Flow for Conversation,** and then select **Turn on**.
>
> Alternatively, in [<u>Power
> Automate</u>,](https://powerautomate.microsoft.com/) search for **QEA
> On Demand Evaluation Case** and the **AI Evaluation Flow for
> Conversation** in **Cloud flows,** and turn these on. Learn more in
> [<u>Power
> Automate</u>.](https://learn.microsoft.com/en-us/power-automate/overview-cloud#find-your-flows-easily)

### Publish the Microsoft Copilot Studio agent

1.  In [<u>Microsoft Copilot
    Studio</u>,](https://copilotstudio.microsoft.com/) select your
    environment, and then search for the **Quality Evaluation Agent -
    Incident** case agent and the
    **QualityEvaluationAgentForConversation** conversation agent.

2.  [<u>Publish the
    agent</u>.](https://learn.microsoft.com/en-us/microsoft-copilot-studio/publication-fundamentals-publish-channels?tabs=web)

> Once done, go to the Copilot Service admin center and enable the
> <u>Quality Evaluation Agent</u>.

## Enable Quality Evaluation Agent

> As an administrator, you need to enable Quality Evaluation Agent for
> your supervisors from the Copilot Service admin center. You can select
> cases or conversations record type, as required. You can also set a
> scoring and a threshold value. Each criteria and question in the
> evaluation is scored out of 100 points. You can set thresholds to
> define good and poor-quality metrics.

1.  In the Copilot Service admin center application, go to **Customer
    Support** \> **Quality Management.** The **Quality management** page
    appears.

2.  Select **Manage** for **Quality Evaluation Agent (preview)**. The
    **Quality Evaluation Agent (preview) page** appears.

3.  In the **Enablement by record type** section:

##### Select the **Case** checkbox for case evaluation.

##### In **Specify data**, you see the default entities that have been added.

2.  Select **Manage data** if you want to,

##### Delete data types or uncheck a row to temporarily exclude the data type from being summarized.

##### Add more data type fields for Quality Evaluation Agent input configuration. Select **Add data** in the **Specify data** dialog box, and then select **Save.**

2.  Select the **Conversation** checkbox for a conversation evaluation.

<!-- -->

4.  In the **Evaluation criteria score** section, select the **Enable
    scoring for criteria** checkbox. The

> **Evaluation criteria scoring turned on** dialog appears.

##### Select **Turn on**. Once turned on, it can’t be turned off.

6.  From the **Set threshold value out of 100** dropdown list, select a
    threshold value.

7.  Select **Save**.

## Evaluation criteria

### Use the out-of-the-box evaluation criteria

> As a quality evaluation supervisor, you can use the default evaluation
> criteria, copy the default evaluation criteria, or create a new
> evaluation criteria to evaluate your cases and conversations.
>
> Use the **Support quality** evaluation criteria for both cases and
> conversations. Use the **Closed Conversations Default Criteria** for
> conversations only.
>
> **Note:** The default evaluation criteria is pre-filled, published and
> read-only.

1.  In Copilot Service workspace, go to Evaluation **criteria.**

##### On the **Evaluation criteria** page, depending on your record type, select the default evaluation criteria, as required.

### Extend evaluation criteria

> After you create a baseline criteria for your business unit, you can
> extend it to fit your organizational requirements. Updates to the
> baseline criteria automatically appear in all extended criteria.
> Select any custom evaluation criteria in the **Published** state as
> source criteria to extend it further.

1.  Select a criteria and then select **Extend criteria**. The \<*new
    extended*\> evaluation criteria page appears.

2.  In the **Extended criteria details** section, enter the following
    details:

    1.  **Criteria name**: Provide a name.

    2.  **Description**: Provide a description. To provide your own
        instructions, turn off the **Use source instructions** toggle.
        To use the source instructions, turn on the **Use source
        instructions** toggle.

    3.  **Extended scoring weight**: If the source criteria has scoring
        criteria enabled, provide the extended scoring weight.

    4.  **Source scoring weight**: Gets auto calculated, depending on
        the extended scoring criteria.

3.  Select **Add question** to add questions to the extended criteria.

4.  Select **Save** and then select **Publish**.

> **Note**:

- The **Source criteria details** in the **Extended criteria details**
  page isn’t editable.  
  However, if you make updates to the source criteria, the extended
  criteria is updated as well.

- The **Criteria scoring** reflects the selection you made in the source
  criteria.

- You can’t extend an out-of-the-box criteria, for example, **Support
  quality**.

### Copy the default quality evaluation criteria for cases and conversations

##### Select the checkbox for the default criteria and then select **Copy**. A copy of the prefilled default criteria form is provided to you as the source. You can make edits as needed.

##### Select **Save**, once you are done making edits.

### Create a scoring evaluation criteria

1.  On the **Evaluation criteria** page, select **New**.

2.  On the **New evaluation criteria** page, in the **Criteria details**
    section, provide the **Criteria name**

> and **Description**.

3.  In the **Add form level instructions**, provide instructions, if
    any.

4.  In **Section 1**, enter the following details:

    1.  **Section name**: Provide a name.

    2.  **Description**: Provide a description.

##### **Section weight (%)**: Provide a weightage for the evaluation criteria. The weight % across sections should add up to 100.

4.  Select **Add question,** if you want to add a question.

##### For every question,

1.  **Select answer type**: Select from the options, **Yes/No**,
    **Multiple choice**, **Choose from list**, or **Text selection**.

2.  **Form question text**: Enter the form question text.

##### **Add question-level instructions**: Provide instructions for the question, if any. Instructions help Quality Evaluation Agent predict answers and improve accuracy.

##### Depending on the answer type you select, you can add scoring for the answers by selecting the **Scoring enabled** checkbox.

5.  For **Answer options,** depending on the answer type you select, the
    answer options appear. Provide **answer-level instructions** for
    your answers, as required.

<!-- -->

6.  You can select **Delete section** or **Duplicate section** or
    **Delete question** or **Duplicate question** for sections or
    questions, respectively.

7.  Select **Save** and then select **Publish**.

### Best practices

- **Criteria-level instructions:** Define instructions that apply to the
  entire evaluation criteria. Include overarching goals, expectations,
  and constraints to guide Quality Evaluation Agent behavior across all
  questions and answers.

- **Question-level instructions**: Provide specific instructions for
  each question to guide the Quality Evaluation Agent’s evaluation.
  These instructions are scoped to the question only, and don’t
  influence other parts of the evaluation.

- **Answer-level instructions**: Include answer-specific instructions
  for each answer option to help the Quality Evaluation Agent understand
  the intent and context of the response.

- **Answer choices**: Clearly define answer options, especially for
  multi-choice or list-type questions. Ensure that you include fallback
  options to handle ambiguous or unexpected responses.

- **Clarity drives accuracy**: Use precise and detailed instructions to
  improve the accuracy of Quality Evaluation Agent evaluations. Avoid
  vague language and ensure that all instructions are explicit,
  contextual, and actionable.

- **Question text**: Define each evaluation question to assess a single,
  well-defined objective to help ensure clarity and direct alignment
  with the answer options.

## Evaluation plan

> The evaluation plan lets supervisors define the frequency, conditions,
> criteria, and methods for evaluation. This plan helps ensure that
> evaluations are systematic and consistent. The three evaluation
> methods are AI agent, AI-assisted, and manual.

### Create and activate evaluation plan for conversations

> **Note**: You can use conversation evaluations for voice and live chat
> channels only.

1.  In Customer Service workspace, go to **Evaluation Plans**.

2.  On the **Evaluation plans** page, select **New**.

3.  On the **New Evaluation Plan** page,

    1.  In the **Evaluation plan details** section, provide the
        following:

        1.  **Plan name**: Enter plan name.

        2.  **Description**: Enter description.

        3.  **Record type**: Select **record type** as
            **Conversations.**

    2.  In the **Frequency** section,

        1.  **Frequency type:** Select **Trigger,** and then provide the
            following:

            1.  **Event**: If you have frequency type as **Trigger**,
                then select **Closed conversation**.

            2.  **Start date**: Provide a start date.

            3.  **End date**: Provide an end date.

    3.  In the **Conditions** section, select **Add** to add conditions
        to your evaluation plan. For example, Add **Conversation
        status** \> **Equals** \> **Closed** or add **Channel type \>
        Contains data \> Live chat.**

    4.  In the **Assign evaluation** section, provide the following:

        1.  **Evaluation criteria:** Select the criteria from the
            dropdown. Example, select

#### Closed Conversations Default Criteria.

2.  **Evaluation method:** Select from **AI assisted, AI agent**, or
    **Manual.**

3.  If you select the **AI assisted** option, from the **Assigned To**
    dropdown list, you need to select **Team** or **User**.

4.  **Due date**: Select a due date.

<!-- -->

4.  Select **Save**.

5.  Select **Activate plan**. The A**ctivate plan** dialog appears.
    Select **Activate plan**. On successful activation, a success
    message appears.

### Activate, pause, or delete the evaluation plan in bulk

1.  In Customer Service workspace, go to **Evaluation plans**.

##### On the **Evaluation Plans** page, select the evaluation plans that you would like to activate or pause in bulk.

3.  Select **Activate plan, Pause plan,** or **Delete**. On the
    respective dialog box, confirm the action and save.

### On-demand evaluation

> The on-demand evaluation feature allows users to request evaluations
> for specific cases.
>
> To request evaluations for multiple cases from the case grid:

##### Select the required records.

2.  Select **Request evaluation**.

> **Note:** You can select up to 20 records for evaluation. To request
> evaluation for a particular case:

1.  Go to **Cases**, select the required case, and then select **Request
    evaluation**.

2.  On the **Request evaluation** dialog, select the following:

    1.  **Evaluation criteria:** Search and select an evaluation
        criteria from the list of criteria.

    2.  **Evaluation method:** Select an evaluation method.

    3.  **Assigned to:** Select the user.

    4.  **Evaluation due date:** Select a due date for the evaluation.

3.  Select **Request**.

4.  Once the AI agent status appears as **Completed,** on the
    **Evaluation associated view**, you can review the **Evaluation
    Summary** provided by Copilot.

5.  Select **Submit and Close**. The **Evaluator status** appears as
    **Completed**.

## Evaluations

> The **Evaluations** side pane shows evaluations for cases and closed
> conversations.

- **Evaluation Summary:** Highlights evaluation results and suggests
  actions for improvement, like coaching opportunities for
  representatives or specific activities to bring a case back on track.
  The Quality Manager and Quality Reviewer base these actions on
  evaluation results to improve the overall quality.

> You can view specific data by using filters such as **Evaluation
> method**, **AI agent status**, **Evaluator status**, **Evaluator due
> date**, **Evaluator Completion date**.

1.  In Copilot Service workspace, go to **Evaluations**. The **All
    evaluations** data grid appears.

2.  Select the required case or conversation record type.

3.  The case or conversation appears with the **Evaluation Summary** and
    **Suggested actions.**

- **Scoring overview:** You see this overview if you have extended your
  evaluation criteria. Shows the **Overall evaluation score**,
  **Compliance score**, and the **Quality and compliance score**,
  including the **Total score** and **Scoring ratio**.

- **Compliance:** Shows the **Total score** with a **Scoring
  breakdown.** For every question, you see a **About this answer** that
  shows you the question-level calculation breakdown.

- **Quality compliance:**

### Evaluation states

> You see the following evaluator and AI agent states on the grid.

###### Evaluator status:


| State           | What it indicates                                                                 |
|-----------------|----------------------------------------------------------------------------------|
| Pending         | The evaluation hasn’t started.                                                    |
| In-progress     | The evaluator is filling in the evaluation                                        |
| Completed       | The evaluator has finished and submitted the evaluation.                          |
| Expired         | The due date provided in the evaluation criteria has expired, and the evaluator can no longer open the evaluation. |
| Not applicable  | The AI agent is in Error status, and therefore the evaluator can’t evaluate.      |

#### AI agent status:

| **State** | **What it indicates** |
|----|----|
| **Pending** | The evaluation hasn’t started. |
| **In-progress** | Evaluation is in progress |
| **Completed** | Evaluation is complete. |
| **Error** | AI agent shows errors due to issues. |
| **Not applicable** | Evaluation isn’t using an AI agent and a manual review is performed. |

## FAQ

**Q: What does private preview offer in terms of participation and data
movement guidance?**

**Ans:** As part of the private preview for quality management
solutions, we are excited to offer early access to its innovative
capabilities. To ensure optimal performance, service calls may be routed
outside the customer's regional boundary if local capacity is
temporarily unavailable.

To participate, customers are kindly requested to provide consent for
potential data movement across regions. This enables us to deliver a
seamless experience leveraging the full capabilities of Copilot and
generative AI features within the Power Platform.

If a customer prefers to keep data strictly within their region, we
respect that choice and recommend waiting for broader availability
before enabling the preview.

Learn more in [Move data across regions for Copilots and generative AI
features – Power Platform \| Microsoft
Learn](https://learn.microsoft.com/en-us/power-platform/admin/geographical-availability-copilot?utm_source=chatgpt.com&tabs=new).

# Preview disclaimer

> Preview features are features that aren’t complete but are made
> available on a “preview” basis so customers can get early access and
> provide feedback. Preview features are not supported by Microsoft
> Support, may have limited or restricted functionality, aren’t meant
> for production use, and may be available only in selected geographic
> areas.

# Copyright

> This document is provided "as-is". Information and views expressed in
> this document, including URL and other Internet web site references,
> may change without notice.
>
> Some examples depicted herein are provided for illustration only and
> are fictitious. No real association or connection is intended or
> should be inferred.
>
> This document does not provide you with any legal rights to any
> intellectual property in any Microsoft product. You may copy and use
> this document for your internal, reference purposes. This document is
> confidential and proprietary to Microsoft. It is disclosed and can be
> used only pursuant to a non- disclosure agreement.
>
> © 2025 Microsoft. All rights reserved.
>
> Microsoft is trademark of the Microsoft group of companies. All other
> trademarks are property of their respective owners.
