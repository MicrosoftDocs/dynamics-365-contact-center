**File upload**

If you select **Upload a file** as the intake method, the **File upload** step appears where you can upload your contact list. You can skip this step to upload the file at a later time.

**Supported file formats**: CSV (.csv) and Excel (.xlsx) only.

**File upload constraints**:

- Maximum file size: 10 MB
- The file must include all required columns; additional columns are optional

**Required columns**:

- **UniqueIdentifier**: The value used to identify and update or insert the contact record. Must correspond to the **Contact unique identifier** attribute selected in the **Details** step.
- **MobilePhoneNumber**, **BusinessPhoneNumber**, or **HomePhoneNumber**: While the least is one phone number column, you can include multiple phone number columns.

**Optional columns**:

Named fields are columns whose names correspond to attributes on the **Contact** table. Values in these columns are used to create or update the contact record during processing. Any extra columns that don't match a **Contact** attribute are treated as pass-through data and are made available on the agent desktop during the call.

Data entered in the **Priority** column is used for custom prioritization when the call order is set to **Custom priority ascending** or **Custom priority descending**.

To download a sample file that contains the required columns and formatting, select **Download sample**.

**Processing behavior**:
Records are processed immediately when the file upload begins.

> [!NOTE]
> The uploaded file isn't stored in any form and can't be downloaded after upload. To access delivery results and records, query the relevant tables in Microsoft Dataverse directly. Learn more in [Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md).

**Upload a file to an existing engagement**:

To add a new file to an engagement that you already created, go to **Copilot Service admin center** > **Productivity** > **Proactive engagements**. Select the engagement, and then select **Run from file**. The new file is added to the existing pending deliveries.