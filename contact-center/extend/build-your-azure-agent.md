---
title: Build Azure AI agent for Dynamics 365 Contact Center
description: Learn how to build a custom Azure agent and integrate it with Dynamics 365 Contact Center. Follow step-by-step instructions to create, configure, and deploy.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 04/15/2026
ms.topic: how-to
ms.collection: bap-ai-copilot
---

# Build an Azure AI agent

This article walks you through creating a custom Azure AI agent and integrating it with Dynamics 365 Contact Center.

You learn how to:

1. Build a basic agent that sends welcome messages

1. Install and enable the Dynamics middleware
1. Integrate your agent with Dynamics 365 Contact Center
1. Implement escalation and end-conversation workflows

## Build a basic agent

Start by creating a simple agent that can receive messages and send a welcome message when a conversation starts.

### Create a project

Run the following commands:

```bash
dotnet new web -n MyDynamicsAgent
cd MyDynamicsAgent
```

### Add packages

Install the required packages:

```bash
dotnet add package Microsoft.Agents.Builder
dotnet add package Microsoft.Agents.Core
dotnet add package Microsoft.Agents.Connector
dotnet add package Microsoft.Agents.Authentication
dotnet add package Microsoft.Agents.Hosting.AspNetCore
```

### Create agent class

Create MyAgent.cs:

```csharp
using Microsoft.Agents.Builder;
using Microsoft.Agents.Builder.App;
using Microsoft.Agents.Core.Models;

namespace MyDynamicsAgent;

public class MyAgent : AgentApplication
{
        public MyAgent(AgentApplicationOptions options) : base(options)
        {
                // Handle when users join the conversation.
                OnConversationUpdate(ConversationUpdateEvents.MembersAdded, OnMembersAddedAsync);

                // Handle incoming messages.
                OnActivity(ActivityTypes.Message, OnMessageActivityAsync);
        }

        private async Task OnMembersAddedAsync(
                ITurnContext turnContext,
                ITurnState turnState,
                CancellationToken cancellationToken)
        {
                var membersAdded = turnContext.Activity.MembersAdded;
                foreach (var member in membersAdded)
                {
                        // Don't respond to the agent joining.
                        if (member.Id != turnContext.Activity.Recipient.Id)
                        {
                                var welcomeMessage = Activity.CreateMessageActivity();
                                welcomeMessage.Text = "Welcome! How can I help you today?";
                                await turnContext.SendActivityAsync(welcomeMessage, cancellationToken);
                        }
                }
        }

        private async Task OnMessageActivityAsync(
                ITurnContext turnContext,
                ITurnState turnState,
                CancellationToken cancellationToken)
        {
                var userMessage = turnContext.Activity.Text;
                var reply = Activity.CreateMessageActivity();
                reply.Text = $"You said: {userMessage}";

                await turnContext.SendActivityAsync(reply, cancellationToken);
        }
}
```

### Configure Program.cs

Update Program.cs:

```csharp
using Microsoft.Agents.Hosting.AspNetCore;
using MyDynamicsAgent;

var builder = WebApplication.CreateBuilder(args);

builder.WebHost.ConfigureKestrel(options =>
{
        options.ListenLocalhost(3979); // HTTPS
        options.ListenLocalhost(3978); // HTTP
});

// Add Agent application.
builder.AddAgentApplicationOptions();
builder.AddAgent<MyAgent, CloudAdapter>();

// Add authentication.
builder.Services.AddControllers();
builder.Services.AddAgentAspNetAuthentication(builder.Configuration);

var app = builder.Build();

app.UseAuthentication();
app.UseAuthorization();

app.UseDefaultFiles()
     .UseStaticFiles()
     .UseRouting()
     .UseEndpoints(endpoints => endpoints.MapControllers());

app.Run();
```

### Configure appsettings.json

Add the following settings:

