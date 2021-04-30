---
title: プレーヤーでの HTTP リクエストタイプの設定
description: プレーヤーでの HTTP リクエストタイプの設定
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
translation-type: ht
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: ht
source-wordcount: '58'
ht-degree: 100%

---

# HTTP リクエストタイプの設定 {#setting-the-http-request-type}

すべてのメディアコレクション API リクエストのリクエスト本文は JSON 形式である必要があるので、プレーヤーでコンテンツリクエストタイプを設定する必要があります。例えば、JavaScript では、`Content-Type` リクエストヘッダーを次のように設定します。

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
