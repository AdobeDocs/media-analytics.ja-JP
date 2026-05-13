---
title: プレーヤーステートトラッキングの例
description: このトピックでは、プレーヤーステートトラッキング機能の例を示します。
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eJ9Pb4tWQy0lRhkNXmexUyflt3qT0105FM--jAsGldQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# プレーヤーステートトラッキングの例


## 長い一時停止の例

ビデオセッションの一時停止時間が 30 分を超える場合、API では新しいセッションが必要となります。 この場合、クライアントは新しいセッション ID を生成する必要があります。 両方のビデオセッションで、クライアントは、プレーヤーの状態をすべて保持し、`sessionStart` 呼び出しの直後にすべての情報を `stateStart` イベントとして送信する必要があります。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

`sessionEnd` が送信されたら、新しいビデオセッションを開始する必要があります。最初の API イベントは次のようになります。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

長い一時停止の例では、プレーヤーが状態も保存しているので、新しいビデオセッションに送信できることを示しています。
