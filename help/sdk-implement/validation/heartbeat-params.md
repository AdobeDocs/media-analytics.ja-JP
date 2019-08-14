---
seo-title: ハートビートパラメーターの説明
title: ハートビートパラメーターの説明
uuid: e9ddda32-0952-43d0- a702-49f5b1bfd8cf
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Media Analytics（ハートビート）パラメーターの説明{#heartbeat-parameter-descriptions}

アドビがハートビートサーバー上で収集および処理するMedia Analyticsパラメーターのリスト:

## すべてのイベント

| 名前 | 必須／オプション | データソース | 説明   |
| ---  | :---: | --- | --- |
| `s:event:type` | R | メディア SDK | 追跡されるイベントのタイプ。イベントタイプ： <ul> <li> `s:event:type=start` </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | R | メディア SDK | このセッションにおける同じタイプの最後のイベントのタイムスタンプ。この値は `-1` |
| `l:event:ts` | R | メディア SDK | イベントのタイムスタンプ。 |
| `l:event:duration` | R | メディア SDK | この値はプレーヤーではなく、VHL ライブラリによって内部的に設定されます（単位はミリ秒）。バックエンドで滞在時間の指標を算出するのに使用されます。For example `a.media.totalTimePlayed` `type=play` Note:  For some of the HB that are sent This parameter is set to 0 for certain events because they are "state change events" (e.g., `type=complete` `type=chapter_complete` `type=bitrate_change` |
| `l:event:playhead` | R | `VideoInfo` | イベントが記録された場合、再生ヘッドは、現在アクティブなアセット（メインまたは広告）の内部にあります。 |
| `s:event:sid` | R | メディア SDK | セッション ID（ランダムに生成された文字列）。特定のセッションのすべてのイベント（ビデオ + 広告）は同じである必要があります。 |
| `l:asset:duration / l:asset:length` （名前を `length``duration` | R | `VideoInfo` | メインアセットのビデオアセットの長さ。 |
| `s:asset:publisher` | R | `MediaHeartbeatConfig` | アセットの投稿者。 |
| `s:asset:video_id` | R | `VideoInfo` | 投稿者のカタログでビデオを一意に識別する ID。 |
| `s:asset:type` | R | メディア SDK | アセットのタイプ（メインまたは広告）。 |
| `s:stream:type` | R | `VideoInfo` | ストリームタイプ。以下のいずれかを指定できます。 <ul> <li> `live` </li> <li> `vod` </li> <li> `linear` </li> </ul>を参照してください。 |
| `s:user:id` | O | モバイルの config オブジェクト、App Measurement VisitorID | ユーザーが特別に設定した訪問者 ID。 |
| `s:user:aid` | O | Experience Cloud 組織 | ユーザーの Analytics 訪問者 ID 値。 |
| `s:user:mid` | R | Experience Cloud 組織 | ユーザーの Experience Cloud 訪問者 ID 値。 |
| `s:cuser:customer_user_ids_x` | O | `MediaHeartbeatConfig` | Audience Manager で設定したすべての顧客のユーザー ID。 |
| `l:aam:loc_hint` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:aam:blob` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:sc:rsid` | R | レポートスイート ID（複数の場合もあります） | レポート送信先のAdobe Analytics RSID。 |
| `s:sc:tracking_server` | R | `MediaHeartbeatConfig` | Adobe Analyticsトラッキングサーバー。 |
| `h:sc:ssl` | R | `MediaHeartbeatConfig` | トラフィックが HTTPS（1 に設定されている場合）または HTTP（0 に設定されている場合）のどちらを使用するか。 |
| `s:sp:ovp` | O | `MediaHeartbeatConfig` | Primetime プレーヤーの場合は「primetime」、他のプレーヤーの場合は実際の OVP に設定されます。 |
| `s:sp:sdk` | R | `MediaHeartbeatConfig` | OVP バージョン文字列。 |
| `s:sp:player_name` | R | `VideoInfo` | ビデオプレーヤー名（実際のプレーヤーソフトウェア。プレーヤーの識別に使用） |
| `s:sp:channel` | O | `MediaHeartbeatConfig` | ユーザーがコンテンツを視聴しているチャネル。モバイルアプリの場合、アプリ名。Web サイトの場合、ドメイン名。 |
| `s:sp:hb_version` | R | メディア SDK | 呼び出しを発行する VideoHeartbeat ライブラリのバージョン番号。 |
| `l:stream:bitrate` | R | `QoSInfo` | ストリームビットレートの現在の値（bps）。 |

## エラーイベント

| 名前 | 必須／オプション | データソース | 説明   |
| ---  | :---: | --- | --- |
| `s:event:source` | R | メディア SDK | プレーヤー内部またはアプリケーションレベルの、エラーのソース。 |
| `s:event:id` | R | メディア SDK | エラーを一意に識別するエラー ID。 |

## 広告イベント

| 名前 | 必須／オプション | データソース | 説明   |
| ---  | :---: | --- | --- |
| `s:asset:ad_id` | R | `AdInfo` | 広告の名前。 |
| `s:asset:ad_sid` | R | メディア SDK | メディア SDK によって生成される一意の識別子。広告関連のすべての ping に追加されます。 |
| `s:asset:pod_id` | R | メディア SDK | ビデオ内部のポッド ID。この値は、次の式に基づいて自動的に計算されます。 `MD5(video_id) + "_" + [pod index]` |
| `s:asset:pod_position` | R | `AdBreakInfo` | ポッド内部の広告のインデックス（最初の広告はインデックス 0、2 番目の広告はインデックス 1、以下同様となります）。 |
| `s:asset:resolver` | R | `AdBreakInfo` | 広告のリゾルバー。 |
| `s:meta:custom_ad_metadata.x` | O | `MediaHeartbeat` | カスタム広告メタデータ。 |

## チャプターイベント

| 名前 | 必須／オプション | データソース | 説明   |
| ---  | :---: | --- | --- |
| `s:stream:chapter_sid` | R | メディア SDK | チャプターの再生インスタンスに関連付けられた一意の識別子。注意：チャプターは、ユーザーによって実行されたシークバック操作が原因で複数回再生される可能性があります。 |
| `s:stream:chapter_name` | O | `ChapterInfo` | チャプターのわかりやすい（つまり、人間が理解できる）名前。 |
| `s:stream:chapter_id` | R | メディア SDK | チャプターの一意の ID。この値は、次の式に基づいて自動的に計算されます。 `MD5(video_id) + "_" + chapter_pos` |
| `l:stream:chapter_pos` | R | `ChapterInfo` | チャプターのリストにあるチャプターのインデックス（1 から始まる）。 |
| `l:stream:chapter_offset` | R | `ChapterInfo` | 広告を除く、メインコンテンツ内のチャプターのオフセット（秒単位で表現される）。 |
| `l:stream:chapter_length` | R | `ChapterInfo` | チャプターの時間（秒単位で表現される）。 |
| `s:meta:custom_chapter_metadata.x` | O | `ChapterInfo` | カスタムチャプターメタデータ。 |

## セッション終了イベント

| 名前 | 必須／オプション | データソース | 説明   |
| ---  | :---: | --- | --- |
| `s:event:type=end` | R | メディア SDK | Adobe コード内の  `end``close` |

