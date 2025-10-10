---
title: '順次トラッキングを含むライブメインコンテンツ '
description: メディア SDK を使用して、順次トラッキングを含むライブコンテンツをトラッキングする方法の例を示します。
uuid: b03477b6-9be8-4b67-a5a0-4cef3cf262ab
exl-id: 277a72b8-453b-41e5-b640-65c43587baf8
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 順次トラッキングを含むライブメインコンテンツ{#live-main-content-with-sequential-tracking}

## シナリオ {#scenario}

このシナリオでは、ライブストリームに参加後、40 秒間広告が再生されていない、1 つのライブアセットがあります。

これは、[広告のない VOD 再生](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)シナリオと同じシナリオですが、コンテンツの一部はスクラブされ、メインコンテンツのあるポイントから別のポイントまでのシークが完了します。

| トリガー | ハートビートメソッド |  ネットワーク呼び出し |  メモ   |
| --- | --- | --- | --- |
| ユーザーが[!UICONTROL 再生]をクリックする | trackSessionStart | Analytics Content Start、Heartbeat Content Start | Measurement Library は、プリロール広告があることに気づかないので、これらのネットワーク呼び出しは、[広告のない VOD 再生](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)シナリオと同一です。 |
| コンテンツ再生の最初のフレーム。 | trackPlay | Heartbeat Content Play | メインコンテンツの前にチャプターコンテンツを再生する場合、ハートビートは、チャプターが開始する際に開始されます。 |
| コンテンツ再生 | | Content Heartbeats | このネットワーク呼び出しは、[広告のない VOD 再生](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)シナリオとまったく同じです。 |
| セッション 1 終了（Episode 1 終了） | trackComplete / trackSessionEnd | Heartbeat Content Complete | 「Complete」は、最初のエピソードの session1 に到達し、視聴が完了したことを意味します。次のエピソードのセッションを開始する前に、このセッションを終わらせる必要があります。 |
| Episode 2 開始（Session 2 開始） | trackSessionStart | Analytics Content Start、Heartbeat Content Start | これは、ユーザーが最初のエピソードを視聴し、別のエピソードまで視聴し続けたためです |
| メディアの最初のフレーム | trackPlay | Heartbeat Content Play | このメソッドは、タイマーをトリガーし、これ以降、ハートビートは、再生が続く限り、10 秒ごとに送信されます。 |
| コンテンツ再生 | | Content Heartbeats | |
| セッション終了（Episode2 終了） | trackComplete / trackSessionEnd | Heartbeat Content Complete | 「Complete」は、2 番目のエピソードの session2 に到達し、視聴が完了したことを意味します。次のエピソードのセッションを開始する前に、このセッションを終わらせる必要があります。 |

## パラメーター {#parameters}

### Heartbeat Content Start

| パラメーター | 値 | メモ |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe レポートスイート ID> |  |
| `s:sc:tracking_serve` | &lt;Analytics トラッキングサーバー URL> |  |
| `s:user:mid` | `s:user:mid` | Adobe Analytics Content Start 呼び出しの mid 値と一致する必要がある |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;メディア名> |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` | *オプション* | メディアに設定されたカスタムメタデータ |

## Heartbeat Content Play {#heartbeat-content-play}

Heartbeat Content Start 呼び出しと同じように見えますが、「s:event:type」パラメーターに重要な違いがあります。すべてのパラメーターは、ここで準備ができている必要があります。

| パラメーター | 値 | メモ |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Content Heartbeats {#content-heartbeats}

メディア再生中に、1 つ以上のハートビートを 10 秒ごと（メインコンテンツ）および 1 秒ごと（広告）に送信するタイマーがあります。それらのハートビートには、再生、広告、バッファーおよびその他多くに関する情報が含まれます。各ハートビートの厳密なコンテンツは、このドキュメントの範囲外であり、検証に重要なことは、ハートビートは、再生が続く間、常にトリガーされるということです。

Content Heartbeats では、いくつかの特定の事柄を探します。

| パラメーター | 値 | メモ |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;再生ヘッドの位置> 例：50、60、70 | これは、再生ヘッドの現在の位置を反映する必要があります。 |

## Heartbeat Content Complete {#heartbeat-content-complete}

任意のエピソードの再生が完了した場合（再生ヘッドがエピソードの境界を越える）、Heartbeat Content Complete 呼び出しが送信されます。これは、他のハートビート呼び出しに似ていますが、いくつか特有のものが含まれます。

| パラメーター | 値 | メモ |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## サンプルコード {#sample-code}

![](assets/ios-live-noads-multiplesessions.png)

### Android

以下に、期待される API 呼び出し順序を示します。

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., when there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing 1st episode/session.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2 /episode 2 of the same live stream.  
// There is no need to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes the 
//    start of session 2 
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue similarly tracking further sessions in the live stream if required 
```

### iOS

以下に、期待される API 呼び出し順序を示します。

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
  
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
  
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
  
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing the first 
//    episode/session. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 4. Call trackSessionEnd to end session 1 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Start tracking session 2 / episode 2 of the same live stream, No need to  
// reinstantiate mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 5. Call trackSessionStart when the playhead reaches a point that denotes  
//    start of session 2 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 6. Call trackPlay to start tracking session 2 playback 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 7. Call trackComplete when the playback reaches the end of session 2,  
//    i.e., when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 
 
// 8. Call trackSessionEnd to end the session 2 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```

### JavaScript

以下に、期待される API 呼び出し順序を示します。

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of a session,  
//    i.e., whn playback completes and finishes playing the 1st episode/session. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2/episode 2 of the same live stream. There is no need  
// to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
var mediaInfo2 = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

var mediaMetadata2 = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes  
//    the start of session 2 
this._mediaHeartbeat.trackSessionStart(mediaInfo2, mediaMetadata2); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```
