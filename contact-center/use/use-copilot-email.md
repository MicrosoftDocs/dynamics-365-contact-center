---
title: Write an email with Copilot
description: Learn how agents can use Copilot to draft emails to increase productivity.
author: gandhamm
ms.author: mgandham
ms.topic: conceptual
ms.collection: bap-ai-copilot
ms.date: 01/16/2025
ms.custom: bap-template 
---

# Write an email with Copilot

When you draft customer emails, Copilot can offer suggestions to make them clearer, concise, and compelling. 

*Always review the response* Copilot generates before you send the email to the customer.

> [!NOTE]
> The feature availability information is as follows.
>
> |Feature| Dynamics 365 Contact Center&mdash;embedded | Dynamics 365 Contact Center&mdash;standalone | 
>  |--------------|----------|----------|
> | Draft an email | Yes   | Yes   | 
## Use Copilot to draft an email

When you use Copilot to draft an email, you can use the following features to help you write a response to a customer:

### Use prompts

- **Suggest a call**: Drafts a reply that suggests a call with the customer the same day or the next day.
- **Request more information**: Drafts a reply that requests more details from the customer to help resolve the problem.
- **Empathize with feedback**: Drafts a reply that provides an empathetic response to a customer who expresses a complaint.
- **Provide product/service details**: Drafts a reply that offers details or answers customer questions about a particular product or service.
- **Resolve the customer's problem**: Drafts a reply that provides a resolution&mdash;and resolution steps, if applicable&mdash;to the customer's problem.
- **Custom**: Allows you to provide your own prompt for the reply.

> [!NOTE]
> - If your administrator has not enabled knowledge base, you will see the **Suggest a call**, **Request more information**, **Empathize with feedback**, and **Custom** prompts only.
> - If you've left the **Regarding** field empty, you will see the **Suggest a call**, **Empathize with feedback**, and **Custom** prompts only.


### Use filters

You can select **Filters** to choose the relevant knowledge articles only that Copilot must use to generate the response.

### How Copilot uses knowledge base and web sources

If your administrator enabled knowledge sources and set up trusted domains, the following actions occur:
-  Copilot uses internal knowledge base sources and searches the internal knowledge base and up to five trusted domains to generate email drafts. 
- The application displays the knowledge sources used to generate the draft when you select **Check sources**.
- When you use a custom prompt to further refine the response, the application displays the **Use knowledge base** toggle that's set to **On**. You can switch the toggle to **Off** to disable knowledge base sources.

### Review suggested replies

When you select one of the predefined prompts, Copilot generates a suggested reply that's displayed on the UI incrementally. You can also see the inline citations that show the knowledge base or website links from which Copilot drew the response. When you hover over the citation, you can see an inline link to the source. You can select **Stop Responding** to stop Copilot from generating the email draft. The application displays the prompts for you to start over. 

### Refine replies

You can select **Adjust** to change the length and tone of the response as follows:

**Length**: Select **Short**, **Medium**, or **Long** to condense or expand on your text. <br>
**Tone**: Select **Friendly**, **Professional**, or **Formal** to adjust the tone of your text.

> [!NOTE]
> The **Adjust** feature supports responses in English only.

### Use follow-up prompts

If you aren't satisfied with Copilot's response, you can use follow-up custom prompts and guide Copilot in a natural, conversational way. You can use up to five prompts at a time to refine the email draft. If your administrator has enabled knowledge base, Copilot will also use those sources.

### Use the responses

To use the draft that Copilot generates, do the following actions:
- In the rich text editor, select **Keep it**. You'll see the draft in the rich text editor that you can use as-is or further edit before sending it to the customer.
- In the Copilot pane, you can:
    - Select **Edit** to further refine the response.
    - Select **Copy** to copy the response and then paste it in the email body.

### Start over

To return to the prompts, select **Start over** at the bottom of the Copilot pane.

## Next Step

[Use Copilot to solve customer issues](use-copilot-features.md)

### Related information

[Enable Copilot to draft emails](../administer/copilot-email-enable.md)
[FAQ for Copilot in Customer Service](/dynamics365/customer-service/administer/faq-copilot-features?context=/dynamics365/contact-center/context/administer-context) 
[FAQ for Copilot in Customer Service](/dynamics365/customer-service/implement/faq-responsible-ai-copilot?context=/dynamics365/contact-center/administer-context) 
