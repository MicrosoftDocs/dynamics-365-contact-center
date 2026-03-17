---
title: Best practices for proactive engagement campaigns
description: Recommendations for running effective and compliant proactive engagement campaigns in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: best-practice
ms.collection: bap-ai-copilot
ms.date: 01/19/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Best practices for proactive engagement campaigns

This article provides recommendations to help you run proactive engagement campaigns that are effective and compliant with applicable regulations.

## Understand and comply with local regulations

Outbound calling is subject to telecommunications regulations that vary by country, region, and industry. Before running any campaign, review the regulations that apply to your organization and your customers' locations.

Key regulatory frameworks to be aware of include:

- **TCPA (United States)**: The Telephone Consumer Protection Act governs automated calls and prerecorded messages. It sets restrictions on calling hours, requires prior express written consent for robocalls, limits abandonment rates, and mandates opt-out mechanisms. AI-generated voices are subject to the same requirements as prerecorded messages.
- **Ofcom (United Kingdom)**: The UK communications regulator sets rules on abandoned call rates, calling line identification, and silent calls. Organizations must not present a false or unavailable caller ID.
- **GDPR (European Union and United Kingdom)**: Outbound calls involving personal data must have a lawful basis—either explicit consent or a documented legitimate interest. Organizations must be able to demonstrate compliance and must honor data subject rights including the right to object to processing.

> [!IMPORTANT]
> Regulations change frequently and vary at the state and local level. Consult your legal team or a qualified compliance specialist before launching campaigns, especially in regulated industries such as financial services and healthcare.

## Keep customer data accurate

The quality of your contact list directly affects campaign performance and compliance. Calling invalid, reassigned, or opted-out numbers wastes capacity and can expose your organization to regulatory risk.

- Validate contact records before each campaign. Remove invalid, disconnected, or ported numbers.
- Suppress contacts against applicable national and regional do-not-call registries before every campaign run.
- Maintain an internal do-not-call list and apply it across all campaigns. Honor opt-out requests promptly and retain records for the period required by applicable law.
- Verify that the phone number on record belongs to the intended contact before using automated or AI-led dial modes.

## Respect customer contact preferences

Contacting customers at the wrong time or too frequently damages trust and increases opt-out rates.

- **Calling hours**: Place calls only during hours that are permissible under applicable law and that reflect your customers' preferences. Federal law in the United States prohibits calls to residential numbers before 8:00 a.m. or after 9:00 p.m. local time at the called party's location. Many states and countries have stricter restrictions.
- **Frequency capping**: Set limits on how often a contact can be called within a given period. Calling the same contact repeatedly in a short time period increases the likelihood of opt-outs and complaints.
- **Retry intervals**: Space retry attempts across different times of day rather than calling at the same time repeatedly. Apply a cooling-off period between attempts.
- **Channel preferences**: If a contact has not responded after several voice attempts, consider whether an alternate channel such as SMS or email is more appropriate before making further calls.

## Register and protect your caller identity

Customers are less likely to answer calls from numbers they don't recognize or that are labeled as spam.

- Register your outbound phone numbers with caller ID reputation registries to reduce the risk of calls being labeled "Spam Likely" or blocked by carriers.
- Work with your telephony provider or a third-party vendor that specializes in caller ID reputation management to monitor how your numbers are classified and to address flagging issues promptly. Considering using a branding service to appropriately brand your calls to increase answer rate. 
- Avoid placing a disproportionately high volume of calls from a single phone number in a short period, as this can trigger carrier spam detection.


### Related information

[Configure proactive engagement](configure-proactive-engagement.md)
[Dial modes for proactive engagement](dial-modes-proactive-engagement.md)
[Outcomes for proactive engagement](proactive-engagement-outcomes.md)
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)