```json
{
    "TokenValidation": {
        "Enabled": false,
        "Audiences": [
            "{{ClientId}}"
        ],
        "TenantId": "{{TenantId}}"
    },
    "AgentApplication": {
        "StartTypingTimer": false,
        "RemoveRecipientMention": false,
        "NormalizeMentions": false
    },
    "Connections": {
        "ServiceConnection": {
            "Settings": {
                "AuthType": ""
            }
        }
    },
    "ConnectionsMap": [
        {
            "ServiceUrl": "*",
            "Connection": "ServiceConnection"
        }
    ],
    "Logging": {
        "LogLevel": {
            "Default": "Information",
            "Microsoft.AspNetCore": "Warning"
        }
    }
}
```

Run the app:

```bash
dotnet run
```

The agent runs on https://localhost:3979 and http://localhost:3978.

[More samples](https://github.com/microsoft/Agents/tree/886e00f2e52e2df3f5b0ace4da65574afe5c09d7/samples)

## Install Dynamics 365 middleware

To enable your agent to work with Dynamics 365 Contact Center, you must install and configure the Dynamics 365 middleware.

### Install the middleware package

```bash
dotnet add package Microsoft.Dynamics.AgentsSDK.Middleware
```

### Create a custom adapter

Create AdapterWithErrorHandler.cs:

```csharp
using Microsoft.Agents.Builder;
using Microsoft.Agents.Core.Models;
using Microsoft.Dynamics.AgentsSDK.Middleware.Core;
using Microsoft.Extensions.Logging;

namespace MyDynamicsAgent;

public class AdapterWithErrorHandler : CloudAdapter
{
    public AdapterWithErrorHandler(
        IConfiguration configuration,
        ILogger<CloudAdapter> logger,
        IServiceProvider serviceProvider)
        : base(configuration, logger, serviceProvider)
    {
        // Add Dynamics middleware.
        Use(new OmnichannelMiddleware());

        // Add error handling.
        OnTurnError = async (turnContext, exception) =>
        {
            logger.LogError(exception, "Exception caught in adapter");
            var errorMessage = Activity.CreateMessageActivity();
            errorMessage.Text = "Sorry, something went wrong. Please try again.";
            await turnContext.SendActivityAsync(errorMessage);
        };
    }
}
```

### Update Program.cs to use custom adapter

Replace:

```csharp
builder.AddAgent<MyAgent, CloudAdapter>();
```

With:

```csharp
builder.AddAgent<MyAgent, AdapterWithErrorHandler>();
```

### Handle Dynamics 365 events

Update MyAgent.cs to handle Dynamics-specific events:

```csharp
public MyAgent(AgentApplicationOptions options) : base(options)
{
    OnConversationUpdate(ConversationUpdateEvents.MembersAdded, OnMembersAddedAsync);
    OnActivity(ActivityTypes.Message, OnMessageActivityAsync);

    // Add Dynamics event handling.
    OnActivity(ActivityTypes.Event, OnEventActivityAsync);
}

private async Task OnEventActivityAsync(
    ITurnContext turnContext,
    ITurnState turnState,
    CancellationToken cancellationToken)
{
    // Handle omnichannelSetContext event.
    if (turnContext.Activity.Name == "omnichannelSetContext")
    {
        var welcomeMessage = Activity.CreateMessageActivity();
        welcomeMessage.Text = "Welcome! How can I help you today?";

        // Bridge message so it is visible to both customer and agent.
        BridgeAgentMessage(welcomeMessage);
        await turnContext.SendActivityAsync(welcomeMessage, cancellationToken);
    }
}

private void BridgeAgentMessage(IActivity activity)
{
    var tags = new { deliveryMode = "bridged" };
    activity.ChannelData = System.Text.Json.JsonSerializer.Serialize(tags);
}
```

[Enable Agent Context for Azure Agents](/dynamics365/customer-service/develop/enable-bot-context-azure)

## Integrate with Dynamics 365

Now register your agent in Azure and connect it to the channel in Dynamics 365 Contact Center.

Learn more in [Integrate Azure Agents](/dynamics365/customer-service/administer/configure-bot-azure#integrate-azure-agents-with-contact-center).

## Implement escalation and end conversation

Add the ability to transfer conversations to service representatives and gracefully end conversations.

### Create helper class for Dynamics 365 operations

Create DynamicsAgentClient.cs:

```csharp
using Microsoft.Agents.Builder;
using Microsoft.Agents.Core.Models;

namespace MyDynamicsAgent;

public static class DynamicsAgentClient
{
    public static async Task BridgeAndSendActivityAsync(
        ITurnContext turnContext,
        IActivity messageActivity,
        CancellationToken cancellationToken)
    {
        BridgeAgentMessage(messageActivity);
        await turnContext.SendActivityAsync(messageActivity, cancellationToken);
    }

    public static async Task EscalateConversationAsync(
        ITurnContext turnContext,
        CancellationToken cancellationToken)
    {
        // Customer-facing message.
        var customerMessage = Activity.CreateMessageActivity();
        customerMessage.Text = "Let me transfer you to a live agent. One moment please.";
        BridgeAgentMessage(customerMessage);

        // Agent-facing message with context.
        var agentMessage = Activity.CreateMessageActivity();
        agentMessage.Text = "Customer requested to speak with an agent.";
        AddEscalationContext(agentMessage);

        // Send both messages.
        await turnContext.SendActivitiesAsync(
            new[] { customerMessage, agentMessage },
            cancellationToken);
    }

    public static async Task EndConversationAsync(
        ITurnContext turnContext,
        CancellationToken cancellationToken)
    {
        // Customer-facing message.
        var customerMessage = Activity.CreateMessageActivity();
        customerMessage.Text = "Thank you for contacting us. Have a great day!";
        BridgeAgentMessage(customerMessage);

        // Agent-facing message.
        var agentMessage = Activity.CreateMessageActivity();
        agentMessage.Text = "Conversation ended by customer.";
        AddEndConversationContext(agentMessage);

        await turnContext.SendActivitiesAsync(
            new[] { customerMessage, agentMessage },
            cancellationToken);
    }

    private static void BridgeAgentMessage(IActivity activity)
    {
        var tags = new { deliveryMode = "bridged" };
        activity.ChannelData = System.Text.Json.JsonSerializer.Serialize(tags);
    }

    private static void AddEscalationContext(IActivity activity)
    {
        var context = new
        {
            tags = new { deliveryMode = "bridged" },
            command = new
            {
                type = "Escalate",
                value = new { }
            }
        };

        activity.ChannelData = System.Text.Json.JsonSerializer.Serialize(context);
    }

    private static void AddEndConversationContext(IActivity activity)
    {
        var context = new
        {
            tags = new { deliveryMode = "bridged" },
            command = new
            {
                type = "EndConversation",
                value = new { }
            }
        };

        activity.ChannelData = System.Text.Json.JsonSerializer.Serialize(context);
    }
}
```

### Update your agent to use escalation and end conversation

Update MyAgent.cs:

```csharp
private async Task OnMessageActivityAsync(
    ITurnContext turnContext,
    ITurnState turnState,
    CancellationToken cancellationToken)
{
    var userMessage = turnContext.Activity.Text?.ToLower() ?? "";

    // Check for escalation request.
    if (userMessage.Contains("agent") || userMessage.Contains("human"))
    {
        await DynamicsAgentClient.EscalateConversationAsync(turnContext, cancellationToken);
        return;
    }

    // Check for end conversation request.
    if (userMessage.Contains("bye") || userMessage.Contains("end chat"))
    {
        await DynamicsAgentClient.EndConversationAsync(turnContext, cancellationToken);
        return;
    }

    // Normal message handling.
    var reply = Activity.CreateMessageActivity();
    reply.Text = $"You said: {userMessage}";

    await DynamicsAgentClient.BridgeAndSendActivityAsync(turnContext, reply, cancellationToken);
}
```

### Test escalation

1. Start a chat via live chat widget.
1. Type "I need an agent".
1. Verify the conversation transfers to a service representative queue.

### Test end conversation

1. Start a chat.
1. Type "Bye".
1. Verify the conversation closes gracefully.

### Related information

[Configure escalation and handoff](/dynamics365/customer-service/administer/configure-bot-azure#integrate-azure-agents-with-contact-center)  