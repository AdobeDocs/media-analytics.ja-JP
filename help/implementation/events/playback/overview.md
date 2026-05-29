---
title: 再生をトラック
description: 再生イベントと、再生、一時停止、バッファー、pingおよびビットレート変更のトラッキングを実装する方法について説明します。
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 230
ht-degree: 2%

---


# 再生をトラック

再生イベントは、セッション全体を通してメディアプレーヤーの状態の遷移を追跡します。 イベントストリームの中心を形成し、あらゆるコンテンツタイプに適用されます。

## プレーヤーイベント

| プレイヤーイベント | アクション |
| --- | --- |
| メディアの再生または再開 | コールプレイ |
| メディアの一時停止 | 呼び出し一時停止の開始 |
| バッファリングが開始されます | 呼び出しバッファー開始 |
| バッファリング終了 | コールプレイ |
| ビットレートの変更 | コールビットレートの変更 |
| タイマー火災 | コールピン |

## 実装手順

1. **コンテンツの最初のフレームが画面に表示されるときに、[ セッション開始](../session/session-start.md)の後に[再生](play.md)**&#x200B;を呼び出します。 一時停止またはバッファストール後に再生が再開された場合も、再生を送信します。 別の再開イベントはありません。
1. **ユーザーが再生を一時停止したときに[一時停止の開始](pause-start.md)**&#x200B;を呼び出します。 再生が再開されたときに再生を送信します。
1. **プレーヤーがデータ待ちの状態で停止した場合、[ バッファー開始](buffer-start.md)**&#x200B;を呼び出します。 XDM ベースのAPIでは、次のPlay イベントを送信するとバッファエンドが推測されます。 Mobile SDKでは、バッファリングが解決する場合に`BufferComplete`を明示的に呼び出します。
1. **メインコンテンツの再生中は10秒ごとに[Ping](ping.md)**&#x200B;に電話し、広告再生中は1秒ごとに電話します。 Pingはセッションを維持し、再生ヘッドの動きを記録します。 モバイル SDKはpingを自動的に送信します。他のすべてのプラットフォームは手動で送信する必要があります。
1. **プレーヤーが新しいビットレートを交渉するたびに[ ビットレート変更](bitrate-change.md)**&#x200B;を呼び出します。 現在のQoE データ（ビットレート、フレーム/秒、ドロップされたフレーム）を含めることで、バックエンドは[平均ビットレート ](/help/reporting/metrics/average-bitrate.md)および関連する品質指標を計算できます。
