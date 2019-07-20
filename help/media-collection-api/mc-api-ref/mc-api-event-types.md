---
seo-title: イベントタイプと説明
title: イベントタイプと説明
uuid: bc4f75a7- ea22-47eb- a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: 69057b2abf7140d52b1897af3dc9d9fd01ca87ad

---


# イベントタイプと説明{#event-types-and-descriptions}

## sessionStart

`sessions` 呼び出しで送信されます。応答が返されたら、Location ヘッダーからセッション ID を抽出し、それをコレクションサーバーに対する後続のイベント呼び出しに使用します。

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). プレーヤーが「再生中」に移行する前の他の状態には、「バッファリング」のほか、ユーザーが「一時停止」から復帰したとき、プレーヤーがエラーから回復したとき、自動再生などがあります。

## ping

* **メインコンテンツ** - 他にどのような API イベントが送信されているかに関係なく、メインコンテンツの再生中に 10 秒ごとに送信する必要があります。最初の ping イベントは、メインコンテンツの再生が開始されたときから 10 秒後に発生する必要があります。
* **広告コンテンツ** - 広告トラッキング中に 1 秒ごとに送信する必要があります。

ping イベントの場合、リクエスト本文に *マップが含まれていては*&#x200B;いけません`params`。

## bitrateChange

ビット予測の変更時に送信されます。

## bufferStart

バッファリングの開始時に送信されます。`bufferResume` イベントタイプはありません。A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

ユーザーが一時停止を押すと送信されます。`resume` イベントタイプはありません。A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

広告の時間の開始を知らせる

## adStart

広告の開始を通知します

## adComplete

広告の時間の完了を通知します

## adSkip

広告スキップの通知

## adBreakComplete

広告の時間の完了を通知します

## chapterStart

チャプターセグメントの開始を通知します

## chapterSkip

チャプタースキップの通知

## chapterComplete

チャプターの完了を通知します

## error

エラーが発生したことを通知します。

## sessionEnd

これは、ユーザーがコンテンツの表示を破棄したときにセッションを直ちに閉じるようにMedia Analyticsのバックエンドに通知するために使用されるため、返されることはほとんどありません。

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

メインコンテンツの終了時に送信されます

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

