---
author: neeranelli
ms.topic: include
ms.date: 09/23/2026
ms.author: nenellim
---

## Prepare for the voice migration

Before you change the production configuration:

- Confirm that the target Microsoft Teams Phone option is available in every country or region where you have phone numbers.

- Inventory phone numbers, number types, voice routes, emergency addresses, applications, queues, and carrier dependencies.
- Confirm that the destination tenant has enough Microsoft Teams Phone licenses for users and resource accounts.
- Assign one of the following roles to the administrator who configures Microsoft Teams Phone:
  - Teams Administrator
  - Teams Communications Administrator
  - Teams Telephony Administrator
- Ensure that an Owner or Contributor for the Azure Communication Services resource is available to review or remove its telephony configuration.
- Prepare emergency address information and review local regulatory requirements for every phone number.
- Coordinate with your carrier, telephony administrators, support team, and other affected stakeholders.
- Schedule the production change for a low-traffic maintenance window.

To review available licenses, sign in to the Microsoft 365 admin center, and then go to **Billing** > **Purchase services** > **Add-on subscriptions**. Learn more in [Use Microsoft Teams administrator roles to manage Teams](/microsoftteams/using-admin-roles).
