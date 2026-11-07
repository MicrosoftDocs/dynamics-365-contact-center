---
author: lalexms
ms.author: laalexan
ms.topic: include
ms.date: 11/06/2026
---
As new social networks and communication channels rapidly evolve, so do customer expectations on how to reach their favorite brands. Communication via many channels isn't only comfortable but expected, and businesses that seek to provide personalized services are rapidly working to enable support through the channels their customers want to use.

Adding channels to your business support offering is a powerful way to provide personalized service to customers on the channels of their choice. It's helpful to recognize a common pattern across all channels that are enabled through the application before diving into the implementation of a single channel.

The implementation pattern for the out-of-the-box channels is as follows:

- Establish your account and respective requirements, such as a page and app, with the channel provider. These requirements ensure that you have an entry point with the channel provider through which customers engage.
- Configure the [workstream](/dynamics365/customer-service/implement/cs-admin-center).
- Configure the channel in Copilot Service admin center and attach it to the workstream.
- Populate the exchange of handshake data, such as token and secrets required between the application and the channel provider. The data exchange is done in both places: the Copilot Service admin center app and the channel provider experience.

## License requirements

Specific licensing requirements apply for using SMS, social channels, Microsoft Teams, and custom messaging. Learn more in [Dynamics 365 Licensing Guide](https://go.microsoft.com/fwlink/p/?LinkId=866544).

Apart from Dynamics 365 subscriptions, if you choose to use any non-Microsoft channels, you need to acquire subscriptions from those providers as well.

The following channels are currently available in the application:

## Chat

If you want to help your customers using live chat, you can use the **Chat for Dynamics 365 Customer Service** channel.

Learn more in [Configure a chat channel](/dynamics365/customer-service/administer/set-up-chat-widget).

## Voice

Configure and use the voice channel to address customer issues. Learn more in [Introduction to the voice channel](/dynamics365/customer-service/administer/voice-channel).

## SMS

If you want to help your customers using SMS, you can use the following SMS channels:

- [SMS through Azure Communication Services](/dynamics365/customer-service/administer/configure-sms-channel-acs)
- [SMS through Twilio](/dynamics365/customer-service/administer/configure-sms-channel-twilio)

## Social channels

> [!NOTE]
> Support for Apple Messages for Business channel is deprecated. Learn more in [Deprecations](/dynamics365/contact-center/implement/deprecations-contact-center).

If you want to help your customers using social media, you can use the following social channels:

- [Facebook](/dynamics365/customer-service/administer/configure-facebook-channel)
- [WhatsApp through Twilio](/dynamics365/customer-service/administer/configure-whatsapp-channel)
- [LINE](/dynamics365/customer-service/administer/configure-line-channel)

## Custom messaging channel

If you want to help your customers using social channels that aren't supported as standard channels, such as Telegram, you can use the custom channels. Learn more in [Configure custom messaging application](/dynamics365/customer-service/administer/configure-custom-channel).

If you want to help your customers using your line-of-business messaging channels, you can use the [Direct Line](/dynamics365/customer-service/develop/bring-your-own-channel) Bot Framework method.

## Microsoft Teams

If you want to help your customers using a standard collaboration channel, you can use the Microsoft Teams channel.

Learn more in [Configure Microsoft Teams](/dynamics365/customer-service/administer/configure-microsoft-teams).

## Entity records

If you want to help your customers using standard entity records such as incident, quote, campaign, and so on, you can use the entity records channel.
