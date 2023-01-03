---
title: プレーヤーステートトラッキングの例
description: このトピックでは、プレーヤーステートトラッキング機能の例を示します。
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '119'
ht-degree: 100%

---

# プレーヤーステートトラッキングの例


## 長い一時停止の例

ビデオセッションの一時停止時間が 30 分を超える場合、API では新しいセッションが必要となります。この場合、クライアントは新しいセッション ID を生成する必要があります。両方のビデオセッションで、クライアントは、プレーヤーの状態をすべて保持し、`sessionStart` 呼び出しの直後にすべての情報を `stateStart` イベントとして送信する必要があります。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

`sessionEnd` が送信されたら、新しいビデオセッションを開始する必要があります。最初の API イベントは次のようになります。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

長い一時停止の例では、プレーヤーが状態も保存しているので、新しいビデオセッションに送信できることを示しています。
