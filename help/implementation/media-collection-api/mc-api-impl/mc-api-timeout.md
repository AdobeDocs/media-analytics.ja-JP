---
title: タイムアウト条件
description: Media Collection API タイムアウト条件について説明します。
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/13vwFrp3NF-e-odFn3eXIuhHusl14ovkwhTpPYbJC0U
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 165
ht-degree: 60%

---

# タイムアウト条件{#timeout-conditions}

**メディアコレクション API のタイムアウト条件**

メディアコレクション API はステートレスであり、メディア SDK とは異なり、タイムアウト条件が発生したときに新しいセッション ID を発行するメカニズムを備えていません。 タイムアウト条件が発生すると、バックエンドはセッションを閉じ、そのセッション IDで行われたその後のすべての呼び出しはドロップされます。 セッションタイムアウトを処理するロジックは、クライアントで処理する必要があります。 つまり、タイムアウト条件を監視し、タイムアウトが発生した場合に新しいセッション IDを取得する必要があります。

* **10 分：API イベントなし**

  API イベントを受け取らなかった場合、バックエンドはセッションを閉じます。
* **30 分：再生ヘッドの変更なし**

  再生ヘッドが 30 分間移動しなかった場合（例えば、ユーザーが一時停止を押した後その場所を離れた場合）、バックエンドはセッションを閉じます。

>[!NOTE]
>
>`sessionEnd` イベントタイプの `events` リクエストを送信することで、強制的にセッションを終了することもできます。
