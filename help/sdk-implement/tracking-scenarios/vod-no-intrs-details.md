---
seo-title: 広告のない VOD 再生
title: 広告のない VOD 再生
uuid: ee2a1b79-2c2f-42e1-8e81- b62bdd0d8cb
translation-type: tm+mt
source-git-commit: b2d2f7078d655c6e50b3f2925002f93d5a0af533

---


# 広告のない VOD 再生{#vod-playback-with-no-ads}

## シナリオ {#section_E4B558253AD84ED59256EDB60CED02AE}

このシナリオは、広告のない 1 つの VOD アセットで構成され、最初から最後まで 1 回再生されます。

| トリガー | ハートビートメソッド | ネットワーク呼び出し | メモ   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Analytics Content Start、Heartbeat Content Start | これは、再生をクリックするユーザーか、自動再生イベントである可能性があります。 |
| メディアの最初のフレーム | `trackPlay` | Heartbeat Content Play | このメソッドは、タイマーをトリガーし、これ以降、ハートビートは、再生が継続する間、10 秒ごとに送信されます。 |
| コンテンツ再生 |  | Content Heartbeats |  |
| コンテンツが完了した | `trackComplete` | Heartbeat Content Complete | *Complete* は、再生ヘッドの終わりに達したことを意味します。 |

## パラメーター {#section_45D7B10031524411B91E2C569F7818B0}

Heartbeat 呼び出し時に確認される同じ値の多くは、Adobe Analytics `Content Start`Content Start 呼び出し時にも確認されます。様々なメディアレポートに入力するためにアドビが使用する多くのパラメーターがありますが、最も重要なパラメーターのみを次の表に示します。

### Heartbeat Content Start

| パラメーター | 値 | メモ   |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe レポートスイート ID&gt; |  |
| `s:sc:tracking_server` | &lt;Analytics トラッキングサーバー URL&gt; |  |
| `s:user:mid` | 設定される必要がある | `Adobe Analytics Content Start` 呼び出しのmid値と一致する必要があります。 |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;メディア名&gt; |  |
| `s:meta:*` | オプション | メディアに設定されたカスタムメタデータ。 |

## Heartbeat Content Play {#section_2ABBD51D3A6D45ABA92CC516E414417A}

These parameters should look nearly identical to the `Heartbeat Content Start` call, but the key difference is the `s:event:type` parameter. その他のパラメーターは、そのまま存在する必要があります。

| パラメーター | 値 | メモ   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Content Heartbeats {#section_3B5945336E464160A94518231CEE8F53}

メディアの再生中に、タイマーは少なくとも1つのハートビートを10秒ごとに送信します。それらのハートビートには、再生、広告、バッファーなどに関する情報が含まれています。各ハートビートの厳密なコンテンツは、このドキュメントの範囲外ですが、重要な問題は、ハートビートは、再生が続く間、常にトリガーされるということです。

Content Heartbeats で、以下のパラメーターを探します。

| パラメーター | 値 | メモ   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;再生ヘッド位置&gt;例:50,60,70 | このパラメーターは、再生ヘッドの現在の位置を反映します。 |

## Heartbeat Content Complete {#section_33BCC4C3181940C39446A57C25D82179}

再生が完了した場合、つまり、再生ヘッドの終わりに達した場合、`Heartbeat Content Complete` 呼び出しが送信されます。この呼び出しは、他のハートビート呼び出しに似ていますが、いくつかの特有のパラメーターが含まれています。

| パラメーター | 値 | メモ   |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## サンプルコード {#section_glq_vw3_x2b}

このシナリオでは、コンテンツの長さは 40 秒です。最後まで中断なく再生されます。

![](assets/main-content-regular-playback.png)

### Android

```java
// Set up  mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay  
//    is used, i.e., there's an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts,  
//    i.e., the first frame of media is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end,  
//    i.e., when the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not watch  
//    the media to completion.  
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

### iOS

```
when the user clicks Play 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 

NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there's an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 

// 2. Call trackPlay when the playback actually starts, i.e., when the  
//    first frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end, i.e.,  
//    when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 

// 4. Call trackSessionEnd when the playback session is over. This method  
//    must be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME, Configuration.MEDIA_ID,  
Configuration.MEDIA_LENGTH,MediaHeartbeat.StreamType.VOD); 
var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 

}; 

// 1. Call trackSessionStart() when the user clicks play, or when autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the main content starts, i.e.,  
//    the first frame of the media content is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end,  
    i.e., the media completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not  
//    watch the media to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........
```

