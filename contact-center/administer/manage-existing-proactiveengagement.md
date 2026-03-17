---
title: Configure proactive engagement
description: Learn how to set up proactive engagement, including dial modes and operational rules for optimized customer service in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 01/19/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

## Configure multiparty (account) engagements 

Contact chaining lets you group related contacts—such as members of the same household or account—and treat them as a single unit for engagement purposes.

- You can group up to five contacts when uploading a file or submitting requests through the API.
- All contacts in the chain are considered for every attempt. The system dials contacts in the order they appear in the file or API array.
- If all phone numbers across all chained contacts are exhausted on an attempt, the system waits for the configured retry interval before starting the next attempt and cycles through all contacts again.

## Configure call cancellation and suppression

You can cancel pending calls and optionally suppress future calls that match defined criteria. 

1. In the site map, select **Proactive engagements**, select the proactive engagement settings, and then select **Add a cancellation policy**.
2. Specify filter criteria using any combination of the following in AND conditions:
   - Proactive engagement configuration ID
   - Country
   - State
   - Postal code
   
4. Optionally, specify an end date **Exectue policy until**. Contacts matching the criteria won't be processed for new calls during the specified period.
5. Optionally, enter a **Comment**. Cancelled calls are marked in the delivery tables with a reference to the cancellation policy to enable reporting.

> [!NOTE]
> Cancellation applies only to queued calls. You can also trigger cancellation and suppression through the CCaaS API. Learn more in [Use CCaaS_CreateProactiveVoiceDelivery API](../extend/api/ccaas_createproactivevoicedelivery.md).

