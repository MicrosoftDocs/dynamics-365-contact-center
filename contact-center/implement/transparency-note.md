---
title: Transparency note for constrained speech recognition 
description: This transparency note discusses constrained speech recognition and the key considerations for making use of this technology responsibly.
author: neeranelli
ms.author: sambobo
ms.reviewer: nenellim
ms.date: 08/25/2025
ms.topic: concept-article
ms.custom: bap-template
---

# Transparency note: Constrained speech recognition

## What is a Transparency Note?

An AI system includes not only the technology, but also the people who will use it, the people who will be affected by it, and the environment in which it is deployed. Creating a system that is fit for its intended purpose requires an understanding of how the technology works, what its capabilities and limitations are, and how to achieve the best performance. Microsoft’s Transparency Notes are intended to help you understand how our AI technology works, the choices system owners can make that influence system performance and behavior, and the importance of thinking about the whole system, including the technology, the people, and the environment. You can use Transparency Notes when developing or deploying your own system, or share them with the people who will use or be affected by your system.

Microsoft’s Transparency Notes are part of a broader effort at Microsoft to put our AI Principles into practice. Learn more in [Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai).

## The basics of constrained speech recognition

### Introduction

Speech Recognition is a vital function for engaging with voice-enabled AI systems. These systems (frequently known as “speech-to-text” engines) converts a user’s spoken words into text, often producing a confidence score indicative of the probability of correctness of the output. Constrained Speech Recognition is a specific modality that specifically limits the set of possible words or phrases to recognize by the engine itself. This constraint is done through a Grammar. Grammars are, by definition, the rules-based list of expected words or phrases for the engine to recognize.

Constrained speech recognition engines are especially useful for:

- Recognizing alphanumeric inputs such as account numbers and tracking numbers.

- Domain specific large lists (stocks, addresses, names).
- Small scoped applications that are designed for interactions with a small set of words and phrases to recognize.
- Directed dialog to assist in navigating a menu tree of items, either used for the first interaction of a caller, or as the basis of the system’s conversational design.

### Key terms

| Term                                            | Definition         |
|-------------------------------------------------|--------------------|
| Grammar                                         | A *grammar* is a description of the words and phrases that a speech recognizer will understand and interpret. Grammars are loaded by the recognizer at runtime to convert the user’s spoken responses and commands into information the voice application can use |
| GrXML                                           | The format in which grammars are composed                                |
| Speech Recognition Grammar Specification (SRGS) | The W3C standard for defining Grammars   |
| Utterance                                       | The spoken words or phrases from a user to an Voice AI system that are interpreted by the speech recognition system |

## Capabilities

### System behavior

Each time the recognizer interprets a user utterance, it compiles a list of the closest possible matches to return to the voice application. This list is called the *n-best list*, since it is made up of a prespecified number *n* of interpretations that best match what the user seems to have said. When the user speaks, the recognizer searches for the best matches among the items defined in the grammar(s), and adds each matching interpretation to the candidates being considered for the n-best list. During this search the recognizer uses acoustic models to
analyze the audio input, lexical models to determine the most probable sentences in the grammars, and semantic models to determine the most probable meanings of what the caller has said. The recognizer searches until it has found the highest possible interpretations, or until the remaining items could not possibly match what was heard.

The recognizer assigns a confidence score to each item in the candidate list, and ranks them from highest confidence to lowest. The recognizer re-assesses and fine-tunes these scores as new interpretations are found. If the grammars allow homonyms (words that sound identical but have different meanings), and one is spoken, the recognizer assigns the homonyms to separate interpretations with identical confidence scores. The recognizer refines the candidate list by processing any constraint lists and/or semantic interpretation scripts (ECMAScript) specified in the grammars. The recognizer removes any interpretations that do not meet the target confidence levels configured for the recognition. The recognizer returns the final top n results to the application. This n-best list contains the matched text (for the entire utterance, and for individual slots), confidence scores, and any keys and values set for the utterances.

## Use cases

### Intended uses

Constrained Speech Recognition can be used in multiple scenarios. The system’s intended uses include:

- **Recognize spoken words:** To translate speech into text constrained by the definitive list provided to the system (via a “Grammar”) such as alphanumeric (license plates, social security numbers, etc) inputs or list-based results (corporate directory, stock tickers, addresses)

