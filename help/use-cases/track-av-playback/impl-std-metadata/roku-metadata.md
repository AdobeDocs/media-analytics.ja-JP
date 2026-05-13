---
title: Roku のメタデータキー
description: Roku で使用可能なメタデータキーについて説明し、標準メタデータ定数の一覧を示します。
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
exl-id: 687dbaa5-4723-4b3f-ab1e-4d5bf447cddf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/nWQiQkx66U5JL19U4yV8o4dvm0nLivpyKq29uNlIXTc
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 472
ht-degree: 75%

---

# Roku のメタデータキー{#roku-metadata-keys}

ビデオ、オーディオおよび広告の標準メタデータをそれぞれメディアと広告の情報オブジェクトに設定できます。 ビデオ/広告メタデータの定数キーを使用して、トラック APIを呼び出す前に、info オブジェクトに標準メタデータを含むディクショナリを設定します。 標準メタデータ定数のリスト全体とサンプルについては、次の表を参照してください。

## ビデオメタデータの定数 {#video-metadata-constants}

| メタデータ名 | コンテキストデータキー | 定数名 |
| --- | --- | --- |
| 番組 | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| シーズン | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| エピソード | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| アセット | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| ジャンル | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| 初回放送日 | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| 初回デジタル放送日 | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| レーティング | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| 作成者 | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| ネットワーク | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| 番組タイプ | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| 広告読み込み | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| 認証済み | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| 日パート | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| フィード | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| ストリーム形式 | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## オーディオメタデータの定数 {#audio-metadata-constants}

| メタデータ名 | コンテキストデータキー | 定数名 |
| --- | --- | --- |
| 作者名 | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| アルバム | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| ラベル | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| 作成者 | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| ステーション | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| 発行者 | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## 広告メタデータ定数 {#ad-metadata-constants}

| メタデータ名 | コンテキストデータキー | 定数名 |
| --- | --- | --- |
| 広告主 | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| キャンペーン ID | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| クリエイティブ ID | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| プレースメント ID | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| サイト ID | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| クリエイティブ URL | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## 定数 {#constants}

メディアイベントのトラッキングに利用できる定数は次のとおりです。

### その他の定数

| 定数 | 説明   |
|---|---|
| `ERROR_SOURCE_PLAYER` | エラーソースがプレーヤーの定数 |

### MediaObjectkey 定数（MediaObject インスタンス内のキーとして使用）

| 定数 | 説明   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | `MediaInfo` `trackLoad` にメタデータを設定するための定数 |
| `MEDIA_STANDARD_AD_METADATA` | `EventData` `trackEvent` に広告メタデータを設定するための定数 |
| `MEDIA_RESUMED` | ビデオ再開のハートビートを送信する定数。 以前に停止されたコンテンツのビデオトラッキングを再開するには、`mediaTrackLoad` を呼び出す際に、`mediaInfo` オブジェクトの `MEDIA_RESUMED` プロパティを設定する必要があります （`MEDIA_RESUMED`は、`mediaTrackEvent` APIを使用して追跡できるイベントではありません）。 ユーザーが視聴を停止したが、現在は視聴を再開しようとしているコンテンツをアプリケーションが追跡し続けたい場合、`MEDIA_RESUMED`をtrueに設定する必要があります。 <br/><br/>例えば、あるユーザーがコンテンツの 30％を視聴してからアプリを閉じたとします。 その場合はセッションが終了します。 その後、同じユーザーが同じコンテンツに再度アクセスした場合、アプリケーションは、そのユーザーが中断した場所から視聴を再開できるようにします。アプリケーションはそのうえで `mediaTrackLoad` API を呼び出し、`MEDIA_RESUMED` を「true」に設定します。 その結果、同じビデオコンテンツに対するこれら2つの異なるメディアセッションをリンクできます。 次に、実装の例を示します：<br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>この例では、ビデオの新しいセッションが作成されますが、SDK によってイベントタイプ「resume」のハートビートリクエストも送信されます。これをレポートで使用することで、2 つのメディアセッションをリンクさせることができます。 |

### コンテンツタイプ定数

| 定数 | 説明   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | ストリームタイプ LIVE の定数 |
| `MEDIA_STREAM_TYPE_VOD` | ストリームタイプ VOD の定数 |

### イベントタイプ定数（trackEvent の呼び出しで使用）

| 定数 | 説明   |
|---|---|
| `MEDIA_BUFFER_START` | バッファー開始のイベントタイプ |
| `MEDIA_BUFFER_COMPLETE` | バッファー完了のイベントタイプ |
| `MEDIA_SEEK_START` | シーク開始のイベントタイプ |
| `MEDIA_SEEK_COMPLETE` | シーク完了のイベントタイプ |
| `MEDIA_BITRATE_CHANGE` | ビットレート変更のイベントタイプ |
| `MEDIA_CHAPTER_START` | チャプター開始のイベントタイプ |
| `MEDIA_CHAPTER_COMPLETE` | チャプター完了のイベントタイプ |
| `MEDIA_CHAPTER_SKIP` | 広告開始のイベントタイプ |
| `MEDIA_AD_BREAK_START` | 広告開始のイベントタイプ |
| `MEDIA_AD_BREAK_COMPLETE` | 広告ブレーク完了のイベントタイプ |
| `MEDIA_AD_BREAK_SKIP` | 広告ブレークスキップのイベントタイプ |
| `MEDIA_AD_START` | 広告開始のイベントタイプ |
| `MEDIA_AD_COMPLETE` | 広告完了のイベントタイプ |
| `MEDIA_AD_SKIP` | 広告スキップのイベントタイプ |
