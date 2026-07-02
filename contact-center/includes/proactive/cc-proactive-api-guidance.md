---
author: neeranelli
ms.topic: include
ms.date: 07/01/2026
ms.author: nenellim
---
Several APIs are available to create proactive deliveries. Use the following guidance to choose the right one:

- **CCaaS_CreateProactiveBulkDelivery**: Use this API to send multiple records in a single request (approximately 15,000 records). It doesn't support account calling.
- **CCaaS_CreateProactiveDelivery**: This API is the most versatile. It supports all features and channels, and account calling (multiple contacts as part of the same request). Use this API for most scenarios.
- **CCaaS_CreateSimpleProactiveDelivery**: This version doesn't require complex JSON nesting and is best suited for surfaces like Power Automate.
- **CCaaS_CreateProactiveVoiceDelivery**: This API is a first-generation voice API that doesn't support newer features. While it's supported, migrate to **CCaaS_CreateProactiveDelivery** for the latest features.
- **CCaaS_CreateProactiveSMSDelivery**: This API is a first-generation SMS API that doesn't support newer features. While it's supported, migrate to **CCaaS_CreateProactiveDelivery** for the latest features.