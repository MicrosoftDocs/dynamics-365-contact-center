---
title: Transparency note for real-time voice agents in Dynamics 365 Contact Center
description: This transparency note discusses real-time voice agents and the key considerations for making use of this technology responsibly.
author: neeranelli
ms.author: srubinstein
ms.reviewer: nenellim
ms.date: 04/06/2026
ms.topic: concept-article
ms.custom: bap-template
ms.collection: bap-ai-copilot
---

# Transparency note: Real-time voice agents

## What is a Transparency Note?

An AI system includes not only the technology, but also the people who will use it, the people who will be affected by it, and the environment in which it is deployed. Creating a system that is fit for its intended purpose requires an understanding of how the technology works, what its capabilities and limitations are, and how to achieve the best performance. Microsoft’s Transparency Notes are intended to help you understand how our AI technology works, the choices system owners can make that influence system performance and behavior, and the importance of thinking about the whole system, including the technology, the people, and the environment. You can use Transparency Notes when developing or deploying your own system, or share them with the people who will use or be affected by your system.  

Microsoft’s Transparency Notes are part of a broader effort at Microsoft to put our AI Principles into practice. Learn more in [Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai).

## The basics of real-time voice agents

### Introduction

Real-time voice agents in Dynamics 365 Contact Center enable organizations to create conversational, low‑latency voice experiences for calling experiences. These agents are authored in Microsoft Copilot Studio and deployed through Dynamics 365 Contact Center, allowing callers to speak naturally and receive spoken responses in real time.

Unlike traditional interactive voice response (IVR) systems that rely on separate steps for speech recognition, language understanding, and text‑to‑speech, real-time voice agents use a real‑time speech‑to‑speech architecture. This approach streams audio input and output through a real‑time multimodal model, reducing latency and enabling more fluid, conversational interactions. The system takes caller audio as input and produces spoken responses as output, while leveraging Copilot Studio for agent instructions, tools, and knowledge configuration.

### Key terms

**Microsoft Copilot Studio**: The authoring environment where makers define agent behavior, instructions, tools, and knowledge sources. 

**Dynamics 365 Contact Center**: Provides telephony integration and orchestration for voice calls and connects callers to Realtime Voice Agents. 

**Real-time voice agent**: An AI‑powered agent that conducts speech‑to‑speech conversations with callers in real time. 

**Real-time multimodal model**: The model that processes streaming audio input and generates streaming audio responses. The model being used for this release is the Azure Foundry GPT Realtime Model.

**Tool/tool call**: An action invoked by the agent (such as a workflow or connector) to retrieve or update information during a call.

**Topics**: Deterministic dialog flows that can be used for specific system or guided interaction scenarios.

## Capabilities

### System behavior

Real-time voice agents are designed to support natural, conversational voice interactions. During a call, caller audio is streamed through the telephony layer to the real‑time model, which interprets intent and generates spoken responses. Copilot Studio provides the agent’s configuration, including instructions that guide behavior and tools that allow the agent to take action or retrieve information.

Depending on configuration, the system can support IVR‑style capabilities such as call escalation, handling of key pad input, and silence detection. These capabilities allow organizations to combine conversational AI with structured contact center workflows where appropriate.

## Use cases

### Intended uses

Real-time vVoice agents in Dynamics 365 Contact Center can be used across a range of customer service scenarios. The system is intended to support routine, repeatable interactions, while enabling escalation to human agents when requests become complex, sensitive, or high‑risk.

- **Self‑service and knowledge‑based assistance**: The agent answers common questions and provides guidance using configured knowledge sources, enabling callers to resolve routine requests quickly without human involvement (for example, order status and returns in retail, policy FAQs in insurance, or hours and eligibility questions in public services). 

- **Automated task completion through tools and workflows**: The agent performs structured actions such as creating or updating records, triggering workflows, or collecting required information by invoking configured tools (for example, resetting credentials, scheduling an appointment, creating a service ticket, or sending a confirmation message). 

- **Call transfer and escalation to human agents**: The agent transfers calls to human agents when requests exceed its capabilities, require additional review, or need personalized assistance, ensuring continuity of the customer experience (for example, complex billing issues, account disputes, or case‑specific inquiries). 

- **Multilingual voice interactions**: The agent understands and responds in multiple languages, subject to supported language availability, enabling voice interactions across diverse caller populations (for example, supporting callers in different regions or offering multilingual access to customer support lines). 

### Considerations when choosing other use cases

We encourage customers to leverage real-time voice agents in Dynamics 365 Contact Center in innovative solutions and applications. When selecting a use case, the following considerations may be helpful:

- **Scope and structure of interactions**: The system is optimized for interactions where guidance can be anchored in configured knowledge, tools, workflows, or topics, while still allowing flexibility for more complex or specialized conversations when properly authored. 

