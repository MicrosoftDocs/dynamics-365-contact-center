---
title: Plan migration from Azure Communication Services
description: Learn how the retirement of Azure Communication Services capabilities affects Dynamics 365 Contact Center and how to plan your voice and messaging migration.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 09/23/2026
ms.topic: concept-article
ms.custom: bap-template
---

# Plan migration from Azure Communication Services

Microsoft is evolving its communications platform to deliver a more unified, scalable, and innovation-ready foundation for customer engagement. This change is a strategic modernization effort designed to better support long-term customer needs.

Microsoft retires certain standalone Azure Communication Services capabilities on September 30, 2028. Dynamics 365 Contact Center uses these capabilities for some voice, SMS, and WhatsApp configurations. This article explains the impact and helps you choose a supported migration path.

Microsoft Teams Phone extensibility is the strategic voice platform for Dynamics 365 Contact Center. Microsoft also provides supported alternatives for SMS and WhatsApp. Learn more in [Azure Communication Services retirement and breaking changes](/azure/communication-services/acs-retirement-and-breaking-changes-guide).

> [!IMPORTANT]
> You don't need to take immediate action. Affected capabilities remain fully supported through September 30, 2028. Begin planning early so that you have time to assess dependencies, test the replacement services, and complete a phased migration.

## Understand the impact

The retirement affects the following Dynamics 365 Contact Center configurations:

- Voice telephony through Azure Communication Services Direct Offer or Direct Routing
- SMS through Azure Communication Services
- WhatsApp through Azure Communication Services

The retirement doesn't affect voice configurations that already use Microsoft Teams Phone extensibility. It also doesn't affect SMS through Twilio or Infobip, or WhatsApp through Twilio.

| Current configuration | Impact | Recommended action |
|---|---|---|
| Microsoft Teams Phone extensibility | No change | No action is required. |
| Voice through Azure Communication Services | Supported through September 30, 2028 | Migrate to Microsoft Teams Phone extensibility. |
| SMS through Azure Communication Services | Supported through September 30, 2028 | Migrate to SMS through Twilio or Infobip. |
| WhatsApp through Azure Communication Services | Supported through September 30, 2028 | Migrate to Meta Direct or WhatsApp through Twilio. |
| SMS through Twilio or Infobip | No change | No action is required. |
| WhatsApp through Twilio | No change | No action is required. |

## Review the retirement schedule

| Date | Milestone |
|---|---|
| September 30, 2026 | Microsoft announces the retirement and related breaking changes. |
| September 30, 2026 | Phone number acquisition restrictions take effect for new Azure Communication Services customers. |
| September 30, 2028 | Retired Azure Communication Services capabilities reach end of service. |

## Plan for phone numbers

During the transition period:

- Organizations with an existing Azure Communication Services resource can continue to acquire phone numbers.
- Porting phone numbers into and out of an existing Azure Communication Services resource remains supported.
- Organizations without an existing Azure Communication Services resource can't acquire or port phone numbers into Azure Communication Services after September 30, 2026.

Include number portability in your migration plan. Portability depends on the destination service, carrier requirements, geographic availability, and local regulations.

## Choose a voice migration path

Customers who use voice telephony through Azure Communication Services must migrate to Microsoft Teams Phone extensibility before September 30, 2028. Choose a path based on your current telephony architecture, carrier strategy, geographic coverage, and connectivity requirements.

| Current configuration | Target configuration | When to choose this path |
|---|---|---|
| Azure Communication Services Direct Offer | [Teams Calling Plan](migrate-direct-offer-to-teams-calling-plan.md) | Choose this option if you want Microsoft-managed public switched telephone network services and don't need a separate carrier relationship or customer-managed session border controller infrastructure. |
| Azure Communication Services Direct Routing | [Teams Direct Routing](migrate-azure-communication-services-direct-routing-to-teams-direct-routing.md) | Choose this option if you want to retain existing carrier relationships and session border controller investments. |
| Azure Communication Services Direct Routing | [Operator Connect](migrate-azure-communication-services-direct-routing-to-operator-connect.md) | Choose this option if you want a participating certified carrier to manage public switched telephone network connectivity. |

## Choose a messaging migration path

The recommended destination depends on the channel and your provider requirements.

