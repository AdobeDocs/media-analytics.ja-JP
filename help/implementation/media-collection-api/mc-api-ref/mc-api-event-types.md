---
title: ストリーミングメディアのイベントタイプと説明
description: メディアコレクションのイベントタイプと説明"
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 06f24e828fb7795d55599ea1fa7913182dd357e6
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 88%

---

# イベントタイプと説明{#event-types-and-descriptions}

## sessionStart

`sessions` 呼び出しと共に送信されます。応答が返されたら、Location ヘッダーからセッション ID を抽出し、それをコレクションサーバーに対する後続のイベント呼び出しに使用します。

## play

プレーヤーが他の状態から「再生中」に移行したとき（つまり、`on('Playing')` コールバックがプレーヤーによってトリガーされたとき）に送信されます。プレーヤーが「再生中」に移行する前の他の状態には、「バッファリング」のほか、ユーザーが「一時停止」から復帰したとき、プレーヤーがエラーから回復したとき、自動再生などがあります。

## ping

* **メインコンテンツ** - 他にどのような API イベントが送信されているかに関係なく、メインコンテンツの再生中に 10 秒ごとに送信する必要があります。最初の ping イベントは、メインコンテンツの再生が開始されたときから 10 秒後に発生する必要があります。
* **広告コンテンツ** - 広告トラッキング中、1 秒ごとに送信する必要があります。

ping イベントの場合、リクエスト本文に *マップが含まれていては*&#x200B;いけません`params`。

## bitrateChange

ビットレートが変更されたときに送信されます。

## bufferStart

バッファリングの開始時に送信されます。`bufferResume` イベントタイプはありません。`bufferStart` の後に `play` イベントを送信すると、`bufferResume` と解釈されます。

## pauseStart

ユーザーが一時停止を押したときに送信されます。`resume` イベントタイプはありません。`pauseStart` の後に `play` イベントを送信すると、`resume` と解釈されます。

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

`sessionEnd` ールが送信されない場合、破棄されたセッションは [ 通常タイムアウト ](../mc-api-impl/mc-api-timeout.md) になります（イベントの受信が 10 分間行われない後、または再生ヘッドの移動が 30 分間行われない後）。 さらに、そのセッション ID を使用して行われた後続のすべてのメディアコールはドロップされます。

## sessionComplete

メインコンテンツの最後に達したときに送信されます。

>[!IMPORTANT]
>
>各イベントタイプについて [JSON 検証スキーマ](mc-api-json-validation.md)を参照して、正しいイベントパラメーターのタイプと要件を確認してください。
