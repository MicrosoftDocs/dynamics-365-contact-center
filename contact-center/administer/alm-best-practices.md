---
title: Best practices for application lifecycle management
description: Learn about the best practices for application lifecycle management.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: conceptual
ms.collection: 
ms.date: 08/27/2024
ms.custom: bap-template
---

# Best practices for application lifecycle management

This article discusses some of the best practices for managing application lifecycle using solution components.

## Managed vs. unmanaged solutions 

When you move configurations from one environment to another, such as development to preproduction or production, we recommend that you package the configurations into an [unmanaged](/power-platform/alm/solution-concepts-alm) solution in the source environment. Then, export the unmanaged solution as a managed solution and import into the target environment.

## Environment parity

For a successful import into the target environment, maintain parity between the source and target environments. Also, make sure that the installed solutions are of the same version on the source and target environments. 

## Update of configuration and active layers

We recommend that you don't edit managed configuration records on the target environment directly. If you edit a managed configuration, you create an active customization for that configuration record that can lead to multiple issues as follows:

- The active customization can lead to a failure when you delete the managed solution containing the configuration. It happens due to the presence of multiple solution layers in which a configuration record, which is part of that managed solution, exists.

- The active layer on the managed record can prevent future configuration updates brought in from source environment from being applied onto the target environment. It can in turn lead to a bad user experience and confusion around things not working despite successful import of the latest version of the managed solution. The active layer always takes precedence over the managed layer. 

The correct approach is to import any changes to managed configuration records as part of the managed solution imports.

## Deletion of managed configuration records

You can't delete the managed configuration records on target environments in which you imported the managed solutions. The correct way to delete the imported configuration is to delete the managed solution that brought in the configuration.

### Related information

[Migrate configurations for channels using solutions](/dynamics365/customer-service/administer/migrate-channel-config-using-solutions?context=/dynamics365/contact-center/context/administer-context)  