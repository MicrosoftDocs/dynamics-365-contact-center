---
title: "Application card: Biometric authentication and fraud detection"
description: Learn how the biometric authentication and fraud detection is built with responsible AI in mind, and the steps you can take to use AI tools responsibly.
author: timsavage
ms.author: timsavage
ms.reviewer: puneetsingh
ms.topic: reference
ms.date: 11/20/2026
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.custom: 
    - bap-template
    - ai-gen-docs-bap
    - ai-seo-date: 11/09/2026
ai-usage: ai-assisted
---

# Application card: Biometric authentication and fraud detection

## What is an Application or Platform Card?

Microsoft's Application and Platform cards are intended to help you understand how our AI technology works, the choices application owners can make that influence application performance and behavior, and the importance of considering the whole application, including the technology, the people, and the environment. Application cards are created for AI applications and platform cards are created for AI platform services. These resources can support the development or deployment of your own applications and can be shared with users or stakeholders impacted by them.

As part of its commitment to responsible AI, Microsoft values [six core principles](https://www.microsoft.com/ai/principles-and-approach#ai-principles): fairness, reliability and safety, privacy and security, inclusiveness, transparency, and accountability. These principles are embedded in the [Responsible AI Standard](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/Microsoft-Responsible-AI-Standard-General-Requirements.pdf?culture=en-us&country=us), which guides teams in designing, building, and testing AI applications. Application and Platform Cards play a key role in operationalizing these principles by offering transparency around capabilities, intended uses, and limitations. For further insight, readers are encouraged to explore Microsoft's [Responsible AI Transparency Report](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/msc/documents/presentations/CSR/Responsible-AI-Transparency-Report-2026.pdf) and Code of Conduct, which outline how [enterprise customers](/legal/ai-code-of-conduct) and [individuals](https://www.microsoft.com/servicesagreement) can engage with AI responsibly.

## Overview

Biometric authentication and fraud detection are AI-enabled capabilities. Biometric authentication is natively integrated within Dynamics 365 Contact Center (D365) and Contact Center Intelligence platforms; fraud detection is only natively integrated within D365 Contact Center. At a high level, these capabilities analyze audio signal that contains speech and unique vocal characteristics that are not dependent on language. The purpose is to compare caller audio to enrolled voiceprints while checking for artifacts of synthesized speech and recorded audio. Two distinct, independently configurable features are supported.

- **Biometric authentication** (applies to both Dynamics 365 Contact Center and Contact Center Intelligence platforms) can be leveraged in both a human-to-bot and human-to-human interactions. Before a caller's voice can be used to create a voiceprint and for authentication, you must get the caller's consent. After you confirm you have received legally sufficient consent from the caller, enrollment proceeds and biometric authentication creates and stores a voiceprint within your Dataverse environment. Caller speech is collected to create a voiceprint that is used in future interactions for voice authentication by associating it to the caller identifier. Once a voiceprint has been successfully created, it can be retrieved and used to compare the voice of the caller to the voiceprint. The service also analyzes caller audio for indicators of synthetic speech or prerecorded audio that may be used to impersonate another person. Synthetic speech and playback detection provide additional signals that you can consider alongside voice biometric authentication and other authentication methods when assessing whether additional verification or review is appropriate.

- **Fraud detection** (only applies to Dynamics 365 Contact Center) is a voice-based service that compares caller audio to your fraud watchlist that you create, alerting your fraud analysts and/or contact center representatives that a potential match has been detected. Fraudster voiceprints are created from a dedicated fraud analyst user interface by authorized users from your organization. Once fraud detection is enabled on a Workstream all interactions create a fraud case. Historical interactions are reviewed by your fraud analysts who create fraudster voiceprints; once created they are added to your watchlist. Watchlists are then compared to incoming calls and matches that surpass your configured threshold generate a fraud alert for fraud analysts and/or customer service representatives depending on your configuration. All data resides within your Dataverse tenant. Customers enable and control relevant thresholds and remain responsible for notice, consent, watchlist governance, fraud-risk determinations, and actions taken after reviewing the result.

## Key terms

The following list provides a glossary of key terms related to biometric authentication and fraud detection:

**Biometric authentication (applies to both Dynamics 365 Contact Center and Contact Center Intelligence platforms):**

- **Biometric authentication:** A process for evaluating a caller's claimed identity by comparing the caller's voice to the voiceprint associated to the claimed caller identifier. The output is a signal for your authentication process, not an independent determination of a caller's legal identity.

- **Caller:** The end-user who is engaging over a voice channel with a contact center customer service representative or contact center voice agent. The caller is the customer's end-user.

- **Caller identifier:** A unique identifier that the customer attributes to their end users for identification and authentication purposes.

- **Customer or "you":** Microsoft's customer who acquires, configures and deploys Microsoft D365 Contact Center or Contact Center Intelligence voice agent application(s). The customer establishes and maintains the relationship with the caller. The customer is the intended reader of this document.

- **Imposter:** A caller who is not the true user of their claimed caller identifier.

- **False acceptance rate:** The percentage of imposter callers who receive a positive authentication decision.

- **False rejection rate:** The percentage of genuine callers who receive a negative authentication decision.

- **Fraud detection:** A process where incoming calls are checked against your watchlist. When a caller's voice matches a fraudster on the customer's watchlist, the application generates an alert for your customer service representatives, fraud analysts, or both.

- **Fraudster:** A caller whose voice is present on your watchlist.

- **Playback detection:** Detection of previously captured audio that's replayed during the call through a loudspeaker.

- **Synthetic speech detection:** Detection of artificially generated speech, such as text-to-speech or voice-cloned audio.

- **Voiceprint:** A numerical representation of characteristics of a person's voice that can be used for comparison to determine the probability that they match the enrollment audio. All voiceprints, enrollment audio and associated metadata are stored within the customer's Dataverse environment. Data retention policies are governed by the customer. It is biometric data and should be handled in accordance with applicable privacy and biometric laws.

**Fraud detection (only applies to Dynamics 365 Contact Center):**

- **Fraud alert:** When a caller's voice is similar to that of a voice on your fraud watchlist, the system generates an alert for your customer service representatives, fraud analysts, or both.

- **Fraud watchlist:** A customer-created and customer-maintained collection of fraud voiceprints associated with suspected or confirmed fraud according to the customer's own processes.

## Key features or capabilities

The key features and capabilities outlined here describe what biometric authentication and fraud detection are designed to do and how they perform across supported tasks.

**Audio quality assessment:** The service assesses whether the audio is suitable for biometric use and can return quality-related outputs, including that audio is too noisy or too soft. This helps avoid relying on comparisons made from unsuitable audio.

**Biometric authentication (applies to both Dynamics 365 Contact Center and Contact Center Intelligence platforms):**

- **Voice biometric enrollment:** After consent is granted by the caller, biometric authentication collects your customer's speech to build a voiceprint. The service converts that speech into a secure mathematical representation and associates it with your caller identifier and stores it within your Dataverse environment. The voiceprint—not the raw audio—is what biometric authentication uses for later comparisons.

- **Voice authentication:** On future calls, biometric authentication retrieves the caller's voiceprint using the caller's identifier and compares the caller's live speech against the stored voiceprint stored within your Dataverse environment. During this comparison, the service evaluates three kinds of signals:

  - **Speaker similarity:** how closely the caller's voice matches the enrolled voiceprint.
  - **Synthetic speech detection:** whether the audio contains suspected non-natural speech patterns.
  - **Playback detection:** whether the audio contains artifacts of being emitted from a loudspeaker.

  Biometric authentication combines these three signals into an authentication decision.

- **Caller consent UI:** Customer supervisors may use a dedicated consent management user interface to look up your caller's voice-authentication data and manage it. You can review your caller's historical authentication activities, consent status, enrollment details, change their consent, lock or unlock their voiceprint stored within your Dataverse environment, and delete their voice-authentication data when needed.

**Fraud detection (only applies to Dynamics 365 Contact Center):**

- **Fraud alert case management:** Fraud detection, for each incoming call, creates a case in the Biometric authentication and fraud detection app. A fraud analyst from the customer's organization reviews these cases to investigate suspicious calls, assign work to the right analyst, flag callers as fraud and create fraud voiceprints. All fraud voiceprints are created from the dedicated user interface by authorized users from your organization. The service does not make any fraud-risk determinations. All data resides within your Dataverse tenant.

- **Fraud watchlist:** A collection of fraud voiceprints owned and maintained by your organization.

**System optimization (applies to both Dynamics 365 Contact Center and Contact Center Intelligence platforms):**

This user interface is designed for customer admins to monitor and configure decisioning thresholds. It shows the volume and outcome of each factor so that you can see how often each control runs:

- **Authentication outcomes:** The proportion of successful and unsuccessful voice authentication attempts.

- **False accepts:** The actual false-accept rate observed in your environment. To measure this rate, biometric authentication and fraud detection runs background imposter tests: after a voiceprint authenticates a caller, a parallel process uses caller's audio to attempt authentication against a voiceprint that isn't theirs. None of these tests should succeed, so any success is counted as a false accept. This metric lets you see how secure your current configuration is at any time.

- **Synthetic speech alert rate:** The percentage of enrollment and authentication interactions that exceeded the synthetic-speech threshold.

- **Playback alert rate:** The percentage of enrollment and authentication interactions that exceeded the playback threshold.

**Tune thresholds:** This section predicts the effect of a threshold change by using your production data. Enter a target rate, and the tool calculates the configuration threshold needed to achieve it.

- False accepts (voice authentication)
- Synthetic speech (voice authentication and enrollment)
- Playback alert rate (voice authentication and enrollment)

## Intended uses

Biometric authentication and fraud detection can be used in multiple contact-center scenarios across a variety of industries. Some examples of intended use cases include:

**Biometric authentication (applies to both Dynamics 365 Contact Center and Contact Center Intelligence platforms):**

- Streamlined authentication in the voice channel. Identity verification runs automatically as the caller speaks, so callers don't have to answer a series of security questions.

- Reduced call handle time. Authentication occurs passively in the background of a normal conversation. Authentication decisions are rendered during call introductions and intent capture.

- Higher authentication success rates. Because biometric authentication doesn't depend on PINs, passwords, one-time passcodes, or access to a trusted phone or email, more callers can be authenticated successfully.

- A better representative experience. Contact center representatives spend less time asking knowledge-based questions and can focus on resolving the caller's issue.

- An additional factor for a multifactor strategy. A voiceprint can serve as one factor alongside other verification methods.

- Real-time protection against spoofing. Detection of non-natural speech patterns, synthetic (AI-generated) speech, and recorded playback to help block impersonation attempts as they happen.

**Fraud detection (only applies to Dynamics 365 Contact Center):**

- Real-time protection against fraudster attacks in the voice channel. Fraud detection matches live speaker audio against fraudster voices on your watchlist. It can alert your customer service representatives via a desktop widget and fraud analysts in real time when it detects a potential match reducing fraud losses, protecting caller accounts and simplifying fraud controls.

- Simplified fraud detection performance management. The service includes a dedicated fraud analyst UI to work fraud alerts, provide human feedback, and create and manage your fraudster voiceprints.

- Unified performance monitoring of fraud alerts, fraud voiceprints, fraud watchlists and impact of fraud alerting on customer service operations.

## Models and training data

Biometric authentication and fraud detection use a proprietary Microsoft owned and maintained model to power the experience. The model includes a speaker-recognition framework used for caller authentication and fraud-watchlist matching, together with synthetic-speech detection and playback-detection models. The underlying speaker-recognition capabilities are text independent, meaning the caller does not need to repeat a fixed phrase.

The primary training data set is Defined.AI contact-center corpora, chosen because they match the deployment domain closely: simulated contact center 8khz audio conversations with varying business context across banking, insurance, healthcare, telecommunications and retail verticals. Microsoft licensed this material with commercial rights to build speaker recognition benchmarks, subject to a restriction on redistribution.

The primary speaker recognition benchmark is built on licensed Defined.AI contact-centre corpora with speaker identity labels for both parties and coverage of 32 languages across 143 telephonic datasets.

The intended scale for ongoing platform-level evaluation is roughly 3,000 audio files per language, producing about 10,000 genuine and 30,000 impostor trials, which is sufficient to measure false rejection at the very low false acceptance rates voice biometric applications target.

## Performance

The application is designed for live 8khz contact-center audio containing speech. Performance is strongest when the audio signal contains sufficient speech, the caller's voice is captured clearly, and the audio is not excessively noisy, soft, clipped, synthetic, or replayed. The input modality is audio signal. Outputs are voice-authentication scores, fraud-watchlist match scores, synthetic-speech scores, playback scores, and audio-quality signals. The models are language agnostic, and the domain-matched evaluation benchmark includes 32 languages.

## Limitations

Understanding biometric authentication and fraud detection's limitations is crucial to determine if it is used within safe and effective boundaries. While we encourage customers to leverage biometric authentication and fraud detection in their solutions, these features were not designed for every possible scenario. We encourage users to refer to either the [Microsoft Enterprise AI Services Code of Conduct](/legal/ai-code-of-conduct) as well as the following considerations when choosing a use case:

- **Audio quality can materially affect accuracy:** Noisy, very soft, or clipped audio can increase recognition errors before a comparison is scored. In testing, audio below 5 dB signal-to-noise had an equal error rate 1.74 times that of clean audio, and heavily clipped audio also increased error. Customers should use the available quality outputs, retry or use another authentication path when audio is unsuitable, and avoid treating a low-quality comparison as conclusive.

- **Outputs are probabilistic signals:** A match or no-match result can be incorrect. The application does not independently establish legal identity, determine that a person committed fraud, or replace a customer's investigation. Customers should combine outputs with other evidence and apply human review before consequential or adverse action.

- **Threshold choices create trade-offs:** A stricter threshold may reduce false acceptances but increase false rejections for legitimate callers. A more permissive threshold may improve convenience while increasing security risk. Customers should validate thresholds for each use case rather than applying a default setting without testing. Tests carried out in optimistic conditions or using inappropriate configurations may increase the rate of incorrect decisions.

- **Fraud watchlists can contain errors (only applies to Dynamics 365 Contact Center):** The application compares audio against the watchlist provided and maintained by the customer. An incorrect enrollment, outdated designation, or poorly governed watchlist can cause inappropriate alerts. Customers should establish documented criteria, access controls, review periods, correction procedures, and deletion processes for watchlist entries.

- **Demographic performance disparities may remain:** Fairness testing measures differences in false acceptance and false rejection rates using a common operating threshold. Even where acceptance criteria are met, residual differences may affect groups differently. Customers should test with representative populations, monitor outcomes, and maintain an appeal or correction path.

- **Prohibited uses:** Customers may not use the fraud detection outputs, including match or no-match results, to evaluate, determine, or inform eligibility for credit, employment, insurance, housing, or another purpose governed by the Fair Credit Reporting Act or similar laws. The Fraud detection functionality is intended only for fraud prevention and authentication and does not generate consumer reports.

## Evaluations

Performance and safety evaluations assess whether AI applications are operating reliably and securely by examining factors like groundedness, relevance, and coherence while identifying the risks of generating harmful content. The following evaluations were conducted with safety components already in place, which are also described in [Safety components and mitigations](#safety-components-and-mitigations).

### Performance and quality evaluations

Customers independently evaluate and control model performance through speech settings, threshold configuration for authentication, synthetic-speech detection, playback detection, and fraud detection. Using the System optimization UI feature, customers can observe actual model performance within their production environment based on their production data. Customer configuration choices directly affect outcomes, customers should validate threshold settings using representative data and monitor false acceptances, rejections, quality failures, escalations, and review fraud watchlist entries after deployment.

Model performance is evaluated by Microsoft using equal error rate and false rejection rate at fixed false acceptance rates of 1.0% and 0.5%. These measures characterize the trade-off between security and convenience. An ideal deployment maintains a low false rejection rate at a strict false acceptance target; a suboptimal deployment reaches acceptable convenience only by relaxing security or uses thresholds that were not validated for the deployment environment.

A variable-duration sweep measures accuracy across enrollment durations of 3 to 30 seconds against verification durations of 1 to 15 seconds, establishing how the engine behaves outside the configured operating range, and a focused sweep covers the exact enrollment and verification durations used by the application. Performance is evaluated separately for the languages with enough surplus speakers, using 119 calibration speakers for Arabic, 139 for American English, 59 for Canadian French and 218 for Italian, and it improves both raw accuracy and score calibration in every case measured. A 2.57% equal error rate on that data set, with 5.38% false rejection at 1.0% false acceptance and 7.37% at 0.5%.

Alongside this domain-matched evaluation, releases are regression-tested against a broader internal suite of nineteen licensed corpora spanning telephone, microphone, smartphone and broadcast audio in many languages, with net speech durations from about one second to over seventy seconds. That suite is deliberately harder than production and serves as a gate on engine releases.

### Risk and safety evaluations

Decisioning bias is rigorously assessed and evaluated to measure bias across a highly diversified population. Based on the methodology and results described in detail below, we can conclude that no material bias is observed.

Using the Fairness Discrepancy Rate (FaDR), which measures the weighted absolute difference in false acceptance and false rejection rates between a reference demographic group and each other group, on a scale where 1.0 indicates identical error rates. Fairness is always measured at an operating point rather than by comparing whole score distributions, because two groups can show similar overall distributions while diverging exactly in the tail where the decision threshold sits. The protocol sets one global threshold on the majority population, English-speaking and, where relevant, male speakers, then measures the error rates the other groups actually experience at that same threshold. A weighting factor w places the two error types in proportionate balance: false acceptance differences are typically fractions of a percent while false rejection differences can exceed ten points, so without weighting the false rejection term would mask the security-relevant one. Speaker recognition and fraudster detection use w = 0.8; anti-spoofing uses w = 1.0 because a shared spoof set makes miss detection statistics identical across groups by construction.

FaDR values must not be read with common-sense percentage intuition. A system can score 0.9 while performing near-perfectly for one group and very poorly for another, because the metric scales with absolute error differences rather than with relative harm. Acceptance thresholds were therefore derived from the error ranges that count as good production performance for the majority group, giving 0.984 for speaker verification, 0.97 for anti-spoofing, and 0.95 for known fraudster detection.

## Safety components and mitigations

**Biometric authentication and fraud detection considerations:**

- **Audio quality gates:** The application can indicate when audio is too noisy or too soft for reliable processing. Customers should use these outputs to avoid relying on low-quality comparisons and should provide retry or alternate-authentication paths.

- **Customer-configurable thresholds:** Biometric authentication, fraud detection, synthetic-speech detection, and playback detection thresholds are independently configurable. Customers should test settings using representative data and document the rationale for chosen operating points. Changes should be evaluated before broad deployment.

- **Correction and removal process:** Customers should maintain a process to investigate disputed matches and remove or correct a voiceprint enrolled in error. A meaningful correction process reduces the risk that an inaccurate or outdated entry leads to repeated adverse treatment.

**Biometric authentication considerations:**

- **Consent and privacy controls:** Biometric authentication requires collection of caller consent as part of the enrollment flow, but customers remain responsible for ensuring that notice and consent are legally sufficient for their jurisdictions and scenarios. Voiceprints, recordings, and associated metadata are stored in the customer's Dataverse environment, where customers should apply appropriate access, retention, and deletion controls.

- **AI generated voices:** Synthetic-speech and playback-detection models provide additional signals for identifying attempts to impersonate a caller. These signals should be considered with other call context and authentication evidence rather than treated as conclusive on their own.

**Fraud detection considerations (only applies to Dynamics 365 Contact Center):**

- **Human review of fraud alerts:** A fraud-watchlist match is treated as a reviewable alert rather than a final decision. A trained fraud analyst should verify relevant evidence before blocking a transaction, restricting access, or taking another adverse action. This is a primary mitigation for false matches and residual performance disparities.

## Best practices for deploying and adopting biometric authentication and fraud detection

Responsible AI is a shared commitment between Microsoft and its customers. While Microsoft builds AI applications and platform services with safety, fairness, and transparency at the core, customers play a critical role in deploying and using these technologies responsibly within their own contexts.

- **Exercise caution and evaluate outcomes in consequential contexts:** Voice authentication, playback detection, synthetic speech detection and fraud detection outputs are probabilistic in nature and some incorrect decisions are inevitable. Outputs should not be the sole basis for an action that could significantly affect an individual. Make sure impacted callers can understand the process, contest an outcome, and correct relevant data.

- You may not use the output of the Fraud detection functionality, including any match or no-match results, to evaluate, determine, or inform a caller's eligibility for credit, employment, insurance, housing, or any other purpose governed by the Fair Credit Reporting Act (FCRA) or similar laws.

- **Exercise human oversight:** Review authentication and fraud signals together with other available evidence. Potential fraud matches should be verified by a trained analyst before adverse action, and callers should have a clear escalation path when results conflict with other information.

- **Avoid overreliance:** A high or low score is not a definitive statement about identity or fraudulent intent. Audio quality, threshold settings, enrollment errors, and model limitations can affect results. Use an alternative authentication method when the result is uncertain or disputed.

- **Support correction and appeal:** Provide a practical way for an affected caller to challenge an incorrect match or enrollment. Investigate disputes promptly and correct or remove inaccurate voiceprints so the error does not persist across future calls.

- **Validate with representative deployment data:** Test the complete experience using actual telephony channels, expected languages and accents, environmental conditions, call durations, and representative user groups. Evaluate false acceptance, rejection rates, quality failures, synthetic speech, playback and fraud detection performance, and demographic disparities at the thresholds intended for production.

- **Configure thresholds deliberately:** Choose thresholds based on the security and convenience requirements of the specific scenario. Document the operating point, approval, and expected trade-offs. Re-test when call routing, audio capture, enrollment procedures, supported populations, or models materially change.

- **Govern enrollment and watchlists:** Restrict who can create, approve, change, or delete voiceprints and watchlist entries. Establish evidence standards, periodic review, retention schedules, and independent correction procedures. Log material changes so that you can investigate disputed outcomes.

- **Use layered authentication:** Do not rely solely on voice authentication for higher-risk transactions or when audio quality is poor. Combine voice signals with additional methods such as one-time passcodes, knowledge-based checks, account context, or trained-agent review, proportionate to the risk.

- **Monitor after deployment:** Track false acceptance and rejection, quality-gate failures, suspected synthetic speech, analyst overrides, disputes, corrected enrollments, and relevant outcomes across user groups. Establish thresholds for escalation and reassess configuration when monitoring indicates drift or disparate impact.

- **Customer responsibility for watchlists and decisions:** Customers are solely responsible for fraud-risk determinations, fraudster designations, and the watchlists used with the application. Customers should document governance, correction, review, retention, and deletion procedures.

- **Protect biometric data:** Apply least-privilege access, encryption, retention, deletion, audit logging, and incident-response controls to voice profiles, recordings, and metadata stored in Dataverse. Avoid retaining biometric data longer than needed for the documented purpose and applicable legal requirements.

## Learn more about biometric authentication and fraud detection

For additional guidance or to learn more about the responsible use of biometric authentication and fraud detection, review the following documentation:

- [Responsible AI for Dynamics 365 Customer Service](/dynamics365/customer-service/implement/responsible-ai-overview?context=/dynamics365/contact-center/context/administer-context)
- [Responsible AI FAQs](/microsoft-copilot-studio/responsible-ai-overview)
- [Microsoft Responsible AI principles](https://www.microsoft.com/ai/responsible-ai)
- [Microsoft responsible AI resources](https://www.microsoft.com/ai/responsible-ai-resources)
- [Microsoft Enterprise AI Services Code of Conduct](/legal/ai-code-of-conduct)
- [Biometric authentication and fraud detection overview](../administer/biometric-authentication-fraud-detection-overview.md)
- [Biometric authentication overview](/contact-center-intelligence/administer/biometric-authentication-overview)
- [Dataverse long term data retention overview](/power-apps/maker/data-platform/data-retention-overview)
- [Privacy and personal data in Microsoft Dynamics 365](/dynamics365/get-started/privacy/)
- [Secure your Dynamics 365 data and apps](/dynamics365/guidance/implementation-guide/security)
