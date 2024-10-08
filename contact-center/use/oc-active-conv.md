---
title: View customer information on Active Conversation form
description: Learn about Active Conversation, its sections, and how you can view customer information.
author: neeranelli
ms.author: nenellim
ms.reviewer: shujoshi
ms.topic: how-to 
ms.date: 07/01/2024
ms.custom: bap-template
---

# View customer information on Active Conversation form

One of the major challenges that customers face when contacting customer support is repeatedly giving the same information about the issue to each support agent they talk to. And if they want to review the status of their request later, they have to share the same information with another support agent to explain the context of the engagement. To avoid this situation, support agents need access to all the information the customer provides, including details about the product or service, issue, case history, related cases, and location.

Having this information ready can help support agents reduce the hold time that they spend retrieving customer information, reduce average handling time, and increase customer satisfaction by resolving issues faster.

## What is Active Conversation?

**Active Conversation** is a page that appears when you accept an incoming request from any channel and gives you complete information about a customer. The  **Active Conversation** view provides the following sections:

- Customer (Contact or Account)
- Conversation summary
- Timeline

For active conversations, you can view the **Active Conversation** form on the agent dashboard of the Contact Center workspace app. The **Active Conversation** form doesn't display details of closed conversations. To view closed conversations, use the **Closed work items** section of the agent dashboard. 

You see the following options on the **Active Conversation** page:  

- **Save**: You can edit and save standard and custom field values added to the **Active Conversation** form by your administrator. However, the following [Logical column names] aren't supported. If a default value is already set for a field, the value appears on the form automatically.
- **Refresh**: Refreshes the data in the form.
- **Queue:** The queue through which the conversation has been assigned to you.
- **Start time:** The time when you started the conversation.
- **Related**: To select and navigate to the required entities.

The application displays the customer or account details with inline edit capabilities.  
   > [!NOTE]
   > - The form selector to switch between **Active Conversation** and **Closed Conversation** is hidden. You can't switch to closed conversation form from the **Active Conversation** form while the conversation is still active or vice versa.
   > - You can see the form selector on the enhanced Active Conversation form if your administrator has enabled it for you. More information: [Display the form selector on Active Conversation form](/dynamics365/customer-service/administer/add-customer-summary-settings?context=/dynamics365/contact-center/context/administer-context). However, if you use the form selector to switch to the closed conversation form, you'll see errors.

## View customer details

This section provides details such as the contact name or account name. For a contact, you can view the location, email, and other details. For an account, you can view location, telephone number, and primary contact person for the account.

Use the customer section to search for an existing contact or account record, and select the record to link it to the conversation. If the record doesn't exist, you can create a new contact or account record by using the **Add Contact** or **Add Account** button, respectively. After you create it, search for the record and then select it to link it to the conversation.

 Displays the customer or account details. The fields displayed on this card are based on your administrator's configuration. For more information, go to [Add the Customer 360 component to a case from]

You can edit the customer or account details inline, without navigating to another tab. However, if you see the default **Customer(Contact or Account)** card, your administrator disabled the enhanced **Customer Details** experience for the **Active Conversation** form.
 
 
## View Conversation summary

Conversation summary changes.

The **Conversation summary** section provides detailed information about the conversation between the agent and customer. The information shown in the **Conversation details** area includes the following:

- **Engagement channel:** The channel, such as live chat or custom channel, through which the conversation is taking place.
- **Waiting time:** The time the customer had to wait before the conversation was assigned to the agent.
- **Skills:** The skills that are attached for routing the conversation. If your administrator enabled the setting for agents to update skills, you can add or remove skills.
- **Queue:** The queue through which the conversation has been assigned to you.
- **Start time:** The time when you started the conversation.

 
In addition, the **Conversation summary** section includes several tabs:

- Prechat survey
- Self service
- Visitor details
- Additional details, if they've been configured and other context variables, if available

These tabs are described in the following sections.

### View Prechat survey

The **Pre-chat survey** tab displays the customer's answers to the survey questions that were posed by your organization, which helps your interaction with the customer.

### View Self service

The **Self service** tab displays information about the activities that the customer performed before starting a conversation with an agent. This information helps you understand why the customer reached out and helps you provide a personalized service for enhanced customer satisfaction. The activity information, which is categorized into the following action types, appears in reverse chronological order.

| Action type | Description |
|-------------|-----------------------------------|
| Page visited | The page visited on the portal, with time stamp.|
| Phrase searched | The keyword or phrase that was searched for, with time stamp. |
| Knowledge article viewed | The knowledge article viewed, with time stamp. |
| Custom action performed | Any other custom action that's tracked by your organization, with time stamp. |

To configure the appearance of the **Self service** tab, see [Enable self-service settings for customer actions in a conversation summary]
### View Visitor details

The **Visitor details** tab provides information such as whether the customer is authenticated, the browser the customer used to contact support, the operating system used by the customer, the customer's location, and the language used during the interaction.

If the customer logs in to the portal to initiate the chat with a support agent, the **Authenticated** field value is **Yes**; otherwise, the **Authenticated** field value is **No**.


### View Additional details

When configured by your administrator or developer, the **Additional details** tab displays the other available context variables for live chat

## View Timeline

This section displays customer-related activities in the form of a timeline. You can create quick notes based on your discussion with the customer. Use the **Linked records** field to switch the timeline based on the contact or account record linked to the conversation.

The **Linked records** field shows the record linked to the conversation. 


### Related information

[Use Contact Center workspace](ccw-overview.md)  