- **User experience expectations**: Organizations should consider how conversational interactions are combined with structured flows, including how prompts, confirmations, and handoffs are presented to callers to ensure a clear and predictable experience. 

- **Latency and responsiveness trade‑offs**: Additional safeguards, validation steps, or processing may introduce latency, which can affect responsiveness in real‑time voice scenarios and should be evaluated during design and testing. 

- **Language, regional availability, and deployment constraints**: Multilingual experiences, regional availability, and data residency requirements may influence which use cases are appropriate and how solutions are deployed. 

- **Legal and regulatory considerations**. Organizations need to evaluate potential specific legal and regulatory obligations when using any AI services and solutions, which may not be appropriate for use in every industry or scenario. Restrictions may vary based on regional or local regulatory requirements. Additionally, AI services or solutions are not designed for and may not be used in ways prohibited in applicable terms of service and relevant codes of conduct.

## Limitations

This section describes the technical, behavioral, operational, and safety‑related factors that influence how Realtime Voice Agents behave in real‑world deployments. These limitations are intended to help system owners understand where the agent may produce unpredictable results, what risks require human oversight, and where additional safeguards or configuration choices may be needed. Some of these limitations reflect fundamental constraints of current speech‑to‑speech AI systems and are not fully mitigable through configuration alone.

### Technical limitations, operational factors and ranges**

**Technology‑related limitations**

**Voice type configuration constraints**

Real-time voice is a one‑time configuration setting; switching back to Classic requires creating a new agent. Scenarios requiring frequent voice‑type changes may experience reduced flexibility.

**Static system messaging requirements**

Certain system messages and instruction patterns must remain static to preserve performance, reliability, and privacy guarantees. Workflows dependent on frequently changing or fully dynamic prompts may not behave as intended. 

**Sensitive data handling in real‑time audio**

Comprehensive protection of sensitive data in streamed speech‑to‑speech interactions may be limited depending on release stage and configuration. Scenarios requiring strict, deterministic filtering or masking of sensitive content may face constraints. 

**Tool invocation reliability**

Tool calls may fail, time out, or return incomplete results. Real‑time workflows should include fallback behaviors, retries, or escalation pathways if tools do not respond as expected. 

**Model behavior variance**

Real-time language model outputs can vary across turns based on timing, barge‑in events, and context shifts. Highly deterministic flows should use topics, structured prompts, or tool‑driven logic instead of relying solely on generative responses.

**Turn‑taking and interruption sensitivity**

Latency, network variability, and device performance can affect interruption timing and barge‑in behavior. Scenarios requiring strict turn ordering or tightly bounded responses may require tuning.

**Multilingual consistency limitations**

Languages that haven't yet undergone full evaluation may exhibit reduced accuracy or inconsistent behavior compared to fully validated languages. Model capability does not imply general availability readiness.

**Context retention boundaries**

Very long or highly stateful conversations may exceed optimal memory retention windows, requiring explicit resets or topic boundaries to maintain predictable behavior.

**Concurrency and GPU capacity constraints**

Real-time performance is constrained by GPU availability within each region. Peak concurrency may be limited in geographies without dedicated model hosting capacity.

**Safety‑relevant behavioral limitations**

**Risk of unauthorized commitments or confident hallucinations**

Generative models may produce confident but incorrect confirmations (for example, approving donations, inferring inventory, or fabricating “offline approvals”). To mitigate this risk, customers should implement human review and approval for any commitments, compliance‑sensitive, or financial actions, and enforce these workflows through deterministic controls and escalation paths.

**Risk of information over‑disclosure**

When provided access to unscoped knowledge content, the agent may disclose information beyond what was requested, like providing all items in a file instead of limiting responses to the queried record. Guardrails depend heavily on the structure and clarity of customer‑authored instructions and knowledge boundaries. To reduce the risk of unintended or potentially harmful outputs, customers should limit the use of general knowledge for their Realtime Voice Agents and explicitly define clear instructions, scoped knowledge boundaries, and allowed behaviors.

**Inconsistent age appropriate responses**

The agent may not reliably recognize contextual indicators of age or enforce age restricted safety guidelines. Attackers can override initial age disclosures by simply stating a different age later. This reflects model level limitations that customer should mitigate by employing external verification techniques and enforcing appropriate policies.

**System instructions may not meaningfully constrain behavior**

Changes to system prompts alone may not be sufficient to prevent undesired behavior in all scenarios. To reduce risk, customers should limit general knowledge, explicitly define allowed and disallowed behaviors in their instructions, and use deterministic controls for safety critical actions rather than relying solely on free form model responses.

**Unresponsiveness during safety filter activation**

