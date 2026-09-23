---
author: neeranelli
ms.topic: include
ms.date: 09/23/2026
ms.author: nenellim
---

## Validate the migration

After the production cutover, validate the following scenarios:

- The target service shows the phone numbers, carrier or trunk, and emergency configuration as active.
- Incoming calls reach the correct Dynamics 365 Contact Center resource account, queue, and representative.
- Outgoing calls use the expected route and display the correct caller identification.
- Transfers, consult calls, voicemail, and routing work as expected.
- Emergency calling provides the correct location information where applicable.
- Call quality and service health don't show unexpected errors.

Monitor the migrated configuration during the initial production period. Before you remove old routes, release phone numbers, or stop Azure Communication Services billing, confirm that the migration is stable and that no workload depends on the previous configuration.
