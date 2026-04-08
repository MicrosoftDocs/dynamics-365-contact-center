---
title: Best practices for proactive engagement campaigns in Dynamics 365 Contact Center
description: Recommendations for running effective and compliant proactive engagement campaigns in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot
ms.date: 04/06/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Best practices for proactive engagement campaigns

This article provides recommendations to help you run proactive engagement campaigns that are effective and compliant with the applicable regulations.

## Understand and comply with local regulations

Outbound calling is subject to telecommunications regulations that vary by country/region and industry. Before you run any campaign, review the regulations that apply to your organization and your customers' locations.

Key regulatory frameworks to be aware of include:

- **TCPA (United States)**: The Telephone Consumer Protection Act governs automated calls and prerecorded messages, including AI-generated voices, regardless of whether the call is for a marketing or informational purpose. It sets restrictions on calling hours, requires prior express written consent to specifically include consent to receive robocalls, limits abandonment rates, and mandates opt-out mechanisms. TCPA is a strict liability regime that provides a private right of action, including class action lawsuits, so compliance should be reviewed closely with legal counsel.

- **UTR (Canada)**: The Unsolicited Telecommunications Rules govern all robocalls, regardless of whether the call is for a marketing or informational purpose, and require registration and screening against do not call lists, restrict calling hours, require prior express written consent for robocalls, and mandate opt-out mechanisms and caller identity.
- **PECR (United Kingdom)**: The Privacy and Electronic Communications Regulation sets rules on abandoned call rates, calling line identification, silent calls, and requires specific prior express consent for autodialed calls. Organizations must not present a false or unavailable caller ID.
- **ePrivacy Directive (European Union) and GDPR (European Union and United Kingdom)**: The ePrivacy Directive requires prior express consent for direct marketing that uses automated dialing systems without human intervention. Consent must meet the standards established by the GDPR. Organizations must be able to demonstrate compliance and must honor data subject rights including the right to object to processing of their personal data.
- **EU AI Act (European Union)**: The EU AI Act states that companies must inform users when they are interacting with an AI system.
- **Asia Pacific and Rest of World**: Many countries in Asia Pacific and rest of world require prior consent and compliance with additional requirements for marketing calls that use automatic dialers and/or artificial/prerecorded voice, such as screening against do not call lists, restricted calling hours, opt-out mechanisms, and caller identity.

> [!IMPORTANT]
> Regulations change frequently and vary at the state and local level. Consult your legal team or a qualified compliance specialist before launching campaigns, especially in regulated industries such as financial services and healthcare.

## Keep customer data accurate

The quality of your contact list directly affects campaign performance and compliance. Calls to invalid, reassigned, or opted-out numbers waste capacity and can expose your organization to regulatory risk.

- Verify contact records before each campaign. Remove invalid, disconnected, or ported numbers.
- Suppress contacts against applicable national and regional do-not-call registries before every campaign run.
- Maintain an internal do-not-call list and apply it across all campaigns. Honor opt-out requests promptly and retain records for the period required by applicable law.
- Verify that the phone number on record belongs to the intended contact before using automated or AI-led dial modes.

## Respect customer contact preferences

Contacting customers at the wrong time or too frequently reduces trust and increases opt-out rates.

- **Calling hours**: Place calls during hours that are permissible under applicable law and reflect your customers' preferences. Federal law in the United States prohibits calls to residential numbers before 8:00 A.M. or after 9:00 P.M. in the customer's local time zone. Many states and countries/regions have stricter restrictions.
- **Frequency capping**: Set limits on how often you can call a contact within a specific period. Calling the same contact repeatedly in a short time increases the likelihood of opt-outs and complaints.
- **Retry intervals**: Space retry attempts across different times of day rather than calling at the same time repeatedly. Apply a cooling-off period between attempts.
- **Channel preferences**: If a contact hasn't responded after several voice attempts, consider whether an alternate channel such as SMS or email is more appropriate before making further calls.

## Register and protect your caller identity

Customers are less likely to answer calls from numbers they don't recognize or that are labeled as spam.

- Register your outbound phone numbers with caller ID reputation registries to reduce the risk of calls being labeled "Spam likely" or blocked by carriers.
- Work with your telephony provider or a third-party vendor that specializes in caller ID reputation management to monitor how your numbers are classified and address flagging issues promptly. Consider using a branding service to brand your calls appropriately and increase answer rates. 
- Avoid placing a disproportionately high volume of calls from a single phone number in a short period to avoid triggering carrier spam detection.

### Related information

[Configure proactive engagement](configure-proactive-engagement.md)  
[Dial modes for proactive engagement](proactive-engagement-dial-modes.md)  
[Outcomes for proactive engagement](proactive-engagement-outcomes.md)  
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)  
