---
title: Configure data masking for screen recordings
description: Blur sensitive information in Dynamics 365 screen recordings automatically. Learn how to connect Azure AI services and choose which payment card industry (PCI) and personally identifiable information (PII) fields to mask.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.date: 10/22/2026
ms.custom: bap-template 
---

# Configure data masking for screen recordings

Screen recordings can capture sensitive information that appears on the screens of customer service representatives (service representatives or representatives), including information in applications outside Dynamics 365. Sensitive information might include payment card numbers, government-issued identifiers, passwords, and other regulated data.

Data masking detects selected types of sensitive information in captured frames and blurs the corresponding regions before the recording is available for playback or download. Supervisors, evaluators, and auditors can then review the masked recording without viewing the detected values.

> [!NOTE]
> Data masking is one control in a broader compliance program. It reduces the exposure of sensitive data in recordings, but it doesn't guarantee that every sensitive value is detected in every frame. Detection accuracy depends on the Azure AI Vision and Azure AI Language services that you connect. Review the [Optical character recognition (OCR) transparency note](/azure/ai-foundry/responsible-ai/computer-vision/ocr-transparency-note) and the [Personally identifiable information (PII) detection transparency note](/azure/ai-foundry/responsible-ai/language-service/transparency-note-personally-identifiable-information) before you rely on data masking. Combine masking with the role-based access and retention controls described in [Configure screen and audio recording with the desktop companion application](configure-screen-recording.md).

You can select the categories of information to mask. For example, you can mask card numbers and passwords for payment card industry (PCI) compliance while leaving customer names visible when evaluators need that context to review an interaction.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. <br> 
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Prerequisites

Before you configure data masking, make sure that the following requirements are met:

- Screen recording is turned on for your organization. Learn more in [Configure screen and audio recording with the desktop companion application](configure-screen-recording.md).
- You have an Azure AI services resource in your Azure subscription that provides the following capabilities.
  - **Azure AI Vision**: Provides the **Read** OCR capability that locates text in recorded frames.
  - **Azure AI Language**: Provides the PII detection capability that classifies the extracted text.
  You can provide both capabilities through one multiservice Azure AI services resource or through two separate resources. Learn more in [What is Azure AI Vision?](/azure/ai-services/computer-vision/overview) and [What is PII detection in Azure AI Language?](/azure/ai-services/language-service/personally-identifiable-information/overview).
- The Azure AI services resource is provisioned in a region that meets your organization's data residency requirements. Frames are processed in the region where the resource is provisioned, which isn't necessarily the region of your Dynamics 365 environment.

> [!NOTE]
> Azure AI services usage is billed to your Azure subscription separately from your Dynamics 365 licenses. The cost depends on the volume and length of the recordings processed.

## How data masking works

When you turn on data masking, each screen recording goes through the following process before it's available for review:

- The desktop companion application uploads the recording to your Dataverse environment.
- The service samples frames from the recording and sends them to the configured **Azure AI Vision Read** endpoint.
- The **Read** capability extracts the text from each frame and returns the coordinates of each text region.
- The extracted text is sent to the configured Azure AI Language PII detection endpoint.
- The PII detection capability identifies values that belong to the sensitive-field categories you selected.
- The corresponding regions are blurred in the recording.
- The masked recording is stored and made available to authorized users for playback or download.

Because data masking processes text that appears on the screen, it can mask sensitive information displayed in any application that the representative uses, not just Dynamics 365 applications.

## Supported sensitive fields

Select the sensitive fields that align with your organization's compliance requirements. Selecting fewer fields can help reviewers retain more context and reduce processing volume. Selecting more fields increases the range of information that the service attempts to detect and mask.

### PCI data

| Field | What it masks |
|---|---|
| Card number | Primary account numbers for credit and debit cards. |
| CVV | Card verification values. |
| Expiry date | Card expiration dates. |
| PIN | Personal identification numbers entered or displayed during payment. |

### PII data

| Field | What it masks |
|---|---|
| Account number | Customer or financial account identifiers. |
| Person name | Names of individuals. |
| Social Security Number (SSN) | US Social Security numbers. |
| Government ID number | National or regional government-issued identifiers. |
| Date of birth | Dates of birth. |
| Tax ID number | Taxpayer identification numbers. |
| Phone number | Telephone numbers. |
| Residential address | Street addresses and other home address details. |
| Email address | Email addresses. |
| Passport number | Passport numbers. |
| Driver license number | Driver's license numbers. |

### Sensitive credentials

| Field | What it masks |
|---|---|
| Password | Passwords and similar secrets that appear as plain text on the screen. |

## Enable data masking

Before you enable data masking, assign the required roles.

### Grant access to the Azure AI services resource

Dynamics 365 authenticates to the Azure AI services resource by using Microsoft Entra ID. Assign the **Cognitive Services User** role on the resource to the Dynamics 365 service principal in your tenant. Learn more in [Authenticate requests to Azure AI services](/azure/ai-services/authentication?branch=main). The Dynamics 365 service principal has the following format: `[<orgname>] <Azure AI services multiservice account name> <timestamp>`. For example, `[contosocrm] screen-recording-redaction 20260925T181302Z`.

