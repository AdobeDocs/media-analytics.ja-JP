---
title: ストリーミングメディアイベントの概要
description: メディアイベントの種類と送信する順序について説明します。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 4%

---


# ストリーミングメディアイベント

ストリーミングメディアトラッキングは、プレーヤーのステートの遷移を表す一連のイベント呼び出しをAdobe データコレクションエンドポイントに送信することで機能します。 すべてのイベントは、[sessionStart](session/session-start.md)呼び出しで始まり、[sessionComplete](session/session-complete.md)または[sessionEnd](session/session-end.md)で終了するアクティブなセッションに属します。

## イベントワークフロー

次の順序付きリストは、プレロール広告と1つのチャプターを含む一般的なVOD再生に必要なイベントシーケンスを示しています。

1. **[セッション開始](session/session-start.md)**：常に最初のイベント。セッションを作成し、セッション IDを返します
2. **[広告ブレーク開始](ads/ad-break-start.md)**：広告イベントの前に必須
3. **[広告開始](ads/ad-start.md)** → **[広告完了](ads/ad-complete.md)** （または&#x200B;**[広告スキップ](ads/ad-skip.md)**）
4. **[広告ブレーク完了](ads/ad-break-complete.md)**：ブレーク内のすべての広告の後に必要
5. **[再生](playback/play.md)**: コンテンツの再生が開始または再開されたことを示すシグナル
6. **[章の開始](chapters/chapter-start.md)**: オプション。章の先頭をマークします
7. **[Ping](playback/ping.md)**: メインコンテンツ中は10秒ごとに、広告中は1秒ごとに送信
8. **[章完了](chapters/chapter-complete.md)**：任意。章の終わりを示します
9. **[一時停止の開始](playback/pause-start.md)** → **[再生](playback/play.md)** （再開）：一時停止の場合
10. **[バッファー開始](playback/buffer-start.md)** → **[再生](playback/play.md)** （再開）：任意のバッファリングの場合
11. **[セッション完了](session/session-complete.md)**：ビューアがコンテンツの最後に到達したとき

ビューアがコンテンツの最後に到達する前にセッションを放棄した場合は、「[ セッションの終了](session/session-end.md)」を使用します。

## セッションのライフサイクル

次のいずれかの条件を満たした場合、セッションは自動的に期限切れになります。

* **10分**&#x200B;のイベントは受信されません
* **30分**&#x200B;の再生ヘッドの移動がありません

## イベント参照

| イベント | カテゴリ | 関連付けられた指標 |
| --- | --- | --- |
| [ セッション開始](session/session-start.md) | セッション | [ メディア開始](/help/reporting/metrics/media-starts.md) |
| [ セッション完了](session/session-complete.md) | セッション | [ コンテンツ完了](/help/reporting/metrics/content-completes.md) |
| [ セッション終了](session/session-end.md) | セッション | — |
| [ プレイ ](playback/play.md) | 再生 | [ コンテンツ開始](/help/reporting/metrics/content-starts.md) |
| [開始を一時停止](playback/pause-start.md) | 再生 | [ イベントを一時停止](/help/reporting/metrics/pause-events.md) |
| [ バッファー開始](playback/buffer-start.md) | 再生 | [ バッファーイベント ](/help/reporting/metrics/buffer-events.md) |
| [ ビットレート変更](playback/bitrate-change.md) | 再生 | [ ビットレートの変更](/help/reporting/metrics/bitrate-changes.md) |
| [Ping](playback/ping.md) | 再生 | — |
| [休憩の開始](ads/ad-break-start.md) | 広告 | — |
| [広告の開始](ads/ad-start.md) | 広告 | [広告開始](/help/reporting/metrics/ad-starts.md) |
| [Ad complete](ads/ad-complete.md) | 広告 | [広告が完了しました](/help/reporting/metrics/ad-completes.md) |
| [広告をスキップ ](ads/ad-skip.md) | 広告 | — |
| [Ad break complete](ads/ad-break-complete.md) | 広告 | — |
| [章の開始](chapters/chapter-start.md) | 章 | [章開始](/help/reporting/metrics/chapter-starts.md) |
| [章完了](chapters/chapter-complete.md) | 章 | [章完了](/help/reporting/metrics/chapter-completes.md) |
| [章をスキップ ](chapters/chapter-skip.md) | 章 | — |
| [状態の開始](player-state/state-start.md) | プレイヤーの状態 | 州によって異なる |
| [状態の終了](player-state/state-end.md) | プレイヤーの状態 | 州によって異なる |
| [ エラー](error.md) | 画質 | [影響を受けるストリームのエラー](/help/reporting/metrics/error-impacted-streams.md) |

>[!MORELIKETHIS]
>
>* [JSON検証スキーマ ](/help/implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)：各イベントタイプのリクエストペイロード構造を検証します
>* [ イベント要求エンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):Media Collection API エンドポイント参照
>* [ セッション要求エンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md): イベントを送信する前にセッションを作成します
>* [ プレーヤー状態の追跡](/help/use-cases/player-state-tracking/implementation-and-reporting.md)：状態の開始と終了の実装の詳細
