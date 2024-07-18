---
title: Roku のメタデータキー
description: Roku で使用可能なメタデータキーについて説明し、標準メタデータ定数の一覧を示します。
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
exl-id: 687dbaa5-4723-4b3f-ab1e-4d5bf447cddf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 98%

---

# Roku のメタデータキー{#roku-metadata-keys}

ビデオ、オーディオおよび広告の標準メタデータをそれぞれメディアと広告の情報オブジェクトに設定できます。ビデオや広告メタデータの定数キーを使用すると、追跡 API を呼び出す前に、標準メタデータを含むディクショナリが情報オブジェクトに設定されます。標準メタデータ定数の一覧と例については、以下の表を参照してください。

## ビデオメタデータ定数 {#video-metadata-constants}

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
| `MEDIA_RESUMED` | ビデオ再開のハートビートを送信する定数。以前に停止されたコンテンツのビデオトラッキングを再開するには、`mediaTrackLoad` を呼び出す際に、`mediaInfo` オブジェクトの `MEDIA_RESUMED` プロパティを設定する必要があります（`MEDIA_RESUMED` は、`mediaTrackEvent` API を使用してトラッキングできるイベントではありません）。アプリケーションで、ユーザーが視聴を中断したものの、視聴再開の意図を示したコンテンツのトラッキングを継続したい場合は、`MEDIA_RESUMED` を true に設定する必要があります。<br/><br/>例えば、あるユーザーがコンテンツの 30％を視聴してからアプリを閉じたとします。その場合はセッションが終了します。その後、同じユーザーが同じコンテンツに再度アクセスした場合、アプリケーションは、そのユーザーが中断した場所から視聴を再開できるようにします。アプリケーションはそのうえで `mediaTrackLoad` API を呼び出し、`MEDIA_RESUMED` を「true」に設定します。これにより、同じビデオコンテンツのこの 2 つのメディアセッションをリンクさせることができます。実装の例を次に示します。<br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>この例では、ビデオの新しいセッションが作成されますが、SDK によってイベントタイプ「resume」のハートビートリクエストも送信されます。これをレポートで使用することで、2 つのメディアセッションをリンクさせることができます。 |

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
