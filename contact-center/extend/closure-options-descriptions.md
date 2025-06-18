---
title: Session closure options and descriptions
description: Learn about session closure options and their descriptions.
author: neeranelli
ms.author: nenellim
ms.topic: reference
ms.date: 06/18/2025
ms.reviewer: nenellim
---

# Session closure options and descriptions

When a session in the conversation is closed, the system identifies the reason and populates the value in the `msdyn_ocsession` table. The closure options and their descriptions are as follows.

|Value|Label|Description|
|-----|-----|-----------|
|192350000|**Default**|Indicates that no other closure reason is applicable.|
|192350001|**AgentReject**|Indicates that the customer service representative (service representative or representative) declined the conversation.|
|192350002|**AgentTimeout**|Indicates that the representative didn't respond to the conversation notification within the allotted time.|
|192350003|**ConversationTimeout**|Indicates that the conversation session ended because of a time out.|
|192350004|**AgentClosed**|Indicates that the representative ended the session, which means the representative selected the session tab "X".|
|192350005|**ConversationClosed**|Indicates that the conversation session was closed.|
|192350006|**AgentTransferred**|Indicates that the conversation was transferred to another representative.|
|192350007|**AgentDisconnected**|Indicates that the representative was disconnected from the conversation.|
|192350008|**AgentReRouted**|Indicates that the conversation was reassigned.|
|192350009|**VirtualAgentClosed**|Indicates that the AI agent has closed the conversation.|
|192350010|**AgentTransferToQueue**|Indicates that a representative has transferred the conversation to a different queue.|
|192350011|**SupervisorAssignToQueue**|Indicates that a supervisor has manually assigned the conversation to a different queue.|
|192350012|**SupervisorTransferToAgent**|Occurs when a supervisor transfers a conversation to a representative.|
|192350013|**SystemReject**|Indicates that the system has rejected the conversation.|
|192350014|**ForceClose**|Indicates that the supervisor forcibly closed the conversation.|
|192350015|**OverflowQueueTransfer**|Occurs when a conversation is transferred from an overflowing queue to another queue.|
|192350016|**OverflowEndConversation**|Occurs when a conversation ends because of overflow.|
|192350017|**AddAgentFailed**|Occurs when an attempt to add a representative to a conversation fails.|
|192350018|**AutoClose**|Occurs when an expired conversation is automatically closed.|
|192350019|**SecondaryChannelClosed**|Occurs when a secondary channel is closed.|
|192350020|**CustomerDisconnect**|Occurs when a customer disconnects from a conversation.|
|192350021|**AgentEndConversation**|Occurs when a representative ends a conversation.|
|192350022|**CustomerEndConversation**|Occurs when a customer ends a conversation.|
|192350023|**QueueTransfer**|Occurs when the representative transfers a conversation to a different queue.|
|192350024|**InqueueOverflowQueueTransfer**|Occurs when inqueue overflow triggers the transfer of conversation from one queue to another and this action closes the previous session.|
|192350025|**InqueueOverflowEndConversation**|Occurs when inqueue overflow ends the conversation.|
|192350026|**BotTransferToAgent**|Indicates that the AI agent has escalated the conversation.|
|192350027|**BotEndConversation**|Indicates that the agent has ended the conversation.|
|192350028|**BotCallFailureEndConversation**|When agent play a message to the caller because of some internal failure and conversation ends.|
|192350029|**BotCallFailureExternalTransfer**|When agent transfers the call to an external phone number because of some internal failure and conversation ends.|
|192350030|**BotCallFailurePromptAndEscalate**|When conversation isn't ending as caller hears a prompt, wait music and then sent to the default fallback queue so caller is transferred to a representative or whatever queue behavior is defined.|
|192350031|**BotCallFailureEscalate**|When conversation isn't ending as caller hears wait music, and is sent to the default fallback queue, so caller is transferred to a representative or whatever queue behavior is defined.|

## Related information

[msdyn_closurereason Choices/Options](/dynamics365/developer/reference/entities/msdyn_ocsession#msdyn_closurereason-choicesoptions)  