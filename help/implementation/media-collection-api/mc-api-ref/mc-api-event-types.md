---
title: ストリーミングメディアのイベントタイプと説明
description: 'メディア コレクションのイベントの種類と説明を教えてください。 '
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gqlCzqKd3F7N2-7WE727Ygl-4wheVjObgnx-ydLbgZk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 395
ht-degree: 79%

---

# イベントタイプと説明{#event-types-and-descriptions}

## sessionStart

`sessions` 呼び出しと共に送信されます。 応答が返されたら、Location ヘッダーからセッション ID を抽出し、それをコレクションサーバーに対する後続のイベント呼び出しに使用します。

## play

プレーヤーが他の状態から「再生中」に移行したとき（つまり、`on('Playing')` コールバックがプレーヤーによってトリガーされたとき）に送信されます。 プレーヤーが「再生中」に移行する前の他の状態には、「バッファリング」のほか、ユーザーが「一時停止」から復帰したとき、プレーヤーがエラーから回復したとき、自動再生などがあります。

## ping

* **メインコンテンツ** - 他にどのような API イベントが送信されているかに関係なく、メインコンテンツの再生中に 10 秒ごとに送信する必要があります。 最初の ping イベントは、メインコンテンツの再生が開始されたときから 10 秒後に発生する必要があります。
* **広告コンテンツ** - 広告トラッキング中、1 秒ごとに送信する必要があります。

ping イベントの場合、リクエスト本文に *マップが含まれていては*&#x200B;いけません`params`。

## bitrateChange

ビットレートが変更されたときに送信されます。

## bufferStart

バッファリングの開始時に送信されます。 `bufferResume` イベントタイプはありません。 `bufferStart` の後に `play` イベントを送信すると、`bufferResume` と解釈されます。

## pauseStart

ユーザーが一時停止を押したときに送信されます。 `resume` イベントタイプはありません。 `pauseStart` の後に `play` イベントを送信すると、`resume` と解釈されます。

## adBreakStart

広告ブレークの開始を示します。

## adStart

広告の開始を示します。

## adComplete

広告ブレークの完了を示します。

## adSkip

広告スキップを示します。

## adBreakComplete

広告ブレークの完了を示します。

## chapterStart

チャプターセグメントの開始を示します。

## chapterSkip

チャプタースキップを示します。

## chapterComplete

チャプターの完了を示します。

## error

エラーが発生したことを示します。

## sessionEnd

これは、コンテンツの視聴を中断したユーザーが復帰する可能性が低いときに、Media Analytics バックエンドにセッションを即座に閉じるよう通知するために使用されます。

`sessionEnd`が送信されない場合、放棄されたセッションは通常[ タイムアウト ](../mc-api-impl/mc-api-timeout.md)になります（イベントを10分間受信しなかった後、または再生ヘッドの移動が30分間行われない場合）。 さらに、そのセッション IDで行われたその後のすべてのメディア呼び出しは削除されます。

## sessionComplete

メインコンテンツの最後に達したときに送信されます。

>[!IMPORTANT]
>
>各イベントタイプについて [JSON 検証スキーマ](mc-api-json-validation.md)を参照して、正しいイベントパラメーターのタイプと要件を確認してください。

## stateStart

プレイヤーの状態トラッキングの開始を示します。

詳しくは、[実装とレポート ](/help/use-cases/player-state-tracking/implementation-and-reporting.md)を参照してください。

## stateEnd

プレイヤーの状態トラッキングの終了を示します。

詳しくは、[実装とレポート ](/help/use-cases/player-state-tracking/implementation-and-reporting.md)を参照してください。
