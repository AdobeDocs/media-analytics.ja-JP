---
title: コンテンツ再生のトラック
description: メディアの読み込み、メディアの開始、メディアの一時停止、メディアの完了など、コア再生のトラッキングについて説明します。
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/cHrkCe0mQm8GlHwLVgf4cjF0VM8B1r3CRt39I2LB6kk
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 803
ht-degree: 2%

---


# コンテンツ再生の追跡

コア再生トラッキングでは、メディアの読み込み、開始、一時停止、再開、完了、セッション終了をカバーしています。 必須ではありませんが、バッファリングとシークのトラッキングも、再生の実装を完了させるための中核となる要素です。

## プレーヤーイベント

| プレイヤーイベント | アクション |
| --- | --- |
| メディア負荷 | メディアオブジェクトを作成、SessionStartを呼び出し |
| メディアの開始 | コールプレイ |
| 一時停止 | PauseStartを呼び出す |
| 一時停止から再開 | コールプレイ |
| Media complete | SessionCompleteの呼び出し |
| メディアの中止/アンロード | SessionEndの呼び出し |
| バッファリング開始 | BufferStartを呼び出す |
| バッファリング終了 | コールプレイ （再開） |
| シーク開始 | SeekStartを呼び出す |
| シーク終了 | SeekCompleteを呼び出してから、Playを呼び出します |

## 実装手順

