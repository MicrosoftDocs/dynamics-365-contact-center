---
title: Use Copilot to solve customer issues
description: Learn about how you can use Copilot in Microsoft Dynamics 365 to enhance your productivity when you work on customer service requests.
ms.date: 01/16/2025
ms.topic: how-to
author: neeranelli
ms.author: nenellim
ms.reviewer: shujoshi
ms.collection: bap-ai-copilot
ms.custom: bap-template
---

# Use Copilot to solve customer issues

Copilot is an AI-powered tool that revolutionizes the agent experience/ It provides real-time assistance to resolve issues faster, handle cases more efficiently, and automate time-consuming tasks so you can focus on delivering high-quality service to your customers.

> [!NOTE]
> The feature availability information is as follows.
>
> |Feature| Dynamics 365 Contact Center&mdash;embedded | Dynamics 365 Contact Center&mdash;standalone | 
>  |--------------|----------|----------|
> | Ask a question | Yes  | Yes   | 
> | Draft an email | Yes   | Yes   | 
> | Generate chat responses | Yes   | Yes   | 

> [!IMPORTANT]
> The AI-generated content is a suggestion. It's your responsibility to review and edit the suggested content to make sure it's accurate and appropriate before sharing the responses.

## License requirements

| Requirement type | You must have |  
|-----------------------|---------|
| **License** | <ul><li>Dynamics 365 Contact Center license |

## Prerequisites

Make sure that your administrator has turned on the Copilot features.

## Ask a question 

When you sign in to any of the Customer Service agent apps, Copilot opens in the right side panel with the **Ask a question** tab ready. Copilot acts as your partner, helping to answer questions without your having to search for the information.

### Draft questions

You can ask free-form questions just as you'd ask your colleague or supervisor who might know the answers.

 :::image type="content" source="../media/copilot-ask-question-mini.png" alt-text="Screenshot of the Ask a question tab in Copilot." lightbox="../media/copilot-ask-question.png":::


With Copilot, you can take the following actions:

- **Ask a direct question**: Copilot shows the most relevant answer from the knowledge sources your organization has made available.
- **Ask follow-up turn by turn questions**: If Copilot's response isn't immediately useful, you can ask follow-up questions and guide Copilot in a natural, conversational way.
- **Ask Copilot to attempt a better response**: Copilot can also rephrase responses based on more guidance such as, "Can you summarize your response?" or "Can you attempt a response providing details for each of the steps you mentioned?"


### View responses

Copilot streams the generated responses on the UI incrementally, and you can view the responses as they are generated. You can also select **Stop responding** for Copilot to stop generating responses, allowing you to start afresh.

In the Copilot's response you can see citation numbers that show the knowledge base or website links from which Copilot drew the response. When you select the citation, you can see an inline link to the source.

### Translate responses

If your administrator has enabled translation, you can select **Translate** and then select your preferred language to translate the response to that language. You can also select **Show original** to translate the response back to the original language.

### Use the responses

If you're satisfied with the response Copilot provides, you can use the whole thing or a part of it to answer the customer's question:

- Copy part of Copilot's reply into your chat or read from it during a voice conversation. Select the copy icon to copy the entire response to the clipboard.  
- When you're in an active digital messaging conversation, select **Send to customer** to open an editing window where you can revise the response and send it to the customer. You can also change customer keywords to prompt Copilot to generate a more accurate response.
- Select **Check sources** to see the knowledge base or website links from which Copilot drew the response. You can use this supplemental information as a resource or share it with the customer.

### Provide feedback

To rate the usefulness of Copilot's responses, select the thumbs-up or thumbs-down icon.

## Draft a chat response (Preview)

Use Copilot to draft chat responses when you're in a conversation with a customer.

:::image type="content" source="../media/copilot-responses.png" alt-text="Screenshot of Copilot suggested responses for conversations.":::

### Generate a chat response

Select the one-click response generation button at the lower-right corner of the Conversation control panel and at the lower-left corner of the Copilot pane. Copilot analyzes the context of the conversation and the latest customer question or message, and drafts a response to send directly to the customer. You don't need to manually type the question.

> [!NOTE]
> The one-click response generation feature is available in North America, Europe, and the United Kingdom only.

### Related information

[Understand Copilot language support](copilot-language-support.md)  
[Manage copilot features in Customer Service](../administer/configure-copilot-features.md)  
[FAQ for Copilot in Customer Service](/dynamics365/customer-service/implement/faq-responsible-ai-copilot?context=/dynamics365/contact-center/administer-context) 