- **Validate Input:** To validate that what was spoken is intended to be accepted by the system. For example, validating that a credit card number is a valid one (mathematically).

- **Remove Output Candidates:** Remove words or phrases from recognition on repeat recognition attempts

### Considerations when choosing other use cases

We encourage customers to leverage Constrained Speech Recognition in their innovative solutions or applications. However, here are some considerations when choosing a use case:

- **Disclosure:** Consistent with any AI-agent creation, always disclose to a caller that the system they are interacting with is AI powered

### Unsupported uses

- **Batch Transcription:** Completely transcribing a persons spoken words into complete textual transcription

- **Intent Interpretation:** Mapping the persons spoken words into an interpreted intent, as opposed to a transcription

**Legal and regulatory considerations.** Organizations need to evaluate potential specific legal and regulatory obligations when using any AI services and solutions, which may not be appropriate for use in every industry or scenario. Restrictions may vary based on regional or local regulatory requirements. Additionally, AI services or solutions are not designed for and may not be used in ways prohibited in applicable terms of service and relevant codes of conduct.

## Limitations

As stated previously, Constrained Speech Recognition performs exceptionally well against specific use cases such as alphanumeric and list-based recognition tasks where the information is explicit, precise, and limited from the user. By contrast, traditional speech-to-text systems that use semantic based or natural language understanding models are best for recognizing a wide-range of spoken topics, interpreting at or around the model. Explicitly put, any speech input that is outside the definition of the grammar will result in no recognition, thus, its
encouraged for developers building voice-based applications to consider where its appropriate to use constrained speech versus alternative methods.

### Technical limitations, operational factors, and ranges

For Constrained Speech Recognition specifically to work accurately, a well-designed grammar must be able to accept many different user responses, and interpret them quickly, accurately, and efficiently. This means that a developer must be able to predict what sort of responses each application prompt will produce, and encode them in a grammar as efficiently as possible. This in turn means that grammars must be designed very much in parallel with the voice application.

A good grammar balances these goals:

- **Thorough coverage:** The grammar accepts and interprets any reasonable response from users to prior application prompt.

- **Accuracy**: The grammar correctly recognizes responses so users are not asked to repeat, and grammars do not pass incorrect values to the  main application.

- **Speed**: The grammar quickly recognizes responses without delays that frustrate users.

- **Resource use:** The grammar processes efficiently.

Grammar writing is an iterative process. You create an initial grammar based on what you expect callers to say, collect some real data, refine the grammar, gather some more data, refine the grammar again, and so on. As you refine the grammar by adding and removing phrases, it more closely approximates the way callers speak to the application. In practice, no grammar can include all of the responses that can occur in your application, because you cannot control how people speak.

The process of developing a set of grammars generally involves the
following steps:

1. **Identify the information items and define the slots**. What information must the user supply to the application, and is there a particular order in which it must be supplied?

1. **Design the dialog.** Determine the most efficient dialog flow between the user and application.

1. **Design the prompts.** Create prompts that will elicit the desired information.

1. **Anticipate the caller responses to the prompts.** Consider the spoken words that the grammar will have to recognize.

1. **Identify the core and filler portions of your grammars.** Identify the key words to look for in the responses.

1. **Plan your grammar strategy.** Determine the best way to meet the requirements for each grammar, and choose a suitable approach or combination of approaches to address them.

1. **Adjust and refine the grammars.** Solve any problems and optimize the grammar performance,

## System performance

The Constrained Speech Recognition engine is highly performant compared to alternative modalities of speech recognition, using limited memory when processing requests. Factors within the developers control have more of an impact on the performance than the system itself. The foremost objective for grammar development is to design for optimal recognition accuracy. The next goal is to write for clarity, maintainability, and extensibility. The third goal is to create efficient recognition contexts.

## Best practices for improving system performance

Below are grammar characteristics that affect resource usage:

- **Coverage**: The grammar covers (includes) the phrases you expect the caller to use. Under-coverage leads to an increase in out-of-vocabulary utterances, confirmations, and retries, which all increase CPU usage, call duration, and lower caller satisfaction.

- **Over-generation**: It is important that the grammar not over-generate by allowing nonsensical phrases, as this reduces accuracy. For example, a grammar that recognizes a city and state
  needs to constrain utterances to valid combinations of cities and states.