If the Azure AI services resource restricts network access, allow traffic from the region of your Dynamics 365 environment so that frames can be submitted for processing.

To enable data masking in Copilot Service admin center, perform the following steps:

1. In the site map of Copilot Service admin center, select **Quality management agent**.
1. For **Enable screen and call recording**, select **Manage**.
1. On the **Enable screen and call recording** page, confirm that **Turn on screen recording** is set to **On**.
1. Set **Enable data masking** to **On**.
1. Under **Azure Service endpoint URL**, enter the [applicable endpoints](#find-the-azure-ai-service-endpoints):
   - **Azure Vision Read Endpoint**: Enter the endpoint of the resource that provides the **Read** capability. Use the following format: `https://your-resource-name.cognitiveservices.azure.com/`.
   - **Azure PII Language Endpoint**: Enter the endpoint of the resource that provides PII detection. If both capabilities use the same multiservice resource, select **Azure PII same as Azure Vision Read Endpoint**. The endpoint field gets populated automatically.
1. Under **Sensitive fields to mask**, expand **PCI data**, **PII data**, and **Sensitive credentials**, and then select the fields to mask.
   - To select every field in a category, select **Select all**. To clear them, select **Clear all**.
   - The number next to each category indicates how many fields are selected.
1. Select **Save**.

### Find the Azure AI service endpoints

1. Sign in to the [Azure portal](https://portal.azure.com/) and open your Azure AI services resource.
1. In the left pane, select **Resource Management** > **Keys and Endpoint**.
1. Copy the value of **Endpoint**.
1. Paste the endpoint into the applicable field in Copilot Service admin center. Ensure that the endpoint includes the trailing slash.

If Azure AI Vision and Azure AI Language use separate resources, repeat these steps for each resource.

> [!NOTE]
> Data masking remains unavailable until you provide valid endpoint URLs. If the endpoint fields are empty or the resources can't be reached, recordings continue to be captured, but they aren't masked.

Configuration changes apply to recordings that are processed after you save the settings. Recordings that were already processed aren't masked retroactively.

## Verify data masking

Before you enable data masking for all representatives, validate the configuration in a controlled test environment.

1. Ask a representative in the test environment to start a screen recording.
1. Display test values (not real customer data) for each sensitive-field category that you selected.
1. End the recording, and allow it to upload and finish processing.
1. In Copilot Service workspace, go to **Screen Recordings**.
1. Open and play the test recording.
1. Verify that:
   - Values that belong to the selected fields are blurred.
   - Values for fields that you didn't select remain visible.

If selected values aren't blurred, check that:

- The Azure AI service endpoints are entered and saved correctly.
- The Azure AI services resources are reachable.
- The appropriate field is selected under the correct category.

## Considerations and limitations

Consider the following limitations before you enable data masking:

- **Masking is irreversible**: Authorized users can't view or recover the original content of a masked region. If your organization requires unmasked recordings for a specific investigative scenario, evaluate whether masking is appropriate for that workload.
- **Detection isn't guaranteed.** Masking depends on optical character recognition and language-based detection. Values might not be detected if they're rendered as images, heavily stylized, obscured by overlapping windows, displayed at low resolution, or visible only briefly. A nonsensitive value might be masked if it resembles a sensitive pattern. For example, a case number that resembles an account number might be blurred.
- **Audio isn't masked.** Data masking applies only to the visual content of screen recordings. To mask sensitive information in chat and asynchronous conversations, use [data masking rules](/dynamics365/customer-service/administer/data-masking-settings). For voice agent interactions, use the [sensitive data setting in Microsoft Copilot Studio](/microsoft-copilot-studio/voice-sensitive-data).
- **Configuration applies across the environment.** The selected fields apply to every screen recording captured in the environment. You can't configure different selections for individual workstreams, queues, or representatives.
- **Processing adds latency.** A masked recording is available for playback only after masking is complete. It might become available later than an unmasked recording of comparable length.
- **Detection accuracy varies by language.** Accuracy depends on the languages supported by Azure AI Vision and Azure AI Language. Learn more in [Language support for Azure AI Vision](/azure/ai-services/computer-vision/language-support) and [Language support for PII detection](/azure/ai-services/language-service/personally-identifiable-information/language-support).

## Related information

- [Configure screen and audio recording with the desktop companion application](configure-screen-recording.md)
- [Create and manage data masking rules](/dynamics365/customer-service/administer/data-masking-settings)
- [Remove sensitive data](/microsoft-copilot-studio/voice-sensitive-data)
- [What is Azure AI Vision?](/azure/ai-services/computer-vision/overview)
- [What is PII detection?](/azure/ai-services/language-service/personally-identifiable-information/overview)
- [Dataverse long-term data retention overview](/power-apps/maker/data-platform/data-retention-overview)