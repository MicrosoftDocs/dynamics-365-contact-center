**Details**

On the **Details** page, configure the engagement identity, routing, and business unit.

1. In **Engagement details**, enter the following information:
   - **Name**: A name for the proactive engagement. The service representative sees the name on the conversation form.
   - **Description**: A description that helps service representatives understand the purpose of the call. The name and description are visible to representatives during the call.
   - **Workstream**: Select the outbound workstream. If you create the proactive engagement from within a workstream, this value is preselected.
   - **Channel type**: The channel used for the proactive engagement.

1. Under **Contact unique identifier**, select the contact attribute to use as the unique identifier. The dropdown lists only those attributes that are marked as unique key eligible on the Contact table. The default is **contactid**. The system performs an update or insert using this identifier. If an incoming record matches an existing contact, the record is updated. Otherwise, the system creates a new contact. Select the correct identifier to prevent duplicate contact records.

   - If Dynamics 365 Contact Center is your system of record, use **contactid** (the Dynamics 365 contact GUID).
   - If you use an external system such as a CRM or MDM system, create a custom attribute on the **Contact** table to store your external identifier, and then select the custom attribute. By passing your external system's ID in the input, you can make sure duplicates aren't created and the data in the contact center stays updated.

1. In **Routing details**, enter the following details:
   - **Primary queue**: Select a queue.
   - **Fallback queue**: The system populates the queue name based on the fallback queue set for the outbound workstream.
   - **Skills**: Select the skills required for the proactive engagement.

1. The **Business unit** field is automatically set to the business unit of the user creating the engagement. The **Owner** field shows the owner that you can change if needed.

1. Select **Next**.