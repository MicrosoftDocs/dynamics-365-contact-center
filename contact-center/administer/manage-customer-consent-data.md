---
title: Manage customer consent and voice-authentication data (preview)
description: Look up a customer by customer ID and manage their consent status, voiceprint lock status, and voice-authentication data in the biometric authentication and fraud detection app.
author: timsavage
ms.author: timsavage
ms.reviewer: puneetsingh
ms.topic: how-to
ms.date: 11/09/2026
ms.custom: 
    - bap-template
    - ai-gen-docs-bap
    - ai-seo-date: 11/09/2026
ai-usage: ai-assisted
---


# Manage customer consent and voice-authentication data (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

As a supervisor, use the customer consent screen in the **Biometric authentication and fraud detection** app to look up your customer's voice-authentication data and manage it. You can review your customer's consent status and enrollment details, change their consent, lock or unlock their voiceprint stored within your Dataverse environment, and delete their voice-authentication data when needed.

You search for a customer by using the **customer ID** as the key, so have your customer ID ready before you start. Use this article when you need to respond to your customer's consent choice, service a data request, or remove voice-authentication data that's no longer needed.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- At least the security role or privilege required to view and manage customer consent data, such as Supervisor.
- The **customer ID** for the customer whose data you want to manage.

## Find a customer's consent record

Search for your customer to open their consent record. Use your customer ID to look up the record.

1. Open the **Biometric authentication and fraud detection** app.
1. Go to the customer consent screen.
1. In the search field, enter the **customer ID**, and then select **Search**.

The customer's record opens and shows their consent and enrollment details.

## Review consent and enrollment details

After you find your customer, review their record to understand their current consent and enrollment state before you make changes. The record shows the following details:

- **Customer ID**: The key used to look up the record.
- **Consent status**: Whether your customer consented to voice authentication (for example, **Yes** or **No**). 
- **Customer name**: The name associated with your customer ID.
- **Voiceprint last adaptation date**: The date your customer's voiceprint was last used.
- **Initial enrollment date**: The date your customer first enrolled in voice authentication.
- **Audio segments**: The audio segments linked to your customer's voiceprint.

## Operations and their impact on customer data

The following matrix summarizes what each operation removes and how it affects the customer's consent status.

| Operation | Voiceprint | Enrollment audio | Customer profile metadata | Non-enrollment audio segments | Consent status after |
| --- | --- | --- | --- | --- | --- |
| Set consent status to No | Deleted | Deleted | Not deleted | Not deleted | No |
| Set consent status to Yes | Not deleted | Not deleted | Not deleted | Not deleted | Yes |
| Lock voiceprint | Not deleted | Not deleted | Not deleted | Not deleted | Unchanged |
| Unlock voiceprint | Not deleted | Not deleted | Not deleted | Not deleted | Unchanged |
| Delete voiceprint | Deleted | Not deleted | Not deleted | Not deleted | No |
| Delete customer profile | Deleted | Deleted | Deleted | Not deleted; disassociated from the customer identifier | Customer profile no longer exists |
| Delete all customer data | Deleted | Deleted | Deleted | Deleted | Customer profile no longer exists |
| Delete enrollment audio | Deleted | Deleted | Not deleted | Not deleted | Unchanged |

## Edit the customer consent status

Update a customer's consent status when the customer changes their choice about voice authentication.

1. Find the customer's consent record. Learn more in [Find a customer's consent record](#find-a-customers-consent-record).
1. Select **Edit** for the consent status.
1. Change the consent status. The available values are **Yes** and **No**.
1. Select **Next**.
1. Review and **Confirm changes**.

The updated consent status appears in the customer's record.

Setting the consent status to **No** doesn't delete any data. Your customer's voiceprint, enrollment audio, and profile remain, and their existing data is unaffected. The status changes to **No**, and future interactions don't offer voiceprint enrollment.

## Edit the voiceprint lock status

Lock or unlock a customer's voiceprint to control whether it can authenticate your customer.

1. Find your customer's consent record. Learn more in [Find a customer's consent record](#find-a-customers-consent-record).
1. Select **Edit** for the voiceprint lock status.
1. Set the lock status to **Locked** or **Unlocked**.
1. Select **Next**.
1. Review and **Confirm changes**.

The updated lock status appears in your customer's record.

Voiceprint locking protects against brute-force attacks. A voiceprint automatically locks after consecutive failed authentication attempts against it, which stops an imposter from continuing to try. A locked voiceprint automatically unlocks after a configurable number of hours, and a supervisor can also lock or unlock it manually from this screen. While a voiceprint is locked, you can't use it to authenticate the customer.

## Delete customer voice-authentication data

You can delete your customer's voiceprint, their customer profile, or all of their data. Choose the option that matches your scenario.

> [!WARNING]
> Deleting **all customer data** is a one-time, irreversible action. After you delete all customer data, searching for that customer ID returns no results, and the data can't be recovered.

For the exact scope of each delete option, go to [Operations and their impact on customer data](#operations-and-their-impact-on-customer-data).

1. Find the customer's consent record. Learn more in [Find a customer's consent record](#find-a-customers-consent-record).
1. Select the delete option that matches what you want to remove: 
   - **Delete voiceprint**: Removes your customer's voiceprint stored within your Dataverse environment.
   - **Delete customer profile**: Removes the customer profile.
   - **Delete all customer data**: Removes all data for the customer ID. This action can't be undone.
1. Confirm the deletion when prompted. 

After deletion, the removed data no longer appears in the customer's record. If you deleted all customer data, searching for that customer ID returns no results.

## Related information
- [Capture customer consent in the Biometric authentication and fraud detection app](capture-consent-for-voice-enrollment.md)
- [Manage voice enrollment and authentication](manage-voice-enrollment-authentication.md)
