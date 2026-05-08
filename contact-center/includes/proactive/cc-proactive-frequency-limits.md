**Frequency limits**

On the **Frequency limits** page, do as follows:

1. Select **Use frequency limits** to turn on frequency controls, and then enter values for:
   - **Maximum engagements per day**: The maximum number of times you can reach a contact in a day across all channels.
   - **Maximum engagements per week**: The maximum number of times you can reach a contact in a week across all channels.

1. Under **Schedule**, select at least one phone number type and set quiet hours for each:
   - **Mobile Phone**
   - **Business Phone** (for voice channel only)
   - **Home Phone** (for voice channel only)

   For voice channel, if you select more than one number type, set the preferred contact order by using the arrows to reorder the phone numbers. The system respects the quiet hours you set for each number type and doesn't place calls during those windows. You must set quiet hours for every phone number type you select before you can proceed.

1. Under **Time zones**, select how to determine the time zone for each contact:
   - **Use customer's local time zone when available (defaults to UTC if not available)**: The system uses the time zone attribute on each contact record to evaluate quiet hours in that contact's local time. If no time zone is specified on the contact, UTC is used. You must explicitly provide the time zone value in the uploaded file or API payload - the system doesn't auto-detect or geo-infer time zones.
   - **Use Coordinated Universal Time (UTC)**: The system evaluates all contacts against quiet hours by using UTC, regardless of their location.

1. Select **Next**.