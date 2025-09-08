---
title: Overview of messaging APIs
description: Learn how to use the messaging APIs in Dynamics 365 Contact Center
ms.date: 04/30/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Overview of messaging APIs

Messaging APIs in Microsoft Dynamics 365 Customer Service allows developers to build tailored, service-to-service communication experiences by offering direct control over customer conversations. These RESTful APIs enable organizations to integrate a custom messaging channel without relying on client-side SDKs, libraries, or user interfaces. 

Messaging APIs are designed specifically for **service-to-service** integrations, and are suited for the following scenarios:

- End-to-end customization of the customer experience is required.
- Environments with strict network or data compliance needs.
- Bring your own custom messaging channel not natively supported in omnichannel.

Key capabilities of the Messaging APIs include:

- Programmatically start and end conversations.
- Send messages and attachments on behalf of the customer.
- Receive real-time activity updates through **webhook subscriptions** (for example, agent responses, typing indicators, or session closures).
- Manage conversation context dynamically to enrich the agent experience.

> [!NOTE] 
> Messaging APIs are intended for back-end integrations. They aren't recommended for use in mobile or web client applications where APIs are invoked directly from the user’s device. For client-to-service scenarios, we recommend that you use Microsoft’s native SDKs or chat widgets.

## Introduction to messaging API and available endpoints

The Messaging API offers a set of RESTful endpoints that allow service-to-service integration for initiating, managing, and tracking customer conversations. 

### HTTP protocol

All API requests must use **HTTPS**. 

### Host URL structure

The base URL for making API calls is constructed using the organization ID and the geographical region where your Dynamics 365 Contact Center is deployed. The format is `HTTPS://m-{org_id}.{geo}.omnichannelengagementhub.com `.



### Supported HTTP methods

- GET
- POST

### Authentication headers

All API calls must be **authenticated** using a valid Microsoft Entra access token. Each request must include the following headers:

```http
Authorization: Bearer {token}
channel-id: {custom_channel_id_guid}
organization-id: {org_id_guid}
```

Where

- **Authorization**: OAuth 2.0 bearer token.
- **channel-id**: Unique identifier of your Messaging API custom channel.
- **organization-id**: Your organization’s GUID.


> [!NOTE] 
> A `401 Unauthorized` error appears if you don't specify the authentication header when you make a call.

### API endpoints

The following endpoints are available:

| **Endpoint**                                      | **Action**                                |
| ------------------------------------------------- | ----------------------------------------- |
| `POST /conversation/create`                       | Start a new conversation                  |
| `POST /conversation/{id}`                         | Send message, typing, or end conversation |
| `GET /conversations`                              | List active conversations                 |
| `GET /conversation/{id}/messages`                 | Retrieve conversation messages            |
| `GET /conversation/{id}/context`                  | Fetch context data for a conversation     |
| `Webhook: POST /v3/conversations/{id}/activities` | Receive agent messages/events             |
