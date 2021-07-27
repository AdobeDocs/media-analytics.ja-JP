---
title: セッションの応答が遅い場合のイベントのキューへの登録
description: 'プレーヤーでイベントが発生した後にセッション ID が返された場合の対処方法について説明します。 '
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '207'
ht-degree: 100%

---

# セッションの応答が遅い場合のイベントのキューへの登録{#queueing-events-when-sessions-response-is-slow}

メディアコレクション API は RESTful です。つまり、ユーザーは、HTTP リクエストを送信し、その応答を待ちます。これは、ビデオ再生の開始時に [Sessions リクエスト](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を送信してセッション ID を取得する場合にのみ重要です。これが重要なのは、このセッション ID が後続のすべてのトラッキングコールで必要なためです。

プレーヤーでは、（セッション ID パラメーターを含む）_Sessions 応答がバックエンドから返される前に_&#x200B;イベントが発生する可能性があります。これが発生すると、アプリは、[Sessions リクエスト](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)とその応答の間に届いたすべてのトラッキングイベントをキューに入れる必要があります。Sessions 応答が届いたら、キューに入れられた[イベント](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)を最初に処理する必要があります。それから、[Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) 呼び出しを使用して&#x200B;_ライブ_&#x200B;イベントの処理を開始できます。

>[!NOTE]
>
>[Events リクエスト](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)は、HTTP 応答コード以外のデータをクライアントに返しません。

セッション ID を受け取る前にイベントを処理する 1 つの方法については、配信環境のリファレンスプレーヤーを確認してください。次に例を示します。

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

**キューに入れられたイベントを処理する -** リファレンスプレーヤーでは、キューに入れられたイベントが次のように処理されます。

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

続いて、トラッキングイベントを発生と同時に処理します。
