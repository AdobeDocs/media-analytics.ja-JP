---
title: プレイヤー状態の追跡の例
description: このトピックには、プレイヤー状態追跡機能の例が含まれています。
translation-type: tm+mt
source-git-commit: 1c2992d2a5992b07fa24823501d542c1878aa296
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# プレイヤー状態の追跡の例


## 長い一時停止の例

ビデオセッションの一時停止時間が30分を超える場合、APIでは新しいセッションが必要です。 この場合、クライアントは新しいセッションIDを生成する必要があります。 両方のビデオセッションの場合、クライアントは、プレイヤーの状態をすべて保持し、呼び出しの直後にすべての情報を `stateStart` イベントとして送信する必要があり `sessionStart` ます。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

が送信さ `sessionEnd` れたら、新しいビデオセッションを開始する必要があり、最初のAPIイベントは次のようになります。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

長い一時停止の例は、プレイヤーがその状態も保存しているので、新しいビデオセッションに送信できることを示しています。
