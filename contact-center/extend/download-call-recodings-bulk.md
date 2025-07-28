---
title: Download call recordings in bulk
description: Download call recordings in bulk in Dynamics 365 Contact Center. 
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 07/28/2025
---

# Download call recordings in bulk

You can download call recordings in bulk within a specified date range using Microsoft Dataverse APIs and Power Automate. The recordings are stored in the [msdyn_ocrecordings](/dynamics365/developer/reference/entities/msdyn_ocrecording) table and are accessible through [Shared Access Signature(SAS)](/power-apps/developer/data-platform/webapi/reference/getfilesasurl) URLs.

## Prerequisites

-  [Call recording and transcription](/dynamics365/customer-service/administer/voice-channel-configure-transcripts#enable-call-recording-and-transcription-for-voice) is enabled for voice calls.
- Required security roles to access the `msdyn_ocrecordings` table.
- Permissions to create and execute Power Automate flows.
- A designated destination for saving the recordings such as SharePoint, OneDrive, or local storage with adequate storage space.

## Create a Power Automate flows to download call recordings

To download the call recordings, you must retrieve a list of recordings within a specified date range and then generate download links for each recording. When you use this process to download call recordings, the Dataverse recording isn't deleted. Perform the following steps:

1. Sign in to [Power Automate](https://make.powerautomate.com).
2. Select **Create** to add a new manual or scheduled trigger flow.
3. Add a trigger, such as **Manually trigger a flow**, to the flow.
4. To retrieve the call recordings within the specified time range perform the following steps:
  - Add a **HTTP** action with the following configuration:
      - **Method**: GET
      - **URI**: `https://<your-org>.crm.dynamics.com/api/data/v9.2/msdyn_ocrecordings?$select=msdyn_ocrecordingid,createdon&$filter=createdon ge 2025-07-01T00:00:00Z and createdon le 2025-07-21T23:59:59Z`
      - Replace `<your-org>` with your environment URL and adjust the date range as needed.
  - Add a **Parse JSON** action to structure the API response for easier access to recording IDs and creation dates. Use the following schema:
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
5. Perform the following steps to loop through each record to generate a unique, time-limited shared access signarture URL for each individual file.
  - Add the **Apply to each** control and select the output from the Parse JSON action. This processes each recording individually to generate downloadable links.
  - Inside the loop, add an **HTTP** action with the following configuration:
     - **Method**: POST
     - **URI**: `https://<your-org>.crm.dynamics.com/api/data/v9.2/GetFileSasUrl(Target=@p1,FileAttributeName='msdyn_recording')?@p1={"@odata.id":"msdyn_ocrecordings(@{items('Apply_to_each')?['msdyn_ocrecordingid']})"}`
     - **Headers**:
      - Content-Type: application/json
      - Authorization: Bearer token (automatically handled by Dataverse connector)
  - Add another **Parse JSON** action to extract the SAS URL and filename using this schema:
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
6. You can save the recording files to a destination of your choice, such as SharePoint or OneDrive. Add a **Create file** action for SharePoint or OneDrive with the following configuration settings:
    - Site address is your SharePoint or OneDrive site URL.
    -  Folder path is the target folder location
    -  File name as `@{body('Parse_JSON_2')?['Result']?['FileName']}`
    - File content as the body of an HTTP GET request to the SAS URL.

> [!NOTE]
> - SAS URLs have a limited validity period and expire after a short time.
> - We recommend that you implement error handling for failed downloads or network issues.

