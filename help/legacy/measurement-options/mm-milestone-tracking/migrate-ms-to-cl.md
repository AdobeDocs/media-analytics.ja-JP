---
title: マイルストーンからカスタムリンクへの移行
description: マイルストーン変数をカスタムリンクに変更し、マイルストーンモジュールのメソッドをカスタムリンク構文に変更する方法を説明します。
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/VrVa44XnAVGI2kNPEFfTB2S840O8jQdvI-PuGX5Y3nM
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 598
ht-degree: 81%

---

# マイルストーンからカスタムリンクへの移行{#migrating-from-milestone-to-custom-link}

## 概要 {#overview}

動画測定のコアコンセプトは、マイルストーンとカスタムリンクトラッキングで同じです。これは、動画プレーヤーのイベントを取得して分析方法にマッピングすると同時に、プレーヤーのメタデータと値を取得し、分析変数にマッピングします。 カスタムリンクのアプローチは、実装と収集されたデータの両方をスリム化し、簡素化するものとみなすべきです。 カスタムリンクソリューションでは、ビデオ測定に事前に定義された変数やメソッドはありません。完全なカスタムセットアップが必要です。 プレーヤーのイベントコードを更新して、開始や完了などの基本的なプレイヤーイベントに対するカスタムリンクトラッキング呼び出しを指すように設定できます。 詳しくは、「[カスタムリンク実装ガイド](/help/legacy/measurement-options/cl-in-aa/cl-impl-guide.md) 」を参照してください。

以下の表では、マイルストーンソリューションとカスタムリンクソリューション間の変更について説明します。

## 移行ガイド {#migration-guide}

### ビデオ変数リファレンス

| マイルストーンの指標 | 変数の種類 | カスタムリンク |
| --- | --- | --- |
| コンテンツ | eVar<br>デフォルトの有効期限：訪問 | 独自の eVar を定義する。 |
| コンテンツタイプ | eVar<br>デフォルトの有効期限：ページビュー | 独自の eVar を定義する。 |
| コンテンツ視聴時間 | イベント<br>タイプ：カウンター | 独自のイベントを定義する。 |
| ビデオ開始 | イベント<br>タイプ：カウンター | 独自のイベントを定義する。 |
| ビデオ完了 | イベント<br>タイプ：カウンター | 独自のイベントを定義する。 |

### メディアモジュール変数

| マイルストーン | マイルストーンの構文 | カスタムリンク | カスタムリンク構文 |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | 該当なし | コンテキストデータの eVar、prop およびイベントへのマッピングは処理ルールによって実施されるようになりました。 |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### オプションの変数

| マイルストーン | マイルストーンの構文 | カスタムリンク | カスタムリンク構文 |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | 該当なし | 使用不可。 |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | 該当なし | 使用不可。 |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | 該当なし | 使用不可。 |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | 該当なし | 使用不可。 |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | リンクの呼び出しで eVar またはコンテキストデータ変数を設定する。 | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | 該当なし | 使用不可。 |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | 該当なし | 使用不可。 |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | 該当なし | 使用不可。 |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | 該当なし | 使用不可。 |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | 該当なし | 使用不可。 |

### 広告トラッキング変数

| マイルストーン | マイルストーンの構文 | カスタムリンク | カスタムリンク構文 |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | 該当なし | 使用不可。 |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | 該当なし | 使用不可。 |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | 該当なし | 使用不可。 |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | 該当なし | 使用不可。 |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | 該当なし | 使用不可。 |

### メディアモジュールメソッド

| マイルストーン | マイルストーンの構文 | カスタムリンク | カスタムリンク構文 |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`：（必須）ビデオレポートに表示するビデオの名前。 | リンクの呼び出しで eVar またはコンテキストデータ変数を設定する。 | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`：（必須）ビデオの長さ（秒単位）。 | リンクの呼び出しで eVar またはコンテキストデータ変数を設定する。 | `s.contextData['video.length']` <br> `  = "90";` |
| mediaPlayerName | `mediaPlayerName`：（必須）ビデオの視聴に使用されるメディアプレーヤーの名前。ビデオレポートに表示する名前です。 | リンクの呼び出しで eVar またはコンテキストデータ変数を設定する。 | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | 該当なし | 使用不可。 |
| name | `name`：（必須）広告の名前または ID。 | 該当なし | 使用不可。 |
| length | `length`：（必須）広告の長さ。 | 該当なし | 使用不可。 |
| playerName | `playerName`：（必須）広告の表示に使用するメディアプレーヤーの名前。 | 該当なし | 使用不可。 |
| parentName | `parentName`：広告が埋め込まれたプライマリコンテンツの名前または ID。 | 該当なし | 使用不可。 |
| parentPod | `parentPod`：広告が表示されたプライマリコンテンツ内の位置。 | 該当なし | 使用不可。 |
| parentPodPosition | `parentPodPosition`：広告が表示されるポッド内の位置。 | 該当なし | 使用不可。 |
| CPM | `CPM`：この再生に適用される CPM または暗号化された CPM（「~」の接頭辞が付く）。 | 該当なし | 使用不可。 |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | カスタムリンクの分析呼び出しを使用してクリックを追跡する。 |
| Media.close | `s.Media.close(mediaName)` | 該当なし | 使用不可。 |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | 該当なし | 使用不可。 |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | 該当なし | 使用不可。 |
| Media.monitor | `s.Media.monitor(s, media)` | リンクの呼び出しで eVar またはコンテキストデータ変数を設定する。 | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | 該当なし | 使用不可。 |