When content filters are triggered (including self-harm scenarios), the agent may stall or loop canned messages. Customers should mitigate this by (1) defining explicit escalation triggers for unresponsiveness and safety critical intents, and (2) ensuring a reliable human handoff path is available to continue support without delay.

**Operational Factors and Performance Considerations**

**Latency and responsiveness tradeoffs**

Safety validation steps, network conditions, or multiple tool calls may introduce latency. Real time use cases requiring immediate responses should be tested under production like conditions.

**Regional availability and infrastructure differences**

Model hosting, telephony infrastructure, and tool execution vary across regions. Regional GPU capacity and deployment availability may affect responsiveness, multilingual support, or quality.

**Identity and context persistence constraints**

Where identity persistence is restricted for privacy reasons, scenarios that assume stable caller identity or long-lived context may not behave predictably.

**Impact across user populations**

Differences in accents, speech patterns, background noise, or language proficiency can affect recognition accuracy and interaction quality. Accessibility and equity considerations should be assessed during deployment.

**Human and organizational limitations**

**Over reliance on AI responses**

Users may overtrust the system’s authoritative tone even when it is uncertain or hallucinating. Generative outputs should be reviewed for accuracy in workflows involving compliance, commitments, or operational risk.

**Variability in authoring quality**

Reliance on makers to write precise instructions, topics, and tool logic means incorrect or incomplete configuration may surface as agent errors, unsafe behaviors, or unintended disclosures.

## System performance

For real-time voice agents, performance refers to how accurately, reliably, and responsively the system supports voice interactions across common use cases such as self service, knowledge retrieval, tool based task completion, and call escalation. Performance is influenced by speech recognition quality, model response accuracy, tool execution reliability, and end to end latency.

Because the system operates in real time, performance should be evaluated holistically across the full interaction rather than by any single component.
Performance metrics and evaluation signals

Common metrics used to assess system performance include:

- **Speech recognition accuracy**: How accurately caller speech is transcribed across accents, speaking styles, background noise levels, and supported languages.
- **Intent or topic matching accuracy**: How often the system correctly identifies when a request can be handled through knowledge responses, tools, or escalation.
- **Task completion success rate**: Whether configured tools or workflows execute successfully and produce the intended outcome.
- **Latency and responsiveness**: The time between caller input and system response, including delays introduced by safeguards or tool calls.
- **Escalation accuracy**: How reliably the system transfers interactions to human agents when required.

Evaluation may include scripted scenario testing, simulated calls, and analysis of production telemetry. Results may vary by language, region, and configuration.
Like all AI systems, Realtime Voice Agents can produce errors. These errors may surface as misunderstandings of caller intent, incomplete answers, incorrect tool invocation, or missed escalation opportunities. Designing for errors—by including confirmations, fallbacks, and human handoff—is an essential part of deploying the system responsibly.

The following table provides illustrative examples using common voice agent scenarios.

| Outcome type | Definition | Example |
|---|---|---|
| True positive | The system correctly handles a request it was designed to support | A caller asks for order status, and the agent retrieves the correct information from a configured system |
| False positive | The system attempts to handle a request it should have escalated | A caller describes a complex billing dispute, and the agent responds with a generic answer instead of transferring |
| True negative | The system correctly escalates a request beyond its scope | A caller asks for account changes requiring manual review, and the agent transfers to a human agent |
| False negative | The system escalates a request it could have handled | A caller asks a common FAQ question, but the agent transfers instead of answering from knowledge sources |

## Best practices for improving system performance

The following practices can help improve reliability, manage error conditions, and support a consistent caller experience across different use cases:

- Design for failure and fallbacks: Include user friendly recovery behaviors when a tool call fails or times out, such as asking the caller to repeat information, offering alternate paths, or escalating to a human agent.
- Keep latency sensitive messages simple: Where greeting or first turn experiences are cached or optimized, prefer static content and avoid dynamic variable references that may introduce latency, privacy, or caching risks.
- Be deliberate about deterministic flows: When using deterministic topic flows, test how interruptions, transitions, and retries affect responsiveness and the overall user experience, especially in real time voice interactions.
- Validate across real operating environments: Test the system under expected telephony conditions, including accents, background noise, call quality, and end to end business workflows, to reduce unexpected behavior at launch.
- Tune escalation behavior intentionally: Different use cases may benefit from earlier or later escalation to human agents; adjusting this balance can affect false positives and false negatives and should be evaluated carefully.
- Monitor and iterate post deployment: Continuously review performance signals such as latency, tool success rates, and escalation frequency to identify areas for refinement and improvement.

## Evaluation of real-time voice agents

### Evaluation methods

**Evaluation Methodology**

