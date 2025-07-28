---
title: Use APIs to pause, resume transcription and recording 
description: Learn how to use APIs to pause and resume transcription and recording in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: reference 
ms.collection: 
ms.date: 11/15/2024
ms.custom: bap-template 
---

# Use APIs to pause, resume transcription and recording 

Dynamics 365 Contact Center provides a set of [APIs](https://github.com/microsoft/dynamics-365-contact-center/tree/main/documentation/CCaaS%20SDK%20APIs) to enable seamless integration of several functionalities into both non-Microsoft CRMs and Dynamics environments.

The [Voice module](https://github.com/microsoft/dynamics-365-contact-center/blob/main/documentation/Embed%20SDK%20APIs/classes/VoiceModule.md) has several methods enable you to control call recording and transcription services during customer interactions. These capabilities are essential when handling sensitive information such as payment details, personally identifiable information, or protected health information that shouldn't be captured in recordings for compliance and security reasons.

## Available methods

- **startRecording**: Initiates voice call recording with automatic transcription.
- **pauseRecording**: Temporarily pauses ongoing recording operations.
- **onRecordingOperationCompleted**: Invokes a callback function with event data when the recording operation is completed.
- **startTranscription**: Begins transcription without full recording.
- **pauseTranscription**: Pauses active transcription services.
- **onTranscriptionOperationCompleted**: Invokes a callback function with event data when the transcription operation is completed.

Learn more about the methods in [available methods in voice module](https://github.com/microsoft/dynamics-365-contact-center/blob/main/documentation/Embed%20SDK%20APIs/classes/VoiceModule.md)

