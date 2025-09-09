---
title: Overview of messaging APIs
description: Learn how to use Dynamics 365 Customer Service or Contact Center messaging APIs to build custom service-to-service communication experiences with RESTful endpoints.
ms.date: 09/10/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---


# Overview of messaging APIs

Messaging APIs let developers build tailored, service-to-service communication experiences by giving direct control over customer conversations. These RESTful APIs let organizations integrate a custom messaging channel without relying on client-side SDKs, libraries, or user interfaces. 
Messaging APIs are designed specifically for **service-to-service** integrations and are suited for the following scenarios:

- End-to-end customization of the customer experience is required.
- Environments with strict network or data compliance needs.
- Bring your own custom messaging channels that aren't supported in omnichannel.

Key capabilities of the messaging APIs include:

- Programmatically start and end conversations.
- Send messages and attachments on behalf of the customer.
- Receive real-time activity updates such as agent or customer service representative (service representative or representative) responses, typing indicators, or session closures through webhook subscriptions.
- Manage conversation context dynamically to enrich the customer service representative experience.

> [!NOTE] 
> Messaging APIs are intended for back-end integrations. They're not recommended for use in mobile or web client applications where APIs are invoked directly from the user’s device. For client-to-service scenarios, we recommend that you use Microsoft’s native SDKs or chat widgets.

## Understand messaging APIs and available endpoints

The Messaging API offers a set of RESTful endpoints that allow service-to-service integration for initiating, managing, and tracking customer conversations. 

### HTTP protocol

All API requests must use **HTTPS** for secure communication. 

### Host URL

The base URL for making API calls uses the organization ID and the geographical region where your Dynamics 365 Contact Center is deployed. The format is `https://m-{org_id}.{geo}.omnichannelengagementhub.com`.



### Supported HTTP methods

- **GET**
- **POST**

### Authentication headers

All API calls must include a valid Microsoft Entra access token for authentication. Each request must include the following headers:

```http
Authorization: Bearer {token}
channel-id: {custom_channel_id_guid}
organization-id: {org_id_guid}
```

Where:

- **Authorization**: OAuth 2.0 bearer token.
- **channel-id**: The unique identifier of your Messaging API custom channel.
- **organization-id**: The GUID of your organization.


> [!NOTE] 
> A `401 Unauthorized` error occurs if you don't include the authentication header in your API call.

### API endpoints

The following endpoints are available:

| **Endpoint**                                      | **Description**                           |
| ------------------------------------------------- | ----------------------------------------- |
| `POST /conversation/create`                       | Start a new conversation                  |
| `POST /conversation/{id}`                         | Send message, typing, or end conversation |
| `GET /conversations`                              | List active conversations                 |
| `GET /conversation/{id}/messages`                 | Retrieve conversation messages            |
| `GET /conversation/{id}/context`                  | Fetch context data for a conversation     |
| `Webhook: POST /v3/conversations/{id}/activities` | Receive messages/events             |
