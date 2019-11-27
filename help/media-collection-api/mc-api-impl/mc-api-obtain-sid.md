---
title: セッション ID の取得
description: null
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

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

