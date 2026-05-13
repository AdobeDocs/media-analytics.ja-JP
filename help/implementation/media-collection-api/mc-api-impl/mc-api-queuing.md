---
title: セッションの応答が遅い場合のイベントのキューへの登録
description: プレーヤーでイベントが発生した後にセッション ID が返された場合の対処方法について説明します。
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/maOCcXZJkPef7edi3UtaSIJKa-4x9byaH6Qzt2eDR2Y
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 205
ht-degree: 80%

---

# セッションの応答が遅い場合のイベントのキューへの登録{#queueing-events-when-sessions-response-is-slow}

メディアコレクション API は RESTful です。つまり、ユーザーは、HTTP リクエストを送信し、その応答を待ちます。 これは、ビデオ再生の開始時に [Sessions リクエスト](../mc-api-ref/mc-api-sessions-req.md)を送信してセッション ID を取得する場合にのみ重要です。 これが重要なのは、このセッション ID が後続のすべてのトラッキングコールで必要なためです。

プレーヤーでは、（セッション ID パラメーターを含む）_Sessions 応答がバックエンドから返される前に_&#x200B;イベントが発生する可能性があります。 これが発生すると、アプリは、[Sessions リクエスト](../mc-api-ref/mc-api-sessions-req.md)とその応答の間に届いたすべてのトラッキングイベントをキューに入れる必要があります。 Sessions 応答が届いたら、キューに入れられた[イベント](../mc-api-ref/mc-api-events-req.md)を最初に処理する必要があります。それから、[Events](../mc-api-ref/mc-api-events-req.md) 呼び出しを使用して&#x200B;_ライブ_&#x200B;イベントの処理を開始できます。

>[!NOTE]
>
>[Events リクエスト](../mc-api-ref/mc-api-events-req.md)は、HTTP 応答コード以外のデータをクライアントに返しません。

セッション IDを受け取る前にイベントを処理する方法を1つ確認してください。 次に例を示します。

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**キューに入ったイベントを処理 –**&#x200B;参照プレーヤーは、キューに入れたイベントを次のように処理します。

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

トラッキングイベントが発生したときに処理を続行します。