| Current configuration | Supported migration paths | Considerations |
|---|---|---|
| SMS through Azure Communication Services | SMS through Twilio or SMS through Infobip | Compare geographic coverage, number portability, compliance requirements, existing provider relationships, procurement, and commercial terms. |
| WhatsApp through Azure Communication Services | WhatsApp through Twilio | WhatsApp through Twilio can be a good fit if your organization already uses Twilio or wants to consolidate messaging providers. |

Existing SMS and WhatsApp channels through Azure Communication Services remain supported until September 30, 2028. For new deployments, use a supported long-term messaging option.

To prepare for messaging migration:

1. Identify all SMS and WhatsApp channels configured through Azure Communication Services.
1. Inventory phone numbers, routing configurations, templates, automations, and related integrations.
1. Evaluate the destination provider for each channel.
1. Validate provider coverage, number migration requirements, and regional compliance requirements.
1. Test messaging workflows, automation, routing, and reporting.
1. After migration, validate inbound and outbound messaging.

Learn more in the following articles:

- [Configure an SMS channel for Twilio](/dynamics365/customer-service/administer/configure-sms-channel-twilio)
- [Configure an SMS channel for Infobip](configure-sms-channel-infobip.md)
- [Configure a WhatsApp channel through Twilio](/dynamics365/customer-service/administer/configure-whatsapp-channel)

## Prepare your migration

Use the following process for each affected channel:

1. Inventory phone numbers, channel configurations, routing, provider dependencies, integrations, and automation.
1. Confirm licensing, commercial, regulatory, emergency calling, and number portability requirements.
1. Design the target configuration and migration sequence.
1. Pilot the target configuration before you migrate production workloads.
1. Schedule production changes during a low-traffic period.

The detailed voice migration articles provide a shared post-cutover validation checklist. Messaging validation is covered in [Choose a messaging migration path](#choose-a-messaging-migration-path).

Complete all migrations before September 30, 2028.

## Frequently asked questions

### Will Dynamics 365 Contact Center stop working on September 30, 2028?

No. Dynamics 365 Contact Center will continue to operate. However, voice, SMS, or WhatsApp configurations that still depend on retired Azure Communication Services capabilities will stop working.

### Can I keep my existing phone numbers?

In many cases, yes. You can continue using existing numbers during the retirement period and might be able to port them to the destination provider. Portability depends on the destination service, carrier, country or region, and local regulations.

### Can I acquire or port phone numbers during the retirement period?

Learn more in [Plan for phone numbers](#plan-for-phone-numbers).

### Can I keep my carrier when I migrate voice services?

In many cases, yes. Teams Direct Routing can preserve existing carrier and session border controller investments. Operator Connect can preserve an existing carrier relationship if the carrier participates in the program.

### How do I choose among Teams Calling Plan, Direct Routing, and Operator Connect?

The information in [Choose a voice migration path](#choose-a-voice-migration-path) can help you select the path. Consider geographic coverage, number portability, existing telecommunications contracts, regulatory requirements, and support models.

### Does Operator Connect require migration?

Operator Connect configurations that already use Microsoft Teams Phone extensibility aren't affected. Verify whether your deployment uses voice services through Azure Communication Services or Microsoft Teams Phone extensibility.

### What replaces SMS through Azure Communication Services?

The supported replacements are SMS through Twilio and SMS through Infobip. Customers already using either provider aren't affected by the retirement.

### What replaces WhatsApp through Azure Communication Services?

WhatsApp through Twilio is a supported provider-based alternative.

### Will an existing SMS or WhatsApp configuration migrate automatically?

No. Plan to assess, configure, test, and validate each channel in the destination service. Microsoft will provide migration guidance, tooling, and support during the transition.

### Do service-level agreements or contracts change during the retirement period?

Current service-level agreements remain in effect through September 30, 2028. Existing commercial agreements remain unchanged during the transition period.

### Should I migrate immediately?

You don't need to migrate immediately, but you should begin planning now. Early planning gives you time to evaluate dependencies, licensing, commercial impact, number portability, and replacement services, and to complete testing and a phased deployment.

## Related information

[Deprecations in Dynamics 365 Contact Center](../implement/deprecations-contact-center.md)  
[Configure Teams Phone in the voice channel](configure-teams-phone-in-voice-channel.md)  
