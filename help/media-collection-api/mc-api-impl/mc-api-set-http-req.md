---
title: プレーヤーでの HTTP リクエストタイプの設定
description: 'すべてのストリーミングメディアコレクション API リクエストのリクエスト本文は、JSON 形式にする必要があります。プレーヤーでコンテンツリクエストタイプを設定する方法を説明します。 '
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '78'
ht-degree: 100%

---

# HTTP リクエストタイプの設定 {#setting-the-http-request-type}

すべてのメディアコレクション API リクエストのリクエスト本文は JSON 形式である必要があるので、プレーヤーでコンテンツリクエストタイプを設定する必要があります。例えば、JavaScript では、`Content-Type` リクエストヘッダーを次のように設定します。

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
