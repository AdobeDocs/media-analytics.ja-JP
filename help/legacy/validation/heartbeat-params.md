---
title: ハートビートパラメーターの説明
description: Media Analytics（ハートビート）サーバーでアドビが収集して処理するハートビートパラメーターについて説明します。
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: "Streaming Media, Variables"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 99%

---

# Media Analytics（ハートビート）パラメーターの説明 {#heartbeat-parameter-descriptions}

Media Analytics（ハートビート）サーバーでアドビが収集して処理する Media Analytics パラメーターの一覧です。

## すべてのイベント

| 名前 | データソース |  説明  |
| ---  | --- | --- |
| `s:event:type` | メディア SDK | （必須）<br/><br/>追跡されるイベントのタイプ。イベントタイプ： <ul> <li> s:event:type=start </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | メディア SDK | （必須）<br/><br/>このセッションにおける同じタイプの最後のイベントのタイムスタンプ。値は -1 です。 |
| `l:event:ts` | メディア SDK | （必須）<br/><br/>イベントのタイムスタンプ。 |
| `l:event:duration` | メディア SDK | （必須）<br/><br/>この値は、プレーヤーではなく、メディア SDK によって内部的に設定されます（ミリ秒単位）。バックエンドで滞在時間の指標を算出するのに使用されます。例えば a.media.totalTimePlayed は、生成されたすべての再生（type=play）ハードビートの総時間として算出されます。<br/>*注意：*「状態変更イベント」（例えば、type=complete、type=chapter_complete または type=bitrate_change）である特定のイベントに対して、このパラメーターは、0 に設定されます。 |
| `l:event:playhead` | VideoInfo | （必須）<br/><br/>イベントが記録された場合、再生ヘッドは、現在アクティブなアセット（メインまたは広告）の内部にあります。 |
| `s:event:sid` | メディア SDK | （必須）<br/><br/>セッション ID（ランダムに生成された文字列）。特定のセッションのすべてのイベント（ビデオ + 広告）は同じである必要があります。 |
| `l:asset:duration` / `l:asset:length` <br/> （長さの期間から名前を変更） | VideoInfo | （必須）<br/><br/>メインアセットのビデオアセットの長さ。 |
| `s:asset:publisher` | MediaHeartbeatConfig | （必須）<br/><br/>アセットの投稿者。 |
| `s:asset:video_id` | VideoInfo | （必須）<br/><br/>投稿者のカタログでビデオを一意に識別する ID。 |
| `s:asset:type` | メディア SDK | （必須）<br/><br/>アセットのタイプ（メインまたは広告）。 |
| `s:stream:type` | VideoInfo | （必須）<br/><br/>ストリームのタイプ。次のいずれかになります。 <ul> <li> live </li> <li> vod </li> <li> 線形 </li> </ul> |
| `s:user:id` | モバイルの config オブジェクト、App Measurement VisitorID | （任意）<br/><br/>ユーザーが特別に設定した訪問者 ID。 |
| `s:user:aid` | Experience Cloud 組織 | （任意）<br/><br/>ユーザーの Analytics 訪問者 ID 値。 |
| `s:user:mid` | Experience Cloud 組織 | （必須）<br/><br/>ユーザーの Experience Cloud 訪問者 ID 値。 |
| `s:cuser:customer_user_ids_x` | MediaHeartbeatConfig | （任意）<br/><br/>Audience Manager で設定したすべての顧客のユーザー ID。 |
| `l:aam:loc_hint` | MediaHeartbeatConfig | （必須）<br/><br/>aa_start の後の各ペイロードで送信した AAM データ。 |
| `s:aam:blob` | MediaHeartbeatConfig | （必須）<br/><br/>aa_start の後の各ペイロードで送信した AAM データ。 |
| `s:sc:rsid` | レポートスイート ID（複数の場合もあります） | （必須）<br/><br/>レポート送信先の Adobe Analytics RSID。 |
| `s:sc:tracking_server` | MediaHeartbeatConfig | （必須）<br/><br/>Adobe Analytics トラッキングサーバー。 |
| `h:sc:ssl` | MediaHeartbeatConfig | （必須）<br/><br/>トラフィックが HTTPS（1 に設定されている場合）または HTTP（0 に設定されている場合）のどちらを使用するか。 |
| `s:sp:ovp` | MediaHeartbeatConfig | （任意）<br/><br/>Primetime プレーヤーの場合は「primetime」、他のプレーヤーの場合は実際の OVP に設定されます。 |
| `s:sp:sdk` | MediaHeartbeatConfig | （必須）<br/><br/>OVP バージョン文字列。 |
| `s:sp:player_name` | VideoInfo | （必須）<br/><br/>ビデオプレーヤー名（実際のプレーヤーソフトウェア。プレーヤーの識別に使用） |
| `s:sp:channel` | MediaHeartbeatConfig | （任意）<br/><br/>ユーザーがコンテンツを視聴しているチャネル。モバイルアプリの場合、アプリ名。Web サイトの場合、ドメイン名。 |
| `s:sp:hb_version` | メディア SDK | （必須）<br/><br/>呼び出しを発行するメディア SDK ライブラリのバージョン番号。 |
| `l:stream:bitrate` | QoSInfo | （必須）<br/><br/>ストリームビットレートの現在の値（bps）。 |

