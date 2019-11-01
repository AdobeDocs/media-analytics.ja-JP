---
title: イベントタイプと説明
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# イベントタイプと説明{#event-types-and-descriptions}

## sessionStart

呼び出しと共に送信さ `sessions` れます。 応答が返されたら、Location ヘッダーからセッション ID を抽出し、それをコレクションサーバーに対する後続のイベント呼び出しに使用します。

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). プレーヤーが「再生中」に移行する前の他の状態には、「バッファリング」のほか、ユーザーが「一時停止」から復帰したとき、プレーヤーがエラーから回復したとき、自動再生などがあります。

## ping

* **メインコンテンツ** - 他にどのような API イベントが送信されているかに関係なく、メインコンテンツの再生中に 10 秒ごとに送信する必要があります。最初の ping イベントは、メインコンテンツの再生が開始されたときから 10 秒後に発生する必要があります。
* **広告コンテンツ** - 広告トラッキング中に 1 秒ごとに送信する必要があります。

ping イベントの場合、リクエスト本文に *マップが含まれていては*&#x200B;いけません`params`。

## bitrateChange

ビットレージが変更されたときに送信されます。

## bufferStart

バッファリングが開始したときに送信されます。 `bufferResume` イベントタイプはありません。A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

ユーザーが一時停止を押すと送信されます。 `resume` イベントタイプはありません。A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

広告の時間の開始を通知します。

## adStart

広告の開始を通知します

## adComplete

広告の時間の完了を知らせる

## adSkip

広告のスキップを通知します

## adBreakComplete

広告の時間の完了を知らせる

## chapterStart

チャプターセグメントの開始を通知します。

## chapterSkip

チャプタースキップを通知する

## chapterComplete

チャプターの完了を知らせる

## error

エラーが発生したことを知らせます。

## sessionEnd

これは、ユーザーがコンテンツの表示を中止し、再び訪問する可能性が低い場合に、Media Analyticsバックエンドにセッションを即座に閉じるように通知するために使用されます。

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

メインコンテンツの終わりに達した場合に送信されます

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

