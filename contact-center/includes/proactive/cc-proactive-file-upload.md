**File upload**

If you select **Upload a file** as the intake method, the **File upload** step appears where you can upload your contact list. You can skip this step to upload the file at a later time.

**Supported file formats**: CSV (.csv) only.

**File upload constraints**:

- Maximum file size: 10 MB
- The file must include all required columns; extra columns are optional
- Use the same value for ID column to link contacts in the same account

**Required columns**:

- **UniqueIdentifier**: The value used to identify and update or insert the contact record. Must correspond to the **Contact unique identifier** attribute selected in the **Details** step.
- **MobilePhoneNumber**, **BusinessPhoneNumber**, or **HomePhoneNumber**:  At least one phone number column is required. You can include multiple phone number columns.

**Optional columns**:

Named fields are columns whose names correspond to attributes on the **Contact** table. Values in these columns are used to create or update the contact record during processing. Any extra columns that don't match a **Contact** attribute are treated as pass-through data and are made available on the representative desktop during the call.

Data entered in the **Priority** column is used for custom prioritization when the call order is set to **Custom priority ascending** or **Custom priority descending**.

To download a sample file that contains the required columns and formatting, select **Download sample**.

**Processing behavior**:
Records are processed immediately when the file upload begins.

> [!NOTE]
> The uploaded file isn't stored in any form and can't be downloaded. To access delivery results and records, query the relevant tables in Microsoft Dataverse directly. Learn more in [Use proactive engagement tables for reporting](/dynamics365/contact-center/extend/proactive-engagement-tables).

**Upload a file to an existing engagement**:

To add a new file to an engagement that you already created, go to **Copilot Service admin center** > **Productivity** > **Proactive engagements**. Select the engagement, and then select **Run from file**. The system added the new file to the existing pending deliveries.