## エラーイベント

| 名前 | データソース | 説明   |
| ---  | --- | --- |
| `s:event:source` | メディア SDK | （必須）<br/><br/>プレーヤー内部またはアプリケーションレベルの、エラーのソース。 |
| `s:event:id` | メディア SDK | （必須）<br/><br/>エラーを一意に識別するエラー ID。 |

## 広告イベント

| 名前 | データソース | 説明   |
| ---  | --- | --- |
| `s:asset:ad_id` | AdInfo | （必須）<br/><br/>広告の名前。 |
| `s:asset:ad_sid` | メディア SDK | （必須）<br/><br/>メディア SDK によって生成される一意の ID。広告関連のすべての ping に追加されます。 |
| `s:asset:pod_id` | メディア SDK | （必須）<br/><br/>ビデオ内部のポッド ID。この値は、次の式に基づいて自動的に計算されます。<br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| `s:asset:pod_position` | AdBreakInfo | （必須）<br/><br/>ポッド内部の広告のインデックス（最初の広告はインデックス 0、2 番目の広告はインデックス 1、以下同様となります）。 |
| `s:asset:resolver` | AdBreakInfo | （必須）<br/><br/>広告のリゾルバー。 |
| `s:meta:custom_ad_metadata.x` | MediaHeartbeat | （任意）<br/><br/>カスタム広告メタデータ。 |

## チャプターイベント

| 名前 | データソース | 説明   |
| ---  | --- | --- |
| `s:stream:chapter_sid` | メディア SDK | （必須）<br/><br/>チャプターの再生インスタンスに関連付けられた一意の ID。<br/> **注意：**&#x200B;チャプターは、ユーザーによって実行されたシークバック操作が原因で複数回再生される可能性があります。 |
| `s:stream:chapter_name` | ChapterInfo | （任意）<br/><br/>チャプターのわかりやすい（つまり、人間が理解できる）名前。 |
| `s:stream:chapter_id` | メディア SDK | （必須）<br/><br/>チャプターの一意の ID。この値は、次の式に基づいて自動的に計算されます。<br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| `l:stream:chapter_pos` | ChapterInfo | （必須）<br/><br/>チャプターのリストにあるチャプターのインデックス（1 から始まる）。 |
| `l:stream:chapter_offset` | ChapterInfo | （必須）<br/><br/>広告を除く、メインコンテンツ内のチャプターのオフセット（秒単位で表現される）。 |
| `l:stream:chapter_length` | ChapterInfo | （必須）<br/><br/>チャプターの時間（秒単位で表現される）。 |
| `s:meta:custom_chapter_metadata.x` | ChapterInfo | （任意）<br/><br/>カスタムチャプターメタデータ。 |

## セッション終了イベント

| 名前 | データソース | 説明   |
| ---  | --- | --- |
| `s:event:type=end` | メディア SDK | （必須）<br/><br/> `end` `close` |