The evaluation framework leverages an LLM-as-a-judge approach, where an independent AI model (e.g., GPT-4.1-mini and GPT-audio) evaluates the agent’s responses against predefined quality metrics (Interruption, Missed-window, Latency, Audio LLM tone, Intent determination, Intent resolution, Acknowledgement).

To ensure broad and representative coverage, we define a diverse set of evaluation scenarios spanning both positive and edge cases, closely mirroring real-world customer interactions. Synthetic conversations are generated using the customer simulator to emulate these scenarios at scale.

Test prompts are executed against the real-time voice agent, and the system captures audio recordings and recording transcripts.

Each interaction is evaluated across the following quality dimensions: Interruption, Missed-window, Latency, Audio LLM tone, Intent determination, Intent resolution, Acknowledgement. RAI evaluation is performed as well. Evaluations are conducted in:

- Single-turn mode – assessing isolated prompt–response pairs
- Multi-turn mode – evaluating full conversational context

Scoring is aggregated using configurable thresholds to determine pass/fail outcomes. Results are exported in CSV format and published to the analytics dashboard for centralized reporting and analysis.

### Dataset and environment characteristics

The evaluation dataset comprises curated test prompts organized by scenario, designed to closely mirror real-world customer interactions. Each scenario represents a realistic customer journey, including both standard (positive) flows and edge-case conditions.

For execution, each scenario is passed to the Customer Simulator (C2), which conducts a dynamic conversation with the real-time voice agent under evaluation. This setup enables end-to-end testing of conversational behavior in a controlled yet realistic environment.

The dataset is intentionally constructed to ensure comprehensive coverage, including:
•	Expected/ideal interaction paths
•	Error handling and recovery flows
•	Edge cases and boundary conditions
•	Variations in intent clarity and conversational complexity
This approach ensures that the evaluation environment reflects production-like conditions while maintaining reproducibility and consistency across test runs.

### Evaluation results

Real-time voice agents have been evaluated using a combination of automated evaluations and human review to assess conversational quality, latency, and expected behavior across common contact center scenarios. These evaluations are designed to validate fitness for purpose rather than guarantee outcomes in all production environments.

Automated evaluations are conducted using curated test scenarios and predefined quality criteria, focusing on areas such as response relevance, ambiguity handling, turn taking behavior, and tool invocation. These tests are primarily run in pre production environments with controlled inputs. As a result, they may not fully capture real world variability such as diverse accents, background noise, call center load, custom configurations, or integration differences across customer environments.

Human evaluations and structured hands on testing sessions are also used to complement automated results, particularly for assessing conversational naturalness, latency perception, and interruption behavior during live voice interactions. While this combined approach helps surface common issues and informs defaults and best practice guidance, it does not represent exhaustive testing of all possible customer use cases or operating conditions. We also completed the responsible AI assessment by testing the scenarios across harmful content categories for the contact center use cases. The system demonstrated harmful content mitigation through safety policies and guardrails.

Evaluation datasets are limited in scope and language coverage, and may emphasize representative enterprise scenarios rather than edge cases or highly specialized workflows. Additionally, some aspects of live voice interactions—such as subjective user perception, regional telephony behavior, and environmental conditions—cannot be fully simulated in automated testing. For these reasons, customers are encouraged to perform their own validation and testing in their target environments, especially for business critical scenarios, regulatory requirements, or region specific deployments.

### Evaluating and integrating real-time voice agents for your use

For real-time voice agents, best practices include training and evaluating the system using representative, real world call data, iteratively tuning prompts, confidence thresholds, and latency parameters, and validating performance across expected call volumes and accents. Varying system parameters such as response latency, interruption sensitivity, and confidence thresholds can improve naturalness and responsiveness, but may introduce tradeoffs between speed, accuracy, and conversational stability; for example, lower latency can feel more human but may increase the likelihood of incomplete or less accurate responses. Customers should test these tradeoffs in their specific use cases to determine appropriate settings. Evaluation tools such as call transcripts, confidence scores, and post call analytics can help identify failure patterns and inform tuning decisions. Appropriate human oversight is critical, including ensuring operators understand the system’s intended use, how to interpret its responses, and when to intervene. For example, in sensitive customer service scenarios, confidence scores or predefined escalation conditions can be used to route calls to human agents when uncertainty is high, helping mitigate automation bias and ensure reliable outcomes.

## Learn more about responsible AI

[Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai)  
[Microsoft responsible AI resources](https://www.microsoft.com/ai/responsible-ai-resources)  
[Microsoft Azure Learning courses on responsible AI](/learn/paths/responsible-ai-business-principles/)  

## Learn more about real-time voice agents

[Configure real-time voice agents](/microsoft-copilot-studio/voice-realtime-voice-agents)  