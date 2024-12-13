---
title: Configure feedback surveys using Copilot Studio (preview)
description: Learn how configure surveys using Copilot Studio agents.
author: neeranelli
ms.author: nenellim
ms.reviewer:
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 11/25/2024
ms.custom: bap-template
---

# Configure feedback surveys using Copilot Studio (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

You can create and manage surveys that go out to the customers after a call or conversation ends. When you create a survey in Contact Center admin center or Customer Service admin center, the application automatically provisions a Microsoft Copilot Studio survey agent that can be used to collect customer feedback. Contact centers can improve their quality of service based on the survey responses.
[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

The survey appears for the customer after the customer service representative (representative) ends the conversation or call.
 
With Microsoft Copilot Studio agents, you can:
- Gather customer feedback and configure contextual actions depending on the feedback.
- Unify and centralize the process of configuring surveys across digital messaging, voice, and custom channels.
- Use predefined templates to create surveys.
- Allow supervisors to view and review feedback summarized into actionable insights.

## How it works

1. Create a survey agent in Contact Center admin center or Customer Service admin center.
1. Edit the survey agent in Copilot Studio.
1. Add the survey agent to the appropriate channel.
1. Experience the survey runtime behavior in Contact Center workspace or Customer Service workspace.

## Prerequisites

- Copilot Studio and the channels in Dynamics 365 Contact Center or Dynamics 365 Customer Service are available in the same environment.
- System Administrator role.

## Create a survey

1. In the site map of Contact Center admin center or Customer Service admin center, go to **Customer settings** in **Customer Support**, and select **Manage** for **Customer feedback (preview)**.
1. On the **Customer feedback (preview)** page, select **New**.
1. On the **Add new customer feedback survey** wizard, select one of the following templates, and then select **Next**:
    - **Customer Satisfaction (CSAT) Survey**: Use to ask questions, such as, “On a scale of 1-5, how would you rate your overall satisfaction with the service you received?”
    - **Net Promoter Score (NPS) Survey**: Use to measure customer loyalty, such as, “On a scale of 0 to 10, how likely are you to recommend our product/service/company?” 
    - **Customer Effort Score (CES)**: Use to quantify the ease with which customers can complete their desired actions or resolve issues when interacting with a company’s products or services. Frame questions, such as, “On a scale of 1 to 7, how easy was it to get the help you needed?
    - **Blank Template**: Use it to start a survey from scratch. 
1. On the **Properties** page, do the following:
    - **Name**: Enter a name based on the survey template that you selected.
    - **Language**: Select a language from the supported languages list. The languages that are supported in Copilot Studio only appear.
    - Select the **Enable for Voice Channels** toggle if you want to use the survey for voice conversations.
1. Select **Next**, and on the page that appears, review your choices.
1. Select **Save survey**. The **Survey Created** page displays the summary and link to the survey where it's hosted. The application creates a survey agent with the same name as the survey and is hosted at the same link.
1. Select **Close**. The survey is listed on the **Customer feedback (preview)** page and its status displays as **In Progress**.

### Complete the configuration in Copilot Studio

After you create the survey in the admin center, it needs to be published. If you're creating the survey for the first time using Copilot Studio, the Dataverse connection must be set up before you publish the survey.

1. Select the survey that you created. The survey opens in Copilot Studio page on a new tab. 
1. Update the survey to suit your business needs. 
1. Select **Publish**. After a couple of minutes, the survey status is updated as **Ready** on the Contact Center admin center or Customer Service admin center **Customer feedback (preview)** page.
2. For any issues publishing the survey bot, please see https://learn.microsoft.com/en-us/troubleshoot/dynamics-365/customer-service/omnichannel-for-customer-service/error-in-conversation-start-topic



### Verify the Dataverse connection

Make sure that the Dataverse connection is established for Copilot Studio so that you can publish the survey agent. 

1. Sign into Power Apps, and then go to **Solutions**.
1. On the **Solutions** page, select **Default Solution** under **Unmanaged**.
1. On the page that appears, search for **Connection references** under **Objects**, and then select **Microsoft Dataverse connection reference for MCS Survey**.
1. On the edit pane that appears, select a connection in the **Connection** box or select **New connection**. A new tab opens to create a connection.
1. Complete the steps to create a **Microsoft Dataverse** connection and select it in the **Connection** box.

Learn more at [Set up a Dataverse connection](/power-apps/maker/data-platform/create-connection-reference).

### Manage the surveys

The surveys that you create using the **Customer feedback (preview)** option only appear on the **Customer feedback (preview)** page. You can't manage surveys created using other methods, such as Customer Voice.

Manage your surveys on the **Customer feedback (preview)** page.
- **Edit**: Select a survey, and then select **Edit**. You can edit the survey name only.
- **Demo link**: Select a link to preview the survey and see how it appears in runtime.
- **Status**: Indicates whether a survey is ready or in progress.
- **Voice Enabled**: Indicates whether a survey is enabled for the voice channel.

### Manage the survey agents in Copilot Studio

You can edit your survey agents to fulfill your business needs as follows:
- Customize agent messages
- Add branching logic
- Add more actions
- Add extra topic questions

Edit the **Conversation Start** system topic only. All other system topics are disabled and must not be used.

### Set up custom hosting

You can host surveys on a link other than the default one.

1. In Contact Center admin center or Customer Service admin center, select the survey that you want to custom host.
1. Select the survey and select **Edit**.
1. In **Survey URL**, enter the custom host page URL where you want to display the survey.
1. Do the following for a seamless hosting experience:
    1. Extract the query parameters from the custom host URL and enter in the code snippet.
    1. In the cshtml file, use following code.

    ```
        @{ 
            var environment = Request.Query["Environment"]; 
        
            var bot = Request.Query["Bot"]; 
        
            var surveyVersion = Request.Query["SurveyVersion"]; 
        
            var regardingLiveWorkItemId = Request.Query["RegardingLiveWorkItemId"]; 
        
            var surveyId = Request.Query["SurveyId"]; 
        
            var invitationId = Request.Query["InvitationId"]; 
        } 
    ```

1. Copy the following code snippet and paste it to your HTML website.
   
    ``` 
        <!DOCTYPE html>
        <html>
        <body> 
        <iframe src="https://powerva.microsoft.com/environments/@environment/bots/@bot/webchat?__version__=2&SurveyVersion=@surveyVersion&RegardingLiveWorkItemId=@regardingLiveWorkItemId&SurveyId=@surveyId&InvitationId=@invitationId" frameborder="0" style="width: 300px; height: 500px;"></iframe> 
        </body> 
        </html>  
    ```
1. Style the iframe to match your website.

## Enable the post-conversation survey for digital messaging channels

1. Perform the steps 1 through 3 in [Configure the post-conversation survey](/dynamics365/customer-service/administer/configure-post-conversation-survey#configure-the-post-conversation-survey).
1. Select **Powered by Microsoft Copilot Studio (preview)**. Select a survey from the list. Only those surveys that you create using the customer feedback option and in published state are displayed for you to select.
1. Perform the rest of the steps in **Configure the post-conversation survey**.

## Enable the post-call survey for the voice channel

1. In Contact Center admin center or Customer Service admin center, go to the voice workstream and select **Edit**. 
1. On the **Behaviors** tab, scroll to the bottom of the page and enable the toggle for Post-call survey.
1. In **Customer feedback survey**, select a survey from the list. Only those surveys that you create using the customer feedback option and in published state are displayed for you to select.
1. Verify that the post-call survey option listed on the **Language** tab of the workstream is disabled. The survey option needs to be disabled for the new experience to work as expected.
1. Save the changes.

## View the survey results

The survey results are stored in Dataverse tables. To view the survey responses, in Power Apps, go to **Tables**, and select **Customer feedback survey response**.

The CSAT scores are displayed in the Omnichannel historical analytics report.

### Related information

[Enable feedback on voice call quality](/dynamics365/customer-service/administer/configure-end-of-call-survey?context=/dynamics365/contact-center/context/administer-context)  


