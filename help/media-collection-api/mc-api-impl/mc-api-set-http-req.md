---
seo-title: プレーヤーでの HTTP リクエストタイプの設定
title: プレーヤーでの HTTP リクエストタイプの設定
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# HTTPリクエストタイプの設定 {#setting-the-http-request-type}

すべてのメディアコレクション API リクエストのリクエスト本文は JSON 形式である必要があるので、プレーヤーでコンテンツリクエストタイプを設定する必要があります。例えば、JavaScript では、`Content-Type` リクエストヘッダーを次のように設定します。

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

