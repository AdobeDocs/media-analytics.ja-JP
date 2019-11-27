---
title: Chromecast のメタデータキー
description: Chromecast 上で、標準ビデオおよび広告メタデータがトラッキングコールで送信されるようにする設定を説明します。
uuid: c446ad41-51b8-46d6-9bc1-abfae866023f
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Chromecast のメタデータキー {#chromecast-metadata-keys}

ビデオと広告の標準メタデータをそれぞれメディアと広告の情報オブジェクトに設定できます。ビデオや広告メタデータの定数キーを使用すると、追跡 API を呼び出す前に、標準メタデータを含むディクショナリが情報オブジェクトに設定されます。標準メタデータ定数の一覧と例については、以下の表を参照してください。

## メタデータ定数 {#video-metadata-constants}

| メタデータ名 | コンテキストデータキー | 定数名 |
| --- | --- | --- |
| Show | `a.media.show` | `ADBMobile.media.VideoMetadataKeys.SHOW` |
| シーズン | `a.media.season` | `ADBMobile.media.VideoMetadataKeys.SEASON` |
| エピソード | `a.media.episode` | `ADBMobile.media.VideoMetadataKeys.EPISODE` |
| アセット | `a.media.asset` | `ADBMobile.media.VideoMetadataKeys.TMS_ID` |
| ジャンル | `a.media.genre` | `ADBMobile.media.VideoMetadataKeys.GENRE` |
| 初回放送日 | `a.media.airDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE` |
| 初回デジタル放送日 | `a.media.digitalDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE` |
| レーティング | `a.media.rating` | `ADBMobile.media.VideoMetadataKeys.RATING` |
| 作成者 | `a.media.originator` | `ADBMobile.media.VideoMetadataKeys.ORIGINATOR` |
| ネットワーク | `a.media.network` | `ADBMobile.media.VideoMetadataKeys.NETWORK` |
| 番組タイプ | `a.media.type` | `ADBMobile.media.VideoMetadataKeys.SHOW_TYPE` |
| 広告読み込み | `a.media.adLoad` | `ADBMobile.media.VideoMetadataKeys.AD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `ADBMobile.media.VideoMetadataKeys.MVPD` |
| 認証済み | `a.media.pass.auth` | `ADBMobile.media.VideoMetadataKeys.AUTHORIZED` |
| 日パート | `a.media.dayPart` | `ADBMobile.media.VideoMetadataKeys.DAY_PART` |
| フィード | `a.media.feed` | `ADBMobile.media.VideoMetadataKeys.FEED` |
| ストリーム形式 | `a.media.format` | `ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT` |

## 広告メタデータ定数 {#ad-metadata-constants}

| メタデータ名 | コンテキストデータキー | 定数名 |
| --- | --- | --- |
| 広告主 | `a.media.ad.advertiser` | `ADBMobile.media.AdMetadataKeys.ADVERTISER` |
| キャンペーン ID | `a.media.ad.campaign` | `ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID` |
| クリエイティブ ID | `a.media.ad.creative` | `ADBMobile.media.AdMetadataKeys.CREATIVE_ID` |
| プレースメント ID | `a.media.ad.placement` | `ADBMobile.media.AdMetadataKeys.PLACEMENT_ID` |
| サイト ID | `a.media.ad.site` | `ADBMobile.media.AdMetadataKeys.SITE_ID` |
| クリエイティブ URL | `a.media.ad.creativeURL` | `ADBMobile.media.AdMetadataKeys.CREATIVE_URL` |

## Chromecast の実装例 {#sample-implementations-for-chromecast}

### ビデオ

```js
// setting Standard Video Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["videotype"] = "episode"; 
 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "sample show"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "sample season"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.EPISODE] = "sample episode"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.TMS_ID] = "sample tms_id"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "sample genre"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "sample first_air_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "sample first_digital_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.RATING] = "sample rating"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.ORIGINATOR] = "sample originator"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.NETWORK] = "sample network"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "sample show type"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "sample ad load"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "sample mvpd"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "sample authorized"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.DAY_PART] = "sample day_part"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FEED] = "sample feed"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT] = "sample format"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### Audio

```js
// setting Standard Audio Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["audiotype"] = "podcast"; 
var standardAudioMetadata = {}; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ARTIST] = “sample artist”; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ALBUM] = "sample album" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.LABEL] = "sample label"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.AUTHOR] = "sample author" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.STATION] = "sample station " ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.PUBLISHER] = "sample publisher"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType, content.mediaType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudiooMetadata] = standardAudiooMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### 広告

```js
// setting Standard Ad Metadata as context data on ad start event 
var standardAdMetadata = {}; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = “sample campaign”; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.ADVERTISER] = "sample advertiser" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "sample creativeid"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.PLACEMENT_ID] = "sample placement id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.SITE_ID] = "sample site id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "sample creative url"; 
 
var adObject = ADBMobile.media.createAdObject(ad.name, ad.id, ad.position, ad.length); 
adObject[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardVideoMetadata; 
 
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, this._player.getAdInfo(), adContextData);
```

