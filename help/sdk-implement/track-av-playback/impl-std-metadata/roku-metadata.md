---
seo-title: Roku のメタデータキー
title: Roku のメタデータキー
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Roku のメタデータキー{#roku-metadata-keys}

標準ビデオ、オーディオ、広告メタデータは、それぞれメディアおよび広告情報オブジェクトに設定できます。 ビデオや広告メタデータの定数キーを使用すると、追跡 API を呼び出す前に、標準メタデータを含むディクショナリが情報オブジェクトに設定されます。標準メタデータ定数の一覧と例については、以下の表を参照してください。

## ビデオメタデータ定数 {#video-metadata-constants}

| メタデータ名 | コンテキストデータキー | 定数名 |
| --- | --- | --- |
| Show | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
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

## オーディオメタデータ定数 {#audio-metadata-constants}

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
| `MEDIA_STANDARD_MEDIA_METADATA` | メタデータを設定する `MediaInfo` 定数 `trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | 広告メタデータを設定する定 `EventData` 数 `trackEvent` |
| `MEDIA_RESUMED` | ビデオ再開のハートビートを送信する定数。To resume video tracking of previously stopped content, you need to set the `MEDIA_RESUMED` property on the `mediaInfo` object when you call `mediaTrackLoad`. (`MEDIA_RESUMED` is not an event that you can track using the `mediaTrackEvent` API.) アプリケーションで、ユーザーが視聴を中断したものの、視聴再開の意図を示したコンテンツのトラッキングを継続したい場合は、`MEDIA_RESUMED` を true に設定する必要があります。<br/><br/>例えば、あるユーザーがコンテンツの 30％を視聴してからアプリを閉じたとします。その場合はセッションが終了します。Later, if the same user returns to the same content, and the application allows that user to resume from the same point where they left off, then the application should set `MEDIA_RESUMED` to "true" while calling the `mediaTrackLoad` API. これにより、同じビデオコンテンツのこの 2 つのメディアセッションをリンクさせることができます。実装の例は次のとおりです。 <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)`<br/><br/>この例では、ビデオの新しいセッションが作成されますが、SDK によってイベントタイプ「resume」のハートビートリクエストも送信されます。これをレポートで使用することで、2 つのメディアセッションをリンクさせることができます。 |

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

