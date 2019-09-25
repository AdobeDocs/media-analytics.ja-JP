---
seo-title: セッションの応答が遅い場合のイベントのキューへの登録
title: セッションの応答が遅い場合のイベントのキューへの登録
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# セッションの応答が遅い場合のイベントのキューへの登録{#queueing-events-when-sessions-response-is-slow}

メディアコレクション API は RESTful です。つまり、ユーザーは、HTTP リクエストを送信し、その応答を待ちます。This is an important point only for when you make a [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) to obtain a Session ID at the beginning of video playback. 以降のすべてのトラッキングコールにセッションIDが必要なので、これは重要です。

It is possible that your player may fire events _before the Sessions response returns_ (with the Session ID parameter) from the backend. If this occurs, your app must queue any tracking events that arrive between the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) and its response. When the Sessions response arrives, you should first process any queued [events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md), then you can start processing _live_ events with the [Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) calls.

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
