---
title: Session closure reasons in Dynamics 365 Contact Center
description: Learn about session closure reasons and their descriptions to help you understand what they mean.
author: neeranelli
ms.author: nenellim
ms.topic: reference
ms.date: 08/31/2026
ms.reviewer: nenellim
---

# Session closure reasons

When a session in the conversation is closed, the system identifies the reason and populates the value in the `msdyn_ocsession` table. The closure reasons with their description are as follows.

|Value|Label|Description|
|-----|-----|-----------|
|192350000|**Default**|Indicates that no other closure reason is applicable.|
|192350001|**AgentReject**|Indicates that the customer service representative (service representative or representative) declined the conversation.|
|192350002|**AgentTimeout**|Indicates that the representative didn't respond to the conversation notification within the allotted time.|
|192350003|**ConversationTimeout**|Indicates that the conversation session ended because of a time out.|
|192350004|**AgentClosed**|Indicates that the representative ended the session, which means the representative selected the **X** icon on the session tab.|
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
|192350024|**InqueueOverflowQueueTransfer**|Occurs when in-queue overflow triggers the transfer of conversation from one queue to another and this action closes the previous session.|
|192350025|**InqueueOverflowEndConversation**|Occurs when in-queue overflow ends the conversation.|
|192350026|**BotTransferToAgent**|Indicates that the AI agent has escalated the conversation.|
|192350027|**BotEndConversation**|Indicates that the agent has ended the conversation.|
|192350028|**BotCallFailureEndConversation**|When agent plays a message to the caller because of some internal failure and conversation ends.|
|192350029|**BotCallFailureExternalTransfer**|When agent transfers the call to an external phone number because of some internal failure and conversation ends.|
|192350030|**BotCallFailurePromptAndEscalate**|When conversation isn't ending as caller hears a prompt, wait music, and then sent to the default fallback queue where the caller is transferred to a representative or handled according to the behavior defined for the fallback queue.|
|192350031|**BotCallFailureEscalate**|When conversation isn't ending as caller hears wait music, and is sent to the default fallback queue, where the caller is transferred to a representative or handled according to the behavior defined for the fallback queue.|
| 192350034 | **ManuallyClosedSession** | Occurs when an individual session is manually closed while the conversation itself might remain open. |
| 192350036 | **ExternalAgentAccept** | Occurs when an external (non-microsoft/partner) representative accepts the conversation. |
| 192350037 | **ExternalAgentReject** | Occurs when an external representative declines the conversation. |
| 192350038 | **ExternalAgentTransfer** | Occurs when the conversation is transferred to or from an external representative. |
| 192350054 | **VoiceConnectivityProblem** | Occurs when the session ends because of a voice/telephony connectivity problem. |
| 192350055 | **MaximumSessionsReached** | Occurs when the session can't proceed because the representative's maximum concurrent session limit is reached. |
| 192350056 | **CallTimedOut** | Occurs when a voice call ends because it timed out. |
| 192350061 | **CustomerNonResponseTimeoutRule** | Occurs when a timeout rule is triggered because the customer didn't respond within the configured time. |
| 192350062 | **AgentNonResponseTimeoutRule** | Occurs when a timeout rule is triggered because the representative didn't respond within the configured time. |
| 192350063 | **AgentMovedConversationToWaiting** | Occurs when a representative moves the conversation to the waiting state, ending the active session. |
| 192350064 | **AutoRejectedDueToBrowserRefresh** | Occurs when a conversation notification is automatically rejected because the representative refreshed the browser. |
| 192350065 | **AutoRejectAsOutboundCallInProgress** | Occurs when an incoming conversation is automatically rejected because the representative is on an outbound call. |

## Related information

[msdyn_closurereason Choices/Options](/dynamics365/developer/reference/entities/msdyn_ocsession#msdyn_closurereason-choicesoptions)  