- **Multiple parses**: Ideally, each possible sentence in the grammar has a unique parse. Occasionally, a grammar may allow *multiple parses* of a single sentence. Usually, multiple parses indicate an oversight in the design of the grammar that needs correction.

- **Keys passed to the application**: You must ensure that key/value pairs are set correctly.

When a caller says a word or phrase that cannot be parsed by the grammar, the word or phrase is said to be out-of-grammar. As a rule of thumb, a 5% out-of-grammar rate is considered acceptable. Occasionally, even 10-20% out-of-grammar rates are not uncommon for certain types of recognition tasks. Consider using alternative forms of speech recognition at this latter rate.

*Latency* is defined as the period of elapsed time from after the caller stops speaking (including the configured end-of-speech timeout) until a recognition result is returned to the application. When latency is too high, the user experience degrades; the system appears sluggish, which can be frustrating to the user and leads to further user interface complications.

In extreme circumstances, excess latency causes unsuccessful application transactions if user stops speaking without accomplishing the goal of their conversation. Poor recognition response times can have many contributing factors:

- Use of very large grammars containing hundreds of thousands of items.

- Extremely long average utterance lengths.

- High amounts of ECMAScript processing within the grammar.

- Network delays when fetching grammars.

Make sure to properly test grammars prior to deploying them within a live running system such as running test scenarios with various phrases to be spoken.

## Evaluation of constrained speech recognition

### Evaluation methods

Some commonly used metrics for evaluating constrained speech recognition include:

- **Word Error Rate (WER)**: This measures the percentage of words that are incorrectly recognized. It is calculated as the sum of substitutions, deletions, and insertions divided by the total number of words in the reference.

- **N-Best List Accuracy**: This evaluates the accuracy of the top N hypotheses generated by the recognizer. It is useful for understanding how often the correct interpretation is among the top suggestions.

- **Coverage**: This metric assesses whether the grammar includes all the necessary phrases and variations that users might say. A grammar with good coverage ensures that the system can handle a wide range of inputs.

- **Latency**: This measures the time it takes for the system to process the spoken input and produce a recognition result. Lower latency is crucial for real-time applications.

- **False Accept/Reject Rate**: this measures false positives and negatives the system experiences. This directly affects caller containment and application success rates for contact center scenarios.

## Fairness considerations

At Microsoft, we strive to empower every person on the planet to do more. An essential part of this goal is working to create technologies and products that are fair and inclusive. Fairness is a multi-dimensional, socio-technical topic and impacts many different aspects of our product development. You can learn more about Microsoft’s approach to fairness here.

One important dimension to consider when using AI systems, including constrained speech recognition, is how well the system performs for different groups of people. Research has shown that without conscious effort focused on improving performance for all groups, AI systems can exhibit varying levels of performance across different demographic factors such as race, ethnicity, gender, and age.

In some cases, there may be remaining performance disparities. It is important to note that these disparities may exceed the target, and we are actively working to address and minimize any potential biases or performance gaps, carefully consider the demographic group choice of the actor, and seek diverse perspectives from a variety of backgrounds.

Regarding representational harms, such as stereotyping, demeaning, or erasing outputs, we acknowledge the risks associated with these issues. While our evaluation process aims to mitigate such risks, we encourage users to consider their specific use cases carefully and implement additional mitigations as appropriate. Having a human in the loop can provide an extra layer of oversight to address any potential biases or unintended consequences.

We are committed to continuously improving our fairness evaluations to gain a deeper understanding of the system's performance across various demographic groups and potential fairness concerns. The evaluation process is ongoing, and we are actively working to enhance fairness and inclusivity, and mitigate any identified disparities. We understand the importance of addressing fairness considerations and strive to ensure that constrained speech recognition delivers reliable and equitable speech recognition outputs.

Please note that this information represents what we know so far about fairness evaluations, and we remain dedicated to refining our evaluation methodologies and addressing any fairness concerns that may arise.

## Learn more about responsible AI

[Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai)  
[Microsoft responsible AI resources](https://www.microsoft.com/ai/responsible-ai-resources)  
[Microsoft Azure Learning courses on responsible AI](/learn/paths/responsible-ai-business-principles/)  

## Learn more about constrained speech recognition

[Use external speech grammars](/microsoft-copilot-studio/voice-external-grammars)  