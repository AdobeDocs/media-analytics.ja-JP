---
title: プレーヤーでの HTTP リクエストタイプの設定
description: 'すべてのストリーミングメディアコレクションAPIリクエストのリクエスト本文は、JSON形式である必要があります。 プレーヤーでコンテンツリクエストタイプを設定する方法を説明します。 '
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 66%

---

# HTTP リクエストタイプの設定 {#setting-the-http-request-type}

すべてのメディアコレクション API リクエストのリクエスト本文は JSON 形式である必要があるので、プレーヤーでコンテンツリクエストタイプを設定する必要があります。例えば、JavaScript では、`Content-Type` リクエストヘッダーを次のように設定します。

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
