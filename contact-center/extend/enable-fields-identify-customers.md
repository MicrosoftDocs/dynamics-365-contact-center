---
title: Enable fields for account and contact for identifying customers
description: How to enable custom fields for account and contact for identifying customers.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.collection:
ms.date: 01/16/2025
ms.custom: bap-template 
---

# Enable fields for identifying customers

You can set a field in Dataverse for Contact and Account tables other than the default fields and identify the customer who contacts over the voice channel.

For example, if you'd like to use the Dataverse fields listed in the table for identifying a voice caller, perform the steps that follow.

| Table | Dataverse field | UI label|
|-----|-----|-----|
|Contact| `Telephone1`| Business Phone|
|Contact|`Telephone2`|Home Phone|
|Contact|`Telephone3`| Telephone 3|
|Contact|`Mobilephone`| Mobile Phone|
|Account|`Telephone1`|Main Phone|
|Account|`Telephone2`|Other Phone|

In the Dynamics 365 instance, check the record identification rules for the voice workstream as follows:

1. To look up `msdyn_recordidentificationrule`, run the following OData API.

   https://`<_org_uri_>`/api/data/v9.0/msdyn_liveworkstreams(`<_workstream_id_>`)

1. Use the following fetch XML to update the fields.

```
(" https://pt-dev.crm6.dynamics.com/api/data/v9.2/msdyn_liveworkstreams(bb4c58fe-468b-d5a3-424c-c5a965ceada2)", { method: 'PATCH', body: JSON.stringify({ "msdyn_recordidentificationrule" : “
<RecordIdentificationRuleSet>
	<RecordIdentificationRule>
		<PrimaryEntity LogicalCollectionName=\"accounts\" PrimaryKeyAttribute=\"accountid\" PrimaryNameAttribute=\"name\"/>
		<fetch version=\"1.0\" output-format=\"xml-platform\" mapping=\"logical\" top=\"2\">
			<entity name=\"account\">
				<attribute name=\"accountid\"/>
				<attribute name=\"name\"/>
				<filter type=\"and\">
					<condition attribute=\"statuscode\" operator=\"eq\" value=\"1\"/>
					<condition attribute=\"name\" operator=\"eq\" value=\"${Name}\"/>
					<filter type=\"or\">
						<condition attribute=\"telephone1\" operator=\"eq\" source=\"msdyn_msdyn_ocliveworkitem_msdyn_ocphonecallengagementctx_liveworkitemid\" value=\"${msdyn_fromphone}\"/>
						<condition attribute=\"telephone2\" operator=\"eq\" source=\"msdyn_msdyn_ocliveworkitem_msdyn_ocphonecallengagementctx_liveworkitemid\" value=\"${msdyn_fromphone}\"/>
					</filter>
					<condition attribute=\"emailaddress1\" operator=\"eq\" value=\"${Email}\"/>
				</filter>
			</entity>
		</fetch>
		<ContextKey name=\"msdyn_account_msdyn_ocliveworkitem_Customer\" isPreferred=\"false\"/>
	</RecordIdentificationRule>
	<RecordIdentificationRule>
		<PrimaryEntity LogicalCollectionName=\"contacts\" PrimaryKeyAttribute=\"contactid\" PrimaryNameAttribute=\"fullname\"/>
		<fetch version=\"1.0\" output-format=\"xml-platform\" mapping=\"logical\" top=\"2\">
			<entity name=\"contact\">
				<attribute name=\"contactid\"/>
				<attribute name=\"fullname\"/>
				<filter type=\"and\">
					<condition attribute=\"statuscode\" operator=\"eq\" value=\"1\"/>
					<condition attribute=\"fullname\" operator=\"eq\" value=\"${Name}\"/>
					<filter type=\"or\">
						<condition attribute=\"mobilephone\" operator=\"eq\" source=\"msdyn_msdyn_ocliveworkitem_msdyn_ocphonecallengagementctx_liveworkitemid\" value=\"${msdyn_fromphone}\"/>
						<condition attribute=\"telephone1\" operator=\"eq\" source=\"msdyn_msdyn_ocliveworkitem_msdyn_ocphonecallengagementctx_liveworkitemid\" value=\"${msdyn_fromphone}\"/>
						<condition attribute=\"telephone2\" operator=\"eq\" source=\"msdyn_msdyn_ocliveworkitem_msdyn_ocphonecallengagementctx_liveworkitemid\" value=\"${msdyn_fromphone}\"/>
						<condition attribute=\"telephone3\" operator=\"eq\" source=\"msdyn_msdyn_ocliveworkitem_msdyn_ocphonecallengagementctx_liveworkitemid\" value=\"${msdyn_fromphone}\"/>
					</filter>
					<condition attribute=\"emailaddress1\" operator=\"eq\" value=\"${Email}\"/>
				</filter>
			</entity>
		</fetch>
		<ContextKey name=\"msdyn_contact_msdyn_ocliveworkitem_Customer\" isPreferred=\"true\"/>
	</RecordIdentificationRule>
	<RecordIdentificationRule>
		<PrimaryEntity LogicalCollectionName=\"incidents\" PrimaryKeyAttribute=\"incidentid\" PrimaryNameAttribute=\"title\"/>
		<fetch version=\"1.0\" output-format=\"xml-platform\" mapping=\"logical\" top=\"2\">
			<entity name=\"incident\">
				<attribute name=\"incidentid\"/>
				<attribute name=\"title\"/>
				<filter type=\"and\">
					<condition attribute=\"ticketnumber\" operator=\"eq\" value=\"${CaseNumber}\"/>
					<condition attribute=\"statuscode\" operator=\"eq\" value=\"1\"/>
					<filter type=\"or\">
						<filter type=\"and\">
							<condition attribute=\"statuscode\" operator=\"eq\" value=\"1\" entityname=\"ac\"/>
							<condition attribute=\"name\" operator=\"eq\" value=\"${Name}\" entityname=\"ac\"/>
							<condition attribute=\"telephone1\" operator=\"eq\" source=\"msdyn_msdyn_ocliveworkitem_msdyn_ocphonecallengagementctx_liveworkitemid\" value=\"${msdyn_fromphone}\" entityname=\"ac\"/>
							<condition attribute=\"emailaddress1\" operator=\"eq\" value=\"${Email}\" entityname=\"ac\"/>
						</filter>
						<filter type=\"and\">
							<condition attribute=\"statuscode\" operator=\"eq\" value=\"1\" entityname=\"co\"/>
							<condition attribute=\"fullname\" operator=\"eq\" value=\"${Name}\" entityname=\"co\"/>
							<condition attribute=\"mobilephone\" operator=\"eq\" source=\"msdyn_msdyn_ocliveworkitem_msdyn_ocphonecallengagementctx_liveworkitemid\" value=\"${msdyn_fromphone}\" entityname=\"co\"/>
							<condition attribute=\"emailaddress1\" operator=\"eq\" value=\"${Email}\" entityname=\"co\"/>
						</filter>
					</filter>
				</filter>
			</filter>
			<link-entity name=\"account\" from=\"accountid\" to=\"customerid\" link-type=\"outer\" alias=\"ac\"/>
			<link-entity name=\"contact\" from=\"contactid\" to=\"customerid\" link-type=\"outer\" alias=\"co\"/>
		</entity>
	</fetch>
	<ContextKey name=\"msdyn_incident_msdyn_ocliveworkitem\"/>
</RecordIdentificationRule>undefined</RecordIdentificationRuleSet> 
“}), headers: { 'Content-type': 'application/json; charset=UTF-8' } }) .then() 
```
### Related information

[Identify your customers automatically](/dynamics365/customer-service/administer/record-identification-rule?context=/dynamics365/contact-center/context/administer-context)  
