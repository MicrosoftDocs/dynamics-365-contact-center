---
title: Optimize real-time agent design for customer journeys
description: Design effective real-time agents with Microsoft tools. Learn to integrate knowledge, APIs, and MCP for dynamic, reliable, and scalable interactions.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 04/03/2026
ms.update-cycle: 180-days
ms.topic: concept-article
ms.collection: bap-ai-copilot
---

# Best practices for selecting real-time voice agents

This guide walks through the best practices for building real-time agents for chat and voice by using Microsoft technologies. This guide isn't a replacement for Microsoft Copilot Studio or Dynamics 365 Contact Center documentation. It's a practical guide for people who need to **design and build real-time agents (RTA)** and want a simple way to choose the right approach based on customer journey.

In addition to this guide, Microsoft has developed templates based on real-world customer implementations that you can find on [Dynamics 365 Contact Center Forward Deployed Engineering GitHub](https://github.com/microsoft/d365cc-fde).

## Select the orchestration and voice mode

When you build an AI agent, start with one simple principle:

- Every agent's design begins by deciding how the conversation is controlled.

For voice agents, there's a second, equally important decision:

- How speech is handled end-to-end.

Conversation orchestration and speech mode shape cost, latency, flexibility, compliance, and operational complexity.

The following diagram summarizes the selection choices.

:::image type="content" source="../media/choose-orchestration-model.png" alt-text="Screenshot of orchestration model selection with Classic, Hybrid, and Generative options, plus Basic and Streaming speech mode panels.":::

### Step 1: Choose how to control the conversation

Conversation control determines who decides the next step: the author or the model.

#### Option A: Classic or deterministic orchestration

Use this option when the conversation must follow a **fixed**, **auditable path**.

In classic orchestration, you design the flow [topic by topic](/microsoft-copilot-studio/guidance/topics-overview). This approach works well for cases where the bot must ask questions in a specific order, validate answers, and follow exact rules. Topics define how the conversation progresses, and classic mode is the non-generative orchestration option. You can still use AI for the [generative Answers as part of a flow within a topic or use generative answers as a fallback.](/microsoft-copilot-studio/nlu-boost-node) When your agent can't find a matching intent (defined in a topic) for the user's query, it uses generative answers to try to answer the question.

**Best for:**

- Authentication and identity verification

- Collecting information via adaptive cards

- PCI or payment collection

- Consent capture

- Regulatory or legal wording

- DTMF menu flows

- Any journey where exact steps matter more than flexibility

**Trade‑offs:**

- Higher authoring effort

- Less flexibility in natural conversation

**Simple rule:**  
If the business says, “the bot must follow these exact steps,” start with classic or deterministic logic using topics. You can switch to other modes later.

> [!NOTE]
> All new agents use generative orchestration. Follow these steps "**[Turn off generative orchestration for an agent](/microsoft-copilot-studio/advanced-generative-actions#turn-off-generative-orchestration-for-an-agent)**" if you want to use Classic orchestration.

#### Option B: Generative orchestration

Using [generative AI](/microsoft-copilot-studio/advanced-generative-actions) to determine the *types of actions* to take in the response (tools, knowledge sources, topic invocation) and how your agent responds can make the conversation more natural and fluid for the user. An agent that uses generative AI can also perform actions autonomously.

**Use this when callers may:**

- Ask questions in many different ways

- Context awareness matters

- Naturally switch intents during the conversation without requiring explicit conditions for every possible transition

- One step correction for entities

- Anaphora

- Combine intents in a single turn

**In [generative orchestration](/microsoft-copilot-studio/advanced-generative-actions), the agent can dynamically select:**

- Topics

- Tools

- Knowledge sources

- Events other agents

This approach applies even though topics still exist. The difference is that the model decides when and how to use them rather than following a fixed path.

**Generative orchestration reduces manual scripting but raises the bar on:**

- Prompt quality

- Tool descriptions

- Guardrails

- Testing and evaluation

[Orchestrate agent behavior with generative AI](/microsoft-copilot-studio/advanced-generative-actions)

**Best for:**

- FAQ and knowledge-based interactions

- Troubleshooting

- Open-ended discovery

- Multi-step self-service that needs tool calls

- Scenarios where callers speak naturally rather than following a menu

**Trade‑offs:**

- Requires strong instructions and guardrails

- More testing investment

**Simple rule:**  
If the business says, “customers ask this question in many different ways,” generative orchestration is usually the better fit.

#### Option C: Hybrid design

Most real enterprise agents shouldn't be fully scripted or fully generative.

**Hybrid control combines:**

- Deterministic logic where risk, compliance, or precision matters

- Generative logic where flexibility improves experience

**Example:**

- Greeting and intent discovery → generative

- Identity verification → deterministic

- Capture consent before proceed → deterministic

- Knowledge lookup → generative

- Use adaptive cards or rich messages in messaging → deterministic topic

- Authentication in messaging -\> always initiates authentication topic

- Payment capture or sensitive confirmation → deterministic

- Final summary or next step guidance → generative or deterministic depending on risk

**Simple rule:**  
Don't try to make the whole journey either fully scripted or fully generative.

## (Voice only) Step 2: Choose how to handle speech

After you choose conversation control, voice agents need to make another decision: **speech architecture**.

## Pattern 1: Basic mode

**Speech → Text → [NLU/NLU +](https://learn.microsoft.com/en-us/microsoft-copilot-studio/nlu-overview) -\> [Classic orchestration](https://learn.microsoft.com/en-us/microsoft-copilot-studio/nlu-overview#classic-orchestration) -\>** **Speech**

In this pattern, the caller's speech is transcribed first, then Microsoft Copilot Studio Dialog flow processes the text, and finally, the text is converted back to speech.

**Use this** **when:**

- You're using a fully classic, deterministic flow.

- Cost minimization is critical.

- You need a custom or neural voice.

- You need fine-grained control over speech recognition.

- You're working with DTMF-heavy flows.

**Tradeoffs:**

- Works with classic orchestration only.

- Can't support hybrid or generative orchestration.

- Requires more work for multilingual and mixed-language input support, such as language detection, per-language prompts and grammar, STT locale configuration, and fallback handling.

**Important note:**  
Basic mode isn't just a "voice model choice." It fundamentally constrains orchestration.

## Pattern 2: Streaming mode 

**Speech → AI model → Speech**

A voice architecture in which a single AI model processes audio end-to-end and natively handles audio input and output. There's no separate Speech-to-Text (STT) or Text-to-Speech (TTS) step. The model receives the caller's audio stream directly and returns a synthesized audio response in real time.

This architecture is optimized for ultra low latency, natural conversational flow, and simplicity of deployment by leveraging a tightly integrated, real-time model pipeline. It's well suited for scenarios where immediacy and conversational fluidity are the primary goals, such as high-volume customer interactions in well supported languages and regions. This approach has a limited number of available voices and limited customization options.

- Key benefit: Ultra-low latency, natural conversational turn-taking.

- Availability: Initially GA in the US (April 2026), then Australia (June 2026).

**Use this pattern when:**

- Conversational naturalness and enhanced prosody are a top priority.

- The business wants a premium conversational experience.

- Superior handling of multilingual and mixed‑language input is required, including seamless language switching.

- Contextual understanding matters (tone, intent, and conversational nuance), reducing reliance on explicit translation layers.

- Low-latency, real-time responsiveness is essential to the experience.

- The team is ready to invest in testing, tuning, evaluation, and guardrails.

**Tradeoffs:**

- Fewer customization points.

- Limited voice options.

- Strong dependency on prompt quality.

- Pricing and model choice matter more.

- <span class="mark">Reasoning depth is bounded by the real‑time speech model (less flexibility to use higher‑capacity text LLM orchestration or specialized agents for complex reasoning)</span>.

- Reasoning depth with the real-time speech model is relatively lower than with text LLM orchestration, as the latter gives you the flexibility to use the strongest model available when needed.

## Prompt best practices

- JSON‑structured system prompts often produce more predictable reasoning and lower latency.

- Expect cost, latency, and quality to shift based on orchestration and speech choices.

- Model choice isn't just a technical decision—it directly impacts operational cost and user experience.

- Revisit voice architecture choices as maturity increases.

Apart from this guidance, the Microsoft Dynamics 365 Contact Center for Forward Deployment Engineering GitHub provides the template. Here are the available templates.

| **Template** | **Description and use case** | **Industry** | **Modalities** | **Orchestration** | **Speech mode** | **State** |
|---|---|---|---|---|---|---|
| Generic | Skeleton template | All | Voice | Generative | Streaming | Ready |
| [Stores Routing](https://github.com/microsoft/d365cc-fde-internal/tree/main/tools/streaming-Mode-agent-templates/retail/store-routing) | A rules‑driven AI IVR that safely and deterministically identifies customer intent, provides approved store information, and routes calls to the correct department or representative without fabricating answers. Use case: Use this IVR to handle high‑volume store calls by answering hours and service questions, sending approved shopping links by SMS (leveraging internal API Tools), and routing customers (for example, pharmacy, vision, OPD, HR) quickly and consistently to the right place. | Retail | Voice | Generative | Streaming | Ready |
| [Appointment-management](https://github.com/microsoft/d365cc-fde-internal/tree/main/tools/streaming-Mode-agent-templates/professional-services/appointment-management) | A deterministic, low‑latency IVR system that strictly identifies customers and manages appointments using validated tools and ISO‑formatted data, designed to reliably book, view, update, or route appointment‑related calls without errors or assumptions. | Financial Services | Voice | Generative | Streaming | Ready |
| Health Care Professional &amp; Patient Voice Agent | **A pharmaceutical-grade, low-latency voice IVR agent that validates HCP sample requests, recognizes and normalizes drug names from casual speech, checks live inventory and opens sample requests against backend ERP systems via API tools, and delivers****confirmed sample request numbers to HCPs over SMS while supporting patient copay and financial assistance intents****conversationally and enabling context-rich CSR escalation. Use case: Use this IVR to handle Pfizer HCP and patient inbound calls****by enforcing sample request eligibility policy, collecting structured data through natural dialogue, verifying drug names for****backend lookup, checking real-time inventory via ERP integration, creating confirmed sample requests and dispatching the request****number by SMS , and routing calls to human CSRs with full context reducing form use,callbacks,****and agent handle time** | Pharmaceuticals | Voice | Generative | Streaming | In progress |
| TBC | **Mohammad to add** | Financial Services | Voice | Generative | Streaming | In progress |
| Drug Pricing &amp; Coverage, Order status | **IVR to handle high-volume pharmacy member service calls by verifying identity once via speech or keypad (numeric and alphanumeric member IDs), then routing silently to dedicated child agents for prescription order status with sensitive medication masking, plan-specific drug pricing with brand vs. generic resolution, and DTMF-secured refill payment collection — allowing callers to switch between intents freely without re-authenticating, and reducing live agent escalation across retail, mail-order, and health plan pharmacy benefit lines.** | Retail Pharmacy / Healthcare | Voice | Generative | Streaming | In progress |
| TBC | **TBC** | Financial Services | Voice and Chat | Generative | Streaming | In progress |
|  |  |  |  |  |  |  |

## Tools, knowledge MCP, and API

In Copilot Studio streaming mode, a single generative AI model (LLM) powers the entire agent. This approach eliminates the need for traditional intent trees, rigid dialog flows, or separate orchestration layers.

Instead of stitching together multiple systems, the model acts as the brain of the agent. It dynamically decides how to respond and what actions to take in real time.

**What the generative model actually does**

The LLM handles the full conversational lifecycle:

- Understanding the user’s request (intent and entities)

- Deciding the next best action, such as:

<!-- -->

- Answering from knowledge sources

- Calling tools, APIs, or MCP integrations

- Asking for clarifying follow-up questions

<!-- -->

- Executing those actions

- Synthesizing a natural, conversational response (voice or text)

This approach represents Microsoft’s generative orchestration model. It replaces:

- Traditional NLU intent classification (Classic orchestration mode)

- Hard-coded dialog routing

- Deterministic decision trees

The result is a much more flexible, human-like interaction model.

### When to Use Knowledge vs API vs MCP

At a high level, the difference between Knowledge, APIs, and MCP comes down to what kind of answer or action is needed. Use Knowledge when the agent simply needs to explain something like policies, FAQs, play disclaimer, or general guidance by using information that doesn't change frequently. Use APIs when the agent needs real-time, customer-specific data, such as checking an order status or retrieving account details from a system of record. Use MCP when you need scale and structure. It provides a standardized way for the model to interact with multiple tools and systems in a consistent, governed manner.

In simple terms: Knowledge helps the agent talk smarter, APIs help it act on live data, and MCP helps it do both reliably across complex enterprise environments.

| **Approach** | **When to Use** | **Key Characteristics** | **Examples** | **How It Works** |
|---|---|---|---|---|
| **Knowledge (Static Content)** | Answer is static or rarely changesNo personalization requiredNo system validation needed | Fast and low costNo backend dependencyIdeal for FAQs and general info | What are your store hours?Do you offer refunds on sale items?How does your subscription plan work? | Model retrieves from knowledge baseGenerates direct response without external calls |
| **APIs (Real-Time Data)** | Need real-time transactional dataRequest is user-specificRequires authoritative system response | Dynamic and personalizedSystem of record drivenEnsures accuracy and freshness | What is my order status?Do I have any upcoming appointments?Has my refund been processed?What’s my current balance | Model detects need for live dataCalls API (Power Automate, connector, HTTP endpoint)Receives structured dataConverts to natural language response |
| **MCP (Tool Orchestration Layer)** | Need standardized, reusable integrationsMultiple systems/tools must work togetherRequire scalable, governed access for LLMs | Acts as a contract layer between model and toolsEnables orchestration across systemsSafe and more scalable for enterprise use | Pull CRM dataCheck billing systemsUpdate ticketing systemsCancel my subscription and refund the last charge if eligible | Model selects MCP toolsMCP orchestrates multiple backend systemsExecutes workflows safelyReturns structured results for response generation |

### FAQ

### Can the agent answer grounded knowledge only, or must it also take action in systems of record?

Not necessarily. You can configure agents to operate purely on grounded knowledge, without taking any action in backend systems. Copilot Studio controls this feature through knowledge and web search settings.

**When “knowledge-only” agents make sense**

Use this mode when the agent’s role is primarily informational:

- Answering FAQs

- Explaining policies

- Providing guidance or instructions

- Deflecting calls or chat

In these scenarios, the model retrieves information from configured sources and generates a response without calling any APIs.

[Knowledge sources summary](/microsoft-copilot-studio/knowledge-copilot-studio)

### How does the agent retrieve current business data, policies, and customer context in real time? 

**Grounded knowledge (static or semi-static)**

**This approach works best for policies, documentation, and structured content.**

The model uses Generative Answers, where it:

- Searches across configured knowledge sources.

- Synthesizes a response.

- Optionally cites sources.

**Supported sources include:**

- SharePoint

- Websites

- Uploaded documents

- Dataverse (indirect via flows only)  
  Dataverse isn't supported as a direct knowledge source for C2‑facing agents due to authentication requirements. You can surface Dataverse data through flows or OData calls and return it to the agent as structured results.

**Best use cases for knowledge**

- Refund and return policies

- Store hours and locations

- Eligibility rules

- Product FAQs

- Internal procedures

**Example:**

**“What’s your refund policy for online orders?”**

**→ The model retrieves policy content from SharePoint and generates a clear answer.**

## Which tasks require exact validation before execution, such as refunds, cancellations, updates, or account changes? 

> Certain actions require strict validation and must never be left to free-form AI decisions.
>
> **High-Risk Categories**

| **Category** | **Examples** | **Why It Matters** |
|---|---|---|
| Financial | Refunds, payments, credits | Financial risk |
| Account State | Cancellations, plan changes | Irreversible actions |
| Identity | Address, phone, SSN updates | Fraud&mdash;compliance |
| Legal | Consent, opt-outs | Regulatory exposure |

> **The Safe Execution Pattern**
>
> **AI decides → System validates → AI communicates**
>
> This principle ensures safe generative orchestration.
>
> Example: Refund Request

1.  Model identifies intent  
    “User wants a refund”

1.  Model gathers required details  
    Order ID, reason, timeframe

1.  API or system of record validates

    - Checks eligibility

    - Applies refund policy

    - Confirms approval or rejection

1.  Model communicates the outcome

    - Explains the result clearly

    - Doesn't invent or assume outcomes

### Clarifying a common misconception

Using a single model doesn't mean uncontrolled automation.

There's a clear separation of responsibilities.

| **Capability** | **Who Decides** | **Who Enforces** |
|---|---|---|
| Intent recognition | Model | — |
| Knowledge answers | Model | Knowledge source scope |
| API selection | Model | Tool availability |
| Validation | System of record | Backend logic |
| Final response | Model | Based on real outcomes |

### Related information

[Configure real-time voice agents](/microsoft-copilot-studio/voice-realtime-voice-agents)  

