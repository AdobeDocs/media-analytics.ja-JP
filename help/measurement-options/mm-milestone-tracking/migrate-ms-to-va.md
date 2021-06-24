---
title: マイルストーンからMedia Analyticsに移行する方法を説明します。
description: マイルストーン変数をMedia Analytics指標およびマイルストーンモジュールメソッドに変更する方法を説明します。
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 96%

---

# マイルストーンから Media Analytics への移行 {#migrating-from-milestone-to-media-analytics}

## 概要 {#overview}

マイルストーンと Media Analytics では、ビデオ測定の中核的な概念は同じです。ビデオプレーヤーのイベントを取得して分析メソッドにマッピングする一方で、プレーヤーのメタデータおよび値を取得して分析変数にマッピングします。Media Analytics ソリューションはマイルストーンが発展したものであるので、多くのメソッドや指標は同じです。ただし、設定のアプローチやコードは大幅に変更されています。新しい Media Analytics のメソッドを指すようにプレーヤーのイベントコードを更新できる必要があります。Media Analytics の実装について詳しくは、[SDK の概要](/help/sdk-implement/setup/setup-overview.md)および[追跡の概要](/help/sdk-implement/track-av-playback/track-core-overview.md)を参照してください。

以下の表では、マイルストーンソリューションと Media Analytics ソリューション間の変更について説明します。

## 移行ガイド {#migration-guide}

### 変数リファレンス

| マイルストーンの指標 | 変数の種類 | Media Analytics の指標 |
| --- | --- | --- |
| コンテンツ | eVar<br>デフォルトの有効期限：訪問 | コンテンツ |
| コンテンツタイプ | eVar<br>デフォルトの有効期限：ページビュー | コンテンツタイプ |
| コンテンツ視聴時間 | イベント<br>タイプ：カウンター | コンテンツ視聴時間 |
| ビデオ開始 | イベント<br>タイプ：カウンター | ビデオ開始 |
| ビデオ完了 | イベント<br>タイプ：カウンター | コンテンツ完了 |


### メディアモジュール変数

| マイルストーン | マイルストーンの構文 | Media Analytics | Media Analytics の構文 |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | 該当なし | すべての Media Analytics データはコンテキストデータのみを使用して送信されます。 |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | 該当なし | Media Analytics のコンテキストデータは、予約変数に自動的に設定されます。実装コード内で eVar、prop およびイベントへのマッピングは不要になりました。お客様は、処理ルールを使用してコンテキストデータを変数にマッピングすることができます。 |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | 該当なし | マッピングは予約変数および処理ルールによって実行されるので、不要になりました。 |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | 該当なし | マッピングは予約変数および処理ルールによって実行されるので、不要になりました。 |

### オプションの変数

| マイルストーン | マイルストーンの構文 | Media Analytics | Media Analytics の構文 |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | 該当なし | 事前定義されたプレーヤーのマッピングは提供されなくなりました。 |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | 該当なし | 事前定義されたプレーヤーのマッピングは提供されなくなりました。 |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | 該当なし | コンテンツ完了では、100％プログレスマーカーのみがサポートされます。 |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | 該当なし | コンテンツ完了では、100％プログレスマーカーのみがサポートされます。 |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK Key: playerName;<br> API Key: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | 該当なし | Media Analytics は、コンテンツの場合は 10 秒、広告の場合は 1 秒に設定されます。他のオプションは利用できません。 |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | 該当なし | Media Analytics は、常に 10％、25％、50％、75％、95％のプログレスマーカーを追跡します。 |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | 該当なし | Media Analytics は、常に 10％、25％、50％、75％、95％のプログレスマーカーを追跡します。 |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | 該当なし | 自動追跡は利用できなくなりました。 |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | 該当なし | 自動追跡は利用できなくなりました。 |

### 広告トラッキング変数

| マイルストーン | マイルストーンの構文 | Media Analytics | Media Analytics の構文 |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | 該当なし | Media Analytics は、コンテンツの場合は 10 秒、広告の場合は 1 秒に設定されます。他のオプションは利用できません。 |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | 該当なし | 広告の場合、プログレスマーカーはデフォルトでは提供されません。広告のプログレスマーカーを作成するには、計算指標を使用します。 |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | 該当なし | 広告の場合、Media Analytics は 1 秒に設定されます。他のオプションは利用できません。 |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | 該当なし | 自動追跡は利用できなくなりました。 |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | 該当なし | 自動追跡は利用できなくなりました。 |

### メディアモジュールメソッド

| マイルストーン | マイルストーンの構文 | Media Analytics | Media Analytics の構文 |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`：（必須）ビデオレポートに表示するビデオの名前。 | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`：（必須）ビデオの長さ（秒単位）。 | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`：（必須）ビデオの視聴に使用されるメディアプレーヤーの名前。ビデオレポートに表示する名前です。 | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name`：（必須）広告の名前または ID。 | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`：（必須）広告の長さ。 | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`：（必須）広告の表示に使用するメディアプレーヤーの名前。 | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`：広告が埋め込まれたプライマリコンテンツの名前または ID。 | 該当なし | 自動的に継承される。 |
| parentPod | `parentPod`：広告が表示されたプライマリコンテンツ内の位置。 | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`：広告が表示されるポッド内の位置。 | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`：この再生に適用される CPM または暗号化された CPM（「~」のプレフィックスが付く）。 | 該当なし | デフォルトでは Media Analytics で使用できません。 |
| Media.click | `s.Media.click(name, offset)` | 該当なし | カスタムリンクの分析呼び出しを使用してクリックを追跡する。 |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause<br> または <br>trackEvent | `trackPause()` <br> または `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> または <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | 追加の変数を指定するには、カスタムまたは標準のメタデータを使用します。 | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | 該当なし | トラッキングコールの頻度は自動的に設定されます。 |