1. **ユーザーが再生をトリガーするタイミングを特定** （ユーザーが「再生」または「自動再生」をクリックしたタイミング）。 コンテンツ名、ID、長さ、ストリームタイプ、メディアタイプを使用して、メディアオブジェクトを作成します。 フィールド定義については、[&#x200B; コンテンツ名](/help/implementation/variables/core/content-name.md)、[&#x200B; コンテンツ ID](/help/implementation/variables/core/content-id.md)、[&#x200B; コンテンツの長さ](/help/implementation/variables/core/content-length.md)、[&#x200B; ストリームタイプ &#x200B;](/help/implementation/variables/core/stream-type.md)および[&#x200B; コンテンツタイプ &#x200B;](/help/implementation/variables/core/content-type.md)を参照してください。
1. **オプションでメタデータを添付** – 標準メタデータ（番組、季節、エピソードなど） データバリエーションを定義することができます。 標準メタデータキーの参照については、[Show](/help/implementation/variables/standard-metadata/show.md)、[Season](/help/implementation/variables/standard-metadata/season.md)、[Episode](/help/implementation/variables/standard-metadata/episode.md)、[Genre](/help/implementation/variables/standard-metadata/genre.md)、および[Network](/help/implementation/variables/standard-metadata/network.md)を参照してください。
1. **セッションのトラッキングを開始するには、[&#x200B; セッション開始](/help/implementation/events/session/session-start.md)**&#x200B;に電話してください。 これにより、データとメタデータが読み込まれ、開始までの時間のQoS測定が開始されます。 SessionStartは、最初のフレームではなく、再生する&#x200B;*インテント*&#x200B;を追跡します。
1. **コンテンツの最初のフレームが画面に表示されたら、[Play](/help/implementation/events/playback/play.md)**&#x200B;を呼び出します。
1. **プレーヤーが一時停止したときに[一時停止の開始](/help/implementation/events/playback/pause-start.md)**&#x200B;を呼び出します。 再生が再開されたときに、再度再生を呼び出します。 別の再開イベントはありません。
1. 視聴者がコンテンツの終わりに達したら、**呼び出し[&#x200B; セッション完了](/help/implementation/events/session/session-complete.md)**。
1. **プレーヤーがアンロードされるか、ビューアが終了せずにコンテンツを放棄すると、[&#x200B; セッション終了](/help/implementation/events/session/session-end.md)**&#x200B;に電話します。 SessionEndはすぐにセッションを閉じます。それ以降のイベントは追跡できません。

>[!IMPORTANT]
>
>`SessionEnd` は、トラッキングセッションの終わりをマークします。 セッションが完了するまで正常に監視された場合は、`SessionEnd`の前に`SessionComplete`に電話してください。 新しいセッションの`SessionStart`を除き、`SessionEnd`の後に他のトラッキング呼び出しは無視されます。

## コア再生

次の例は、セッションの開始からコンテンツの完了、セッションの終了に至るまで、セッションフロー全体を示しています。

プラットフォーム別の実装の詳細については、[&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、[再生](/help/implementation/events/playback/play.md)、[開始を一時停止](/help/implementation/events/playback/pause-start.md)、[&#x200B; セッション完了](/help/implementation/events/session/session-complete.md)、および[&#x200B; セッション終了](/help/implementation/events/session/session-end.md)を参照してください。

## バッファリング

バッファー開始は、プレイヤーがデータを待っていることを示すシグナルです。 BufferStart （XDM ベースのAPI）の後にPlay イベントを送信すると、バッファーエンドが推測されます。 Mobile SDKでは、BufferCompleteも明示的に呼び出します。

実装の詳細については、[&#x200B; バッファー開始](/help/implementation/events/playback/buffer-start.md)を参照してください。

## シーク

視聴者がスクラブしていることを開始シグナルを求めます。 シーク終了の後に再生が続き、コンテンツの再生が再開されます。

実装の詳細については、[開始を一時停止](/help/implementation/events/playback/pause-start.md) （シーク開始）および[再生](/help/implementation/events/playback/play.md) （シーク終了）を参照してください。

## アプリの割り込みの処理

メディアアプリケーションの再生は、ユーザーが一時停止を押したり、アプリがバックグラウンドに移動したり、電話が到着したりするなど、さまざまな方法で中断する可能性があります。 原因に関係なく、トラッキング手順は同じです。

1. アプリケーションが中断された場合（バックグラウンドに移動、メディアの一時停止など）、**PauseStart**&#x200B;を呼び出します。
1. アプリケーションがフォアグラウンドに戻ったり、メディアの再生が再開されたりしたら、**Play**&#x200B;に電話してください。

>[!NOTE]
>
>アプリがバックグラウンドから戻ったときにSessionStartを呼び出さないでください。 SessionStartを呼び出すと、その時点までの再生が合計再生時間にカウントされなくなり、以前の進行状況マーカー、セグメント、章の境界が失われます。

**一時停止したセッションはいつ終了しますか？** アプリケーションがバックグラウンド再生を許可しない場合は、PauseStartをすぐに呼び出し、バックグラウンドで約1分後にSessionEndを呼び出します。 アプリケーションはバックグラウンドから一時停止pingを送信し続けることはできず、セッションを無期限に開いたままにすると、エクスペリエンスが低下します。 アプリケーションがバックグラウンド再生（オーディオアプリ、ビデオポッドキャストアプリ）をサポートしている場合は、バックグラウンドでのpingの送信を続行します。

**長いバックグラウンド期間の後に再起動：** セッションの有効期限が切れるほどアプリがバックグラウンド化された場合（非アクティブな状態が30分）、SessionEndを呼び出して残っているセッションを完全に終了し、視聴者が戻ってきたときにSessionStartを呼び出して新しいセッションを開始します。

## 非アクティブなセッションの再開

10分間イベントを受信しなかった場合、または30分間プレイヘッドの移動がない場合、セッションは自動的に期限切れになります。 セッションの有効期限が切れた後にユーザーが戻った場合は、SessionStartをもう一度呼び出して新しいセッションを開きます。

**デバイス間で再開（クロスデバイスのハンドオフ）:**&#x200B;視聴者がデバイス間で再生を転送する場合（例えば、電話からテレビにキャストする場合）、再開フラグを使用して、Analytics レポートでセッションを結合します。

1. **ソースデバイス**&#x200B;で、ビューアがキャストを開始したときにSessionEndを呼び出します。 SessionCompleteを呼び出さないでください。コンテンツは完了しません。
1. **宛先デバイス**&#x200B;で、再開フラグを`true`に設定してSessionStartを呼び出し、ソースデバイスから同じコンテンツメタデータと再生ヘッドの位置を渡します。

再開フラグを設定すると、Analyticsは、ハンドオフの2番目のレグに対して[&#x200B; メディア開始](/help/reporting/metrics/media-starts.md)ではなく[&#x200B; コンテンツ再開](/help/reporting/metrics/content-resumes.md)を増分します。

**以前に閉じられたセッションを手動で再開する：** アプリケーションがユーザーデータを保存し、以前に閉じられたセッションを再開できる場合は、セッション開始時に再開フラグを設定します。 すべてのプラットフォームの実装の詳細については、[&#x200B; セッション開始](/help/implementation/events/session/session-start.md#resuming-a-session)を参照してください。
