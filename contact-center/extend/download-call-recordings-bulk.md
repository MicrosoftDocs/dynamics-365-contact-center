---
title: Download call recordings in bulk
description: Learn how to use Power Automate and Microsoft Dataverse APIs to download Dynamics 365 Contact Center call recordings in bulk.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection:
ms.date: 08/27/2026
ms.update-cycle: 180-days
---

# Download call recordings in bulk

Use Microsoft Dataverse APIs and Power Automate to download call recordings for a specified date range. The recordings are stored in the [`msdyn_ocrecordings` table](/dynamics365/developer/reference/entities/msdyn_ocrecording) and you can access them through [Shared Access Signature (SAS) URLs](/power-apps/developer/data-platform/webapi/reference/getfilesasurl).

## Prerequisites

- [Call recording and transcription](/dynamics365/customer-service/administer/voice-channel-configure-transcripts#enable-call-recording-and-transcription-for-voice) is enabled for voice calls.
- You have the required [security roles](/power-platform/admin/security-roles-privileges) to access the `msdyn_ocrecordings` table.
- Permissions to create and run Power Automate flows.
- A designated destination for saving the recordings such as SharePoint, OneDrive, or local storage with adequate storage space.

## Create a flow to download call recordings

Retrieve the recordings for a specified date range, and then generate a download link for each recording. This process doesn't delete the recordings from Dataverse. In [Power Automate](https://make.powerautomate.com):

1. Select **Create** to add a new manual or scheduled trigger flow.
1. Add a trigger, such as **Manually trigger a flow**, to the flow.
1. Retrieve the call recordings within the specified time range:
  - Add an **HTTP** action with the following configuration:
      - **Method**: `GET`
      - **URI**: `https://<your-org>.crm.dynamics.com/api/data/v9.2/msdyn_ocrecordings?$select=msdyn_ocrecordingid,createdon&$filter=createdon ge 2025-07-01T00:00:00Z and createdon le 2025-07-21T23:59:59Z`
      - Replace `<your-org>` with your environment URL, and adjust the date range as needed.
  - Add a **Parse JSON** action to structure the API response. Use the following schema:
     ```json
     {
      "type": "object",
      "properties": {
       "value": {
         "type": "array",
         "items": {
           "type": "object",
           "properties": {
             "msdyn_ocrecordingid": { "type": "string" },
             "createdon": { "type": "string" }
             }
           }
         }
       }
      }
     ```
1. Generate a unique, time-limited SAS URL for each recording:
  - Add the **Apply to each** control, and select the output from the **Parse JSON** action.
  - Inside the loop, add an **HTTP** action with the following configuration:
     - **Method**: `POST`
     - **URI**: `https://<your-org>.crm.dynamics.com/api/data/v9.2/GetFileSasUrl(Target=@p1,FileAttributeName='msdyn_recording')?@p1={"@odata.id":"msdyn_ocrecordings(@{items('Apply_to_each')?['msdyn_ocrecordingid']})"}`
     - **Headers**:
      - Content-Type: application/json
      - Authorization: Bearer token (automatically handled by Dataverse connector)
  - Add another **Parse JSON** action to extract the SAS URL and file name. Use this schema:
     ```json
     {
      "type": "object",
       "properties": {
        "Result": {
         "type": "object",
         "properties": {
           "SasUrl": { "type": "string" },
           "FileName": { "type": "string" }
          }
         }
       }
     }
    ```
1. Add a **Create file** action for SharePoint or OneDrive with the following settings:
    - **Site address**: Your SharePoint or OneDrive site URL.
    - **Folder path**: The target folder location.
    - **File name**: `@{body('Parse_JSON_2')?['Result']?['FileName']}`
    - **File content**: The body of an HTTP `GET` request to the SAS URL.

> [!NOTE]
> - SAS URLs have a limited validity period and expire after a short time.
> - We recommend that you implement error handling for failed downloads or network issues.
