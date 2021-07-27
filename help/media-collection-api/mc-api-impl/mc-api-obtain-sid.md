---
title: セッション ID の取得
description: Sessions リクエストをコーディングしてレスポンスの Location ヘッダーからセッション ID を取得する方法を説明します。
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '63'
ht-degree: 100%

---

# セッション ID の取得 {#obtaining-a-session-id}

このリファレンスプレーヤーのコードスニペットは、[Sessions リクエスト](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)をコーディングする 1 つの方法と、セッション ID（およびメディアコレクション API バージョン）を応答の Location ヘッダーから抽出する方法を示しています。

```js
var  
sessionData = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
...

const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    ...
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data": sessionData             // Mandatory params 
     }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    ...
```
