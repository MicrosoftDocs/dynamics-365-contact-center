---
title: CCaaS_ModifyAgentPresence
description: Modify an agent's presence information at runtime.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: reference 
ms.collection: 
ms.date: 11/15/2024
ms.custom: bap-template 
---

# Pause and Resume Transcription and Recording API 

The pause and resume transcription and recording API enables you to programmatically control call recording and transcription services during customer interactions. This feature is important when handling sensitive information such as payment details, PII (Personally Identifiable Information), or PHI (Protected Health Information) that shouldn't be captured in recordings for compliance and security reasons.

You can use this API to do the following actions:

- **Pause Recording and Transcription**: Suspend both recording and transcription when triggered, so that no sensitive information is captured.
- **Pause Transcription Only**: Suspend transcription when triggered, so that no sensitive information is captured.
- **Resume Recording and Transcription**: Restart both recording and transcription services after handling sensitive information.
- **Integrate through web link**: Embed API functionality into a web link or button that, when selected by customer service representatives automatically pauses recording and transcription, launches a web page for the service representative to do a secure transaction, and resumes recording and transcription when the transaction is completed.


## Sample code 

```
window.top.document.getElementById("myDialog")?.remove();

const voiceOrVideoCalling = window.Microsoft.CCaaS.CCaaSSdk.voiceOrVideoCalling; //Need this

if (window.my_sdk_handlers) {
    window.my_sdk_handlers.forEach(id => {
        window.Microsoft.CCaaS.CCaaSSdk.utility.removeEventHandlerById(id);
    });
}

const getCurrentConversation = async () => {   //Need this full function
    const sessionCtx = await Microsoft.Apm.getFocusedSession().getContext();
    return sessionCtx.parameters.LiveWorkItemId;
}

const createButton = (text, callback) => {
   const btn = window.top.document.createElement("button");
    btn.onclick = callback
    btn.innerText = text; 

    return btn;
}

const createTextDiv = (text) => {
    const myDiv = window.top.document.createElement("div");
    myDiv.innerText = text;
    return myDiv;
}

const myDialog = window.top.document.createElement("div");
myDialog.id = "myDialog";
myDialog.style = "margin: auto; width: 50%; border: 3px solid green; padding: 10px; z-index: 1; background-color: white; position: fixed; left: 600px;top: 300px;";

const buttonsDiv = window.top.document.createElement("div");
const stateDiv = window.top.document.createElement("div");
const eventsDiv = window.top.document.createElement("div");
const errorsDiv = window.top.document.createElement("div");

const displayError = (errorMsg) => {
    errorsDiv.innerHTML = `<b>Last error from action: ${errorMsg}</b>`;
}

const clearError = () =>  errorsDiv.innerHTML = '';

const generateDataElements = (call) => {
    stateDiv.innerHTML = '';

    const lastRefreshDiv = createTextDiv(`Data last updated: ${new Date().toUTCString()}`);
    const lwiIdDiv = createTextDiv(`LiveWorkItemId: ${call.liveWorkItemId}`);
    const callStateDiv = createTextDiv(`Call state: ${call.callState}`);
    const recordingStateDiv = createTextDiv(`Recording state: ${call.recordingState}`);
    const transcriptionStateDiv = createTextDiv(`Transcription state: ${call.transcriptionState}`);

    stateDiv.appendChild(lastRefreshDiv);
    stateDiv.appendChild(lwiIdDiv);
    stateDiv.appendChild(callStateDiv);
    stateDiv.appendChild(recordingStateDiv);
    stateDiv.appendChild(transcriptionStateDiv);
}

const startRecordingBtn = createButton("Start Recording", async () => {  
    try {
        const myConversation = await getCurrentConversation();    //Need this
        await voiceOrVideoCalling.startRecording({ liveWorkItemId: myConversation }); //Need this
        clearError();
    } catch (error) {
        displayError(error?.message);
    }
});

const pauseRecordingBtn = createButton("Pause Recording", async () => {
    try {
        const myConversation = await getCurrentConversation(); //Need this
        await voiceOrVideoCalling.pauseRecording({ liveWorkItemId: myConversation }); //Need this
        clearError();
    } catch (error) {
        displayError(error?.message);
    }
});

const startTranscriptionBtn = createButton("Start Transcription", async () => {
    try {
        const myConversation = await getCurrentConversation();
        await voiceOrVideoCalling.startTranscription({ liveWorkItemId: myConversation });
        clearError();
    } catch (error) {
        displayError(error?.message);
    }
});

const pauseTranscriptionBtn = createButton("Pause Transcription", async () => {
    try {
        const myConversation = await getCurrentConversation();
        await voiceOrVideoCalling.pauseTranscription({ liveWorkItemId: myConversation });
        clearError();
    } catch (error) {
        displayError(error?.message);
    }
});

const refreshDataBtn = createButton("Refresh data", async () => {
    const activeConversationId = await getCurrentConversation();
    
    const calls = await voiceOrVideoCalling.getActiveCalls();
    const call = calls.find(c => c.liveWorkItemId === activeConversationId);
    
    generateDataElements(call);
})

const recordingEventDataDiv = window.top.document.createElement("div");
const recordingHandlerId = voiceOrVideoCalling.onRecordingOperationCompleted((recordingOperationArgs) => {
    recordingEventDataDiv.innerHTML = `Last recording event: <pre>${JSON.stringify(recordingOperationArgs, null, " ")}}</pre>`;
    refreshDataBtn.click();
});

const transcriptionEventDataDiv = window.top.document.createElement("div");
const transcriptionHandlerId = voiceOrVideoCalling.onTranscriptionOperationCompleted((transcriptionOperationArgs) => {
    transcriptionEventDataDiv.innerHTML = `Last transcription event: <pre>${JSON.stringify(transcriptionOperationArgs, null, " ")}}</pre>`;
    refreshDataBtn.click();
});

eventsDiv.appendChild(recordingEventDataDiv);
eventsDiv.appendChild(transcriptionEventDataDiv);

window.my_sdk_handlers = [ recordingHandlerId, transcriptionHandlerId ];

buttonsDiv.appendChild(startRecordingBtn);
buttonsDiv.appendChild(pauseRecordingBtn);
buttonsDiv.appendChild(startTranscriptionBtn);
buttonsDiv.appendChild(pauseTranscriptionBtn);
buttonsDiv.appendChild(refreshDataBtn);

myDialog.appendChild(buttonsDiv);
myDialog.appendChild(stateDiv);
myDialog.appendChild(errorsDiv);
myDialog.appendChild(eventsDiv);

window.top.document.body.appendChild(myDialog);

refreshDataBtn.click();

```