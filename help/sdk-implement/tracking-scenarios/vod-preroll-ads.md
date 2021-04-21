---
title: プリロール広告のある VOD 再生
description: メディア SDK を使用した、プリロール広告を含む VOD コンテンツの追跡方法の例です。
uuid: 5d1022a8-88cb-40aa-919c-60dd592a639e
exl-id: c77f6457-ac3b-4d7a-8eed-e7ebd357a6a5
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '526'
ht-degree: 100%

---

# プリロール広告のある VOD 再生 {#vod-playback-with-pre-roll-ads}

このシナリオでは、メインコンテンツの前にプリロール広告が挿入されています。特に指定のない限り、ネットワーク呼び出しは、[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)シナリオの呼び出しと同じです。ネットワーク呼び出しは同時に発生しますが、ペイロードは異なります。

| トリガー | ハートビートメソッド | ネットワーク呼び出し   | メモ   |
| --- | --- | --- | --- |
| ユーザーが[!UICONTROL 再生]をクリックする | `trackSessionStart` | Analytics Content Start、Heartbeat Content Start | Measurement Library は、プリロール広告があることに気づかないので、これらのネットワーク呼び出しは、[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)シナリオと同一です。 |
| 広告が開始されます。 | <ul> <li> `trackEvent:AdBreakStart` </li> <li> `trackEvent:AdStart` </li> </ul> | Analytics Ad Start、Heartbeat Ad Start |  |
| 広告 #1 のフレームが再生されます。 | `trackPlay` | Heartbeat Ad Play | メインコンテンツの前に広告コンテンツを再生し、ハートビートは、広告が開始する際に開始されます。 |
| 広告が再生されます。 |  | Ad Heartbeats |  |
| 広告 #2の再生が完了します。 | `trackEvent:trackAdComplete` | Heartbeat Ad Complete | 広告の終わりに到達しました。 |
| 広告 #2 の最初のフレームが再生されます。 | `trackEvent:AdStart` | Analytics Ad Start、Heartbeat Ad Start |  |
| 広告が再生されます。 |  | Ad Heartbeats |  |
| 広告 #2の再生が完了します。 | <ul> <li> `trackEvent:trackAdComplete` </li> <li> `trackEvent:AdBreakComplete` </li> </ul> | Heartbeat Ad Complete | 広告の終わりとポッドの終わりに達しました。 |
| コンテンツが再生されます。 |  | Content Heartbeats | このネットワーク呼び出しは、[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)シナリオと同じです。 |
| コンテンツが完了する。 | `trackComplete` | Heartbeat Content Complete | このネットワーク呼び出しは、[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)シナリオと同じです。 |
| セッションが終了する | `trackSessionEnd` |  | `SessionEnd` |

## パラメーター {#parameters}

広告の再生が開始されると、`Heartbeat Ad Start` 呼び出しが送信されます。広告の開始が 10 秒のタイマーと同時に起こらない場合、`Heartbeat Ad Start` 呼び出しは、数秒間遅延され、呼び出しは次の 10 秒のインターバルに進みます。これが発生すると、`Content Heartbeat` 呼び出しは同じインターバルから出ます。この 2 つの呼び出しの違いは、イベントタイプとアセットタイプを調査することで区別できます。

### Heartbeat Ad Start

| パラメーター | 値 | メモ |
|---|---|---|
| `s:event:type` | `start` |  |
| `s:asset:type` | `ad` |  |

広告は、`Content Heartbeats` と同じ基本モデルに従うので、`Ad Play` 呼び出しは、`Content Play` 呼び出しに似ています。

### Heartbeat Ad Play 呼び出し

| パラメーター | 値 | メモ |
|---|---|---|
| `s:event:type` | `play` |  |
| `s:asset:type` | `ad` |  |

これらのパラメーターは `Content Heartbeats` 呼び出しに似ていますが、`Ad Heartbeats` 呼び出しは、いくつかの追加のパラメーターを含んでいます。

### Ad Heartbeats

| パラメーター | 値 | メモ |
|---|---|---|
| `s:event:type` | `play` |  |
| `s:asset:type` | `ad` |  |
| `s:asset:ad_id` | &lt;広告 ID> |  |
| `s:asset:pod_id` | &lt;広告ポッド ID> |  |

`Heartbeat Content Complete` 呼び出しと同様、再生が完了した（再生ヘッドの終わりに達した）場合、`Heartbeat Ad Complete` 呼び出しが送信されます。この呼び出しは、他の `Heartbeat Ad` 呼び出しに似ていますが、いくつか特有のものが含まれます。

### Heartbeat Ad Complete 呼び出し

| パラメーター | 値 | メモ |
|---|---|---|
| `s:event:type` | `complete` |  |
| `s:asset:type` | `ad` |  |

## プリロール広告ブレークのサンプルコード {#sample-code-for-a-pre-roll-ad-break}

このシナリオでは、VOD は、プリロール広告、2 番目のプリロール広告で構成され、次にコンテンツが再生されます。

![](assets/preroll-regular-playback.png)

* **Android** Android でこのシナリオを表示するには、以下のコードを設定します。

   ```java
   // Set up  mediaObject 
   MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
       Configuration.MEDIA_NAME,  
       Configuration.MEDIA_ID,  
       Configuration.MEDIA_LENGTH,  
       MediaHeartbeat.StreamType.VOD 
   ); 
   
   HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
   videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
   videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
   
   // 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
   //    i.e., there's an intent to start playback.  
   _mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
   
   ...... 
   ...... 
   
   // Pre-roll 
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
                                        ADBREAK_POSITION,  
                                        ADBREAK_START_TIME); 
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(AD_NAME,  
                                   AD_ID,  
                                   AD_POSITION,  
                                   AD_LENGTH); 
   
   // Context ad data 
   HashMap<String, String> adMetadata = new HashMap<String, String>(); 
   adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
   adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
   
   // 2. Track the MediaHeartbeat.Event.AdBreakStart event when the pre-roll pod starts  
   //    to play. Note that since this is a pre-roll, call must track the 
   //    "MediaHeartbeat.Event.AdBreakStart" event before you call trackPlay().  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
   
   ....... 
   ....... 
   
   // 3. Track the MediaHeartbeat.Event.AdStart event when the pre-roll pod's ad starts  
   //    to play. Note that since this is a pre-roll, you must track the  
   //    "MediaHeartbeat.Event.AdStart" event before you call trackPlay(). 
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 4. Call trackPlay() when the playback actually starts, i.e., when the first frame  
   //    of the ad video is rendered on the screen. 
   _mediaHeartbeat.trackPlay(); 
   
   ....... 
   ....... 
   
   // 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
   //    i.e., when the ad completes and finishes playing.  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   
   ....... 
   ....... 
   
   // 6. Track the MediaHeartbeat.Event.AdStart event when the pre-roll pod's second ad  
   //    starts to play. 
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 7. Track the MediaHeartbeat.Event.AdComplete event when the second ad reaches the  
   //    end, i.e., the second ad completes and finishes playing. 
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   
   ....... 
   ....... 
   
   // 8. Track the MediaHeartbeat.Event.AdBreakComplete event when all of the ads in the  
   //    pod finish playing.  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   
   ....... 
   ....... 
   
   // 9. Call trackComplete() when the playback reaches the end, i.e., when the video 
   //    completes and finishes playing. 
   _mediaHeartbeat.trackComplete(); 
   
   ........ 
   ........ 
   
   // 10. Call trackSessionEnd() when the playback session is over. This method must be  
   //     called even if the user does not watch the video to completion.  
   _mediaHeartbeat.trackSessionEnd(); 
   
   ........ 
   ........ 
   ```

* **iOS -** iOS でこのシナリオを表示するには、以下のコードを設定します。

   ```
   //  Set up mediaObject 
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                        length:MEDIA_LENGTH  
                        streamType:ADBMediaHeartbeatStreamTypeVOD]; 
   
   NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
   [videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
   [videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
   
   // 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
   //    i.e., there is an intent to start playback. 
   [_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
   ....... 
   ....... 
   
   // Pre-roll 
   ADBMediaObject *adBreakInfo =  
     [ADBMediaHeartbeat createAdBreakObjectWithName:AD_BREAK_NAME  
                        position:AD_BREAK_POSITION  
                        startTime:AD_BREAK_START_TIME]; 
   ADBMediaObject *adInfo =  
     [ADBMediaHeartbeat createAdObjectWithName:AD_NAME  
                        adId:AD_ID  
                        position:AD_POSITION  
                        length:AD_LENGTH]; 
   
   // context ad data 
   NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
   [adDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
   [adDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
   
   // 2. Track the ADBMediaHeartbeatEventAdBreakStart event when the pre-roll pod  
   //    starts to play. Note that since this is a pre-roll, you must track the  
   //    "ADBMediaHeartbeatEventAdBreakStart" event before you call trackPlay. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                    mediaObject:adBreakObject  
                    data:nil]; 
   ....... 
   ....... 
   
   // 3. Track the ADBMediaHeartbeatEventAdStart event when the pre-roll pod's  
   //    ad starts to play. Note that since this is a pre-roll, you must track  
   //    the "ADBMediaHeartbeatEventAdStart" event before you call trackPlay. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                    mediaObject:adObject  
                    data:adDictionary]; 
   ....... 
   ....... 
   
   // 4. Call trackPlay when the playback actually starts, i.e., when the   
   //    first frame of the main content is rendered on the screen. 
   [_mediaHeartbeat trackPlay]; 
   ....... 
   ....... 
   
   // 5. Track the ADBMediaHeartbeatEventAdComplete event when the ad reaches  
   //    the end, i.e., when the video completes and finishes playing. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                    mediaObject:nil  
                    data:nil]; 
   ....... 
   ....... 
   
   // 6. Track the ADBMediaHeartbeatEventAdStart event when the pre-roll pod's  
   //    second ad starts to play. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                    mediaObject:adBreakObject  
                    data:nil]; 
   ....... 
   ....... 
   
   // 7. Track the ADBMediaHeartbeatEventAdComplete event when the second ad  
   //    reaches the end, i.e., it completes and finishes playing. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                    mediaObject:nil  
                    data:nil]; 
   ....... 
   ....... 
   
   // 8. Track the ADBMediaHeartbeatEventAdBreakComplete event when all the  
   //    ads in the pod finish playing. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                    mediaObject:adBreakObject  
                    data:nil]; 
   ....... 
   ....... 
   
   // 9. Call trackComplete when the playback reaches the end, i.e., when the  
   //    video completes and finishes playing. 
   [_mediaHeartbeat trackComplete]; 
   ....... 
   ....... 
   
   // 10. Call trackSessionEnd when the playback session is over. This method  
   //     must be called even if the user does not watch the video to completion. 
   [_mediaHeartbeat trackSessionEnd]; 
   ....... 
   ....... 
   ```

* **JavaScript** JavaScript でこのシナリオを表示するには、以下のテキストを入力します。

   ```js
   // Set up mediaObject 
   var mediaInfo =  
     MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                      Configuration.MEDIA_ID,  
                                      Configuration.MEDIA_LENGTH,MediaHeartbeat.StreamType.VOD); 
   var videoMetadata = { 
       CUSTOM_KEY_1 : CUSTOM_VAL_1,  
       CUSTOM_KEY_2 : CUSTOM_VAL_2, 
       CUSTOM_KEY_3 : CUSTOM_VAL_3 
   }; 
   
   // 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
   //    i.e., there's an intent to start playback. 
   this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
   
   ...... 
   ...... 
   
   // Preroll 
   var adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(ADBREAK_NAME, ADBREAK_POSITION, ADBREAK_START_TIME); 
   var adInfo =  
     MediaHeartbeat.createAdObject(AD_NAME, AD_ID, AD_POSITION, AD_LENGTH); 
   
   // Custom ad metadata 
   var adMetadata = { 
       CUSTOM_AD_KEY_1 : CUSTOM_AD_VAL_1,  
       CUSTOM_AD_KEY_2 : CUSTOM_AD_VAL_2 
   }; 
   
   // 2. Track the MediaHeartbeat.Event.AdBreakStart event when the preroll pod starts to play.  
   //    Note that since this is a preroll, track the MediaHeartbeat.Event.AdBreakStart  
   //    event before you call trackPlay(). 
   this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
   
   ....... 
   ....... 
   
   // 3. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's ad starts to play.  
   //    Note that since this is a preroll, track the MediaHeartbeat.Event.AdStart event before  
   //    you call trackPlay(). 
   this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 4. Call trackPlay() when the playback actually starts, i.e., the first frame of the  
         main content is rendered on the screen.  
   this._mediaHeartbeat.trackPlay(); 
   
   ....... 
   ....... 
   
   // 5. Track event MediaHeartbeat.Event.AdComplete when the ad reaches the end,  
   //    i.e., when it completes and finishes playing. 
   this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
   
   ....... 
   ....... 
   
   // 6. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's second  
   //    ad starts to play. 
   this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 7. Track the MediaHeartbeat.Event.AdComplete event when the second ad reaches  
   //    the end, i.e., when it completes and finishes playing. 
   this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
   
   ....... 
   ....... 
   
   // 8. Track the MediaHeartbeat.Event.AdBreakComplete event when all the ads  
   //    in the pod finish playing. 
   this._mediaheartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
   
   ....... 
   ....... 
   
   // 9. Call trackComplete() when the playback reaches the end, i.e., when it 
   //    completes and finishes playing.  
   this._mediaHeartbeat.trackComplete(); 
   
   // 10. Call trackSessionEnd() when the playback session is over. This method must  
   //     be called even if the user does not watch the video to completion. 
   this._mediaHeartbeat.trackSessionEnd(); 
   
   ....... 
   .......
   ```

## 複数の広告ブレークのサンプルコード {#sample-code-for-multiple-ad-breaks}

このシナリオでは、VOD コンテンツは、プリロール広告、コンテンツ、ミッドロール広告、コンテンツ、ポストロール広告を再生します。

![](assets/ad-content-regular-playback.png)

* **Android** Android でこのシナリオを表示するには、以下のコードを設定します。

   ```java
   // Set up mediaObject 
   MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
       Configuration.MEDIA_NAME,  
       Configuration.MEDIA_ID,  
       Configuration.MEDIA_LENGTH,  
       MediaHeartbeat.StreamType.VOD 
   ); 
   
   HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
   videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
   videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
   
   // 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
   //   i.e., there's an intent to start playback. 
   _mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
   
   ...... 
   ...... 
   
   // Pre-roll 
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
                                        ADBREAK_POSITION,  
                                        ADBREAK_START_TIME); 
   MediaObject adInfo = MediaHeartbeat.createAdObject(AD_NAME,  
                                                      AD_ID,  
                                                      AD_POSITION,  
                                                      AD_LENGTH); 
   
   // Context ad data 
   HashMap<String, String> adMetadata = new HashMap<String, String>(); 
   adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
   adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
   
   // 2. Track the MediaHeartbeat.Event.AdBreakStart event when the pre-roll pod  
   //    starts to play. Note that since this is a pre-roll, you must track the  
   //    "MediaHeartbeat.Event.AdBreakStart" event before you call trackPlay().  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
   
   ....... 
   ....... 
   
   // 3. Track the MediaHeartbeat.Event.AdStart event when the pre-roll pod's ad  
   //    starts to play. Note that since this is a pre-roll, you must track the  
   //    "MediaHeartbeat.Event.AdStart" event before you call trackPlay().  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 4. Call trackPlay() when the playback actually starts, i.e., when the first  
   //    frame of the main content is rendered on the screen.  
   _mediaHeartbeat.trackPlay(); 
   
   ....... 
   ....... 
   
   // 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
   //    i.e., when the ad completes and finishes playing.  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   
   ....... 
   ....... 
   
   // 6. Track the MediaHeartbeat.Event.AdBreakComplete event when all of the ads in  
   //;    the pod finish playing. 
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   
   ....... 
   ....... 
   
   // Mid-roll 
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(mid-roll_BREAK_NAME,  
                                        mid-roll_BREAK_POSITION,  
                                        mid-roll_BREAK_START_TIME); 
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(mid-roll_AD_NAME,  
                                   mid-roll_AD_ID,  
                                   mid-roll_AD_POSITION,  
                                   mid-roll_AD_LENGTH); 
   
   // Context ad data 
   HashMap<String, String> adMetadata = new HashMap<String, String>(); 
   adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
   adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
   
   // 7. Track the MediaHeartbeat.Event.AdBreakStart event when the mid-roll pod  
   //    starts to play.  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
   
   ....... 
   ....... 
   
   // 8. Track the MediaHeartbeat.Event.AdStart event when the mid-roll pod's ad  
   //    starts to play.  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 9. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
   //    i.e., when the adcompletes and finishes playing.  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   
   ....... 
   ....... 
   
   // 10. Track the MediaHeartbeat.Event.AdBreakComplete event when all the ads in the  
   //      mid-roll pod finish playing.  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   
   ....... 
   ....... 
   
   // Post-roll 
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(POSTROLL_BREAK_NAME,  
                                        POSTROLL_BREAK_POSITION,  
                                        POSTROLL_BREAK_START_TIME); 
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(POSTROLL_AD_NAME,  
                                   POSTROLL_AD_ID,  
                                   POSTROLL_AD_POSITION,  
                                   POSTROLL_AD_LENGTH); 
   
   // Context ad data 
   HashMap<String, String> adMetadata = new HashMap<String, String>(); 
   adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
   adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
   
   // 11. Track the MediaHeartbeat.Event.AdBreakStart event when the post-roll pod  
   //     starts to play.  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
   
   ....... 
   ....... 
   
   // 12. Track the MediaHeartbeat.Event.AdStart event when the post-roll pod's  
   //     ad starts to play.  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 13. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the  
   //     end, i.e., when the ad completes and finishes playing. 
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   
   ....... 
   ....... 
   
   // 14. Track the MediaHeartbeat.Event.AdBreakComplete event when all the ads in  
   //     the post-roll pod finish playing.  
   _mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   
   ....... 
   ....... 
   
   // 15. Call trackComplete() when the playback reaches the end, i.e., when the 
   //     video completes and finishes playing. 
   _mediaHeartbeat.trackComplete(); 
   
   ........ 
   ........ 
   
   // 16. Call trackSessionEnd() when the playback session is over. This method  
   //     must be called even if the user does not watch the video to completion.  
   _mediaHeartbeat.trackSessionEnd(); 
   
   ........ 
   ........ 
   ```

* **iOS** iOS でこのシナリオを表示するには、以下のコードを設定します。

   ```
   //  Set up mediaObject 
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                        length:MEDIA_LENGTH  
                        streamType:ADBMediaHeartbeatStreamTypeVOD]; 
   
   NSMutableDictionary *videoContextData =  
     [[NSMutableDictionary alloc] init]; 
   [videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
   [videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
   
   // 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
   //    i.e., there is an intent to start playback. 
   [_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
   ....... 
   ....... 
   
   // Pre-roll 
   ADBMediaObject *adBreakInfo =  
     [ADBMediaHeartbeat createAdBreakObjectWithName:AD_BREAK_NAME  
                        position:AD_BREAK_POSITION  
                        startTime:AD_BREAK_START_TIME]; 
   ADBMediaObject *adInfo =  
     [ADBMediaHeartbeat createAdObjectWithName:AD_NAME  
                        adId:AD_ID  
                        position:AD_POSITION  
                        length:AD_LENGTH]; 
   
   // Context ad data 
   NSMutableDictionary *adDictionary =  
     [[NSMutableDictionary alloc] init]; 
   [adDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
   [adDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
   
   // 2. Track the ADBMediaHeartbeatEventAdBreakStart event when the  
   //    pre-roll pod starts to play. Note that since this is a pre-roll,  
   //    you must track the ADBMediaHeartbeatEventAdBreakStart event  
   //    before you call trackPlay. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                    mediaObject:adBreakObject  
                    data:adDictionary]; 
   ....... 
   ....... 
   
   // 3. Track the ADBMediaHeartbeatEventAdStart when the pre-roll  
   //    pod's ad starts to play. Note that since this is a pre-roll,  
   //    you must track the ADBMediaHeartbeatEventAdStart before you 
   //    call trackPlay. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                     mediaObject:adObject  
                     data:adDictionary]; 
   ....... 
   ....... 
   
   // 4. Call trackPlay when the playback actually starts, i.e., when 
   //    the first frame of the main content is rendered on the screen. 
   [_mediaHeartbeat trackPlay]; 
   ....... 
   ....... 
   
   // 5. Track the ADBMediaHeartbeatEventAdComplete event when the ad  
   //    reaches the end, i.e., when it completes and finishes playing. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                     mediaObject:nil  
                     data:nil]; 
   ....... 
   ....... 
   
   // 6. Track the ADBMediaHeartbeatEventAdBreakComplete event when all  
   //    of the ads in the pod finish playing. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                     mediaObject:nil  
                     data:nil]; 
   ....... 
   ....... 
   
   // Mid-roll 
   ADBMediaObject *adBreakInfo =  
     [ADBMediaHeartbeat createAdBreakObjectWithName:MIDROLL_BREAK_NAME  
                        position:MIDROLL_BREAK_POSITION  
                        startTime:MIDROLL_BREAK_START_TIME]; 
   ADBMediaObject *adInfo =  
     [ADBMediaHeartbeat createAdObjectWithName:MIDROLL_AD_NAME  
                        adId:MIDROLL_AD_ID position:MIDROLL_AD_POSITION  
                        length:MIDROLL_AD_LENGTH]; 
   
   // context ad data 
   NSMutableDictionary *midrollAdDictionary = [[NSMutableDictionary alloc] init]; 
   [midrollAdDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
   [midrollAdDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
   
   // 7. Track the ADBMediaHeartbeatEventAdBreakStart event when the mid-roll pod  
   //    starts to play. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                     mediaObject:adBreakObject  
                     data:nil]; 
   ....... 
   ....... 
   
   // 8. Track the ADBMediaHeartbeatEventAdStart event when the mid-roll pod's  
   //    ad starts to play. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                    mediaObject:adObject  
                    data:midrollAdDictionary]; 
   ....... 
   ....... 
   
   // 9. Track the ADBMediaHeartbeatEventAdComplete event when the ad reaches  
   //    the end, i.e., when it completes and finishes playing. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                    mediaObject:nil  
                    data:nil]; 
   ....... 
   ....... 
   
   // 10. Track the ADBMediaHeartbeatEventAdBreakComplete event when all the  
   //     ads in the mid-roll pod finish playing. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                    mediaObject:nil  
                    data:nil]; 
   ....... 
   ....... 
   
   // Post-roll 
   ADBMediaObject *postrollBreakInfo =  
     [ADBMediaHeartbeat createAdBreakObjectWithName:POSTROLL_BREAK_NAME  
                        position:POSTROLL_BREAK_POSITION  
                        startTime:POSTROLL_BREAK_START_TIME]; 
   ADBMediaObject *adInfo =  
     [ADBMediaHeartbeat createAdObjectWithName:POSTROLL_AD_NAME  
                        adId:POSTROLL_AD_ID  
                        position:POSTROLL_AD_POSITION  
                        length:POSTROLL_AD_LENGTH]; 
   
   // Context ad data 
   NSMutableDictionary *postrollAdDictionary =  
     [[NSMutableDictionary alloc] init]; 
   [postrollAdDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
   [postrollAdDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
   
   // 11. Track the ADBMediaHeartbeatEventAdBreakStart event when the  
   //     post-roll pod starts to play. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                    mediaObject:adBreakObject  
                    data:nil]; 
   ....... 
   ....... 
   
   // 12. Track the ADBMediaHeartbeatEventAdStart event when the  
   //     post-roll pod's ad starts to play. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                    mediaObject:adObject  
                    data:postrollAdDictionary]; 
   ....... 
   ....... 
   
   // 13. Track the ADBMediaHeartbeatEventAdComplete event when the  
   //     post-roll pod's ad finishes playing. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                    mediaObject:nil  
                    data:nil]; 
   ....... 
   ....... 
   
   // 14. Track the ADBMediaHeartbeatEventAdBreakComplete event when  
   //     all the ads in the post-roll pod finish playing. 
   [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                    mediaObject:nil data:nil]; 
   ....... 
   ....... 
   
   // 15. Call trackComplete when the playback reaches the end,  
   //     i.e., when the video completes and finishes playing. 
   [_mediaHeartbeat trackComplete]; 
   ....... 
   ....... 
   
   // 16. Call trackSessionEnd when the playback session is over. This method  
   //     must be called even if the user does not watch the video to completion. 
   [_mediaHeartbeat trackSessionEnd]; 
   ....... 
   ....... 
   ```

* **JavaScript** JavaScript でこのシナリオを表示するには、以下のテキストを入力します。

   ```js
   // Set up mediaObject 
   MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
       Configuration.MEDIA_NAME,  
       Configuration.MEDIA_ID,  
       Configuration.MEDIA_LENGTH,  
       MediaHeartbeat.StreamType.VOD 
   ); 
   
   var videoMetadata = { 
       CUSTOM_KEY_1 : CUSTOM_VAL_1,  
       CUSTOM_KEY_2 : CUSTOM_VAL_2,  
       CUSTOM_KEY_3 : CUSTOM_VAL_ 
   }; 
   
   // 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
   //    i.e., when there's an intent to start playback.  
   this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
   
   ...... 
   ...... 
   
   // Preroll 
   var adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
                                        ADBREAK_POSITION,  
                                        ADBREAK_START_TIME); 
   var adInfo =  
     MediaHeartbeat.createAdObject(AD_NAME,  
                                   AD_ID,  
                                   AD_POSITION,  
                                   AD_LENGTH); 
   
   // Custom ad metadata 
   var adMetadata = { 
       CUSTOM_KEY_1 : CUSTOM_VAL_1,  
       CUSTOM_KEY_2 : CUSTOM_VAL_2 
   
   }; 
   
   // 2. Track the MediaHeartbeat.Event.AdBreakStart event when the preroll pod  
   //    starts to play. Note that since this is a preroll, you must track the  
   //    MediaHeartbeat.Event.AdBreakStart event before you call trackPlay().  
   this._trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
   
   ....... 
   ....... 
   
   // 3. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's ad  
   //    starts to play. Note that since this is a preroll, you must track the 
   //    MediaHeartbeat.Event.AdStart event before you call trackPlay().  
   this._heartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 4. Call trackPlay() when the main content actually starts, i.e., when the  
   //    first frame of the video content is rendered on the screen.  
   this._mediaHeartbeat.trackPlay(); 
   
   ....... 
   ....... 
   
   // 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches the end,  
   //    i.e., when the ad completes and finishes playing. 
   this._heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   
   ....... 
   ....... 
   
   // 6. Track the MediaHeartbeat.Event.AdBreakComplete event when all of the ads in  
   //    the pod finish playing. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
   
   ....... 
   ....... 
   
   // Midroll 
   var adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(MIDROLL_BREAK_NAME,  
                                        MIDROLL_BREAK_POSITION,  
                                        MIDROLL_BREAK_START_TIME); 
   var adInfo =  
     MediaHeartbeat.createAdObject(MIDROLL_AD_NAME,  
                                   MIDROLL_AD_ID, 
                                   MIDROLL_AD_POSITION,  
                                   MIDROLL_AD_LENGTH); 
   
   // Custom ad metadata 
   var adMetadata = { 
       CUSTOM_KEY_1 : CUSTOM_VAL_1,  
       CUSTOM_KEY_2 : CUSTOM_VAL_2 
   
   }; 
   
   // 7. Track the MediaHeartbeat.Event.AdBreakStart event when the  
   //    midroll pod starts to play. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
   
   ....... 
   ....... 
   
   // 8. Track the MediaHeartbeat.Event.AdStart event when the midroll  
   //    pod's ad starts to play. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                   adInfo,  
                                   adMetadata); 
   
   ....... 
   ....... 
   
   // 9. Track the MediaHeartbeat.Event.AdComplete event when the ad  
   //    reaches the end, i.e., when the ad completes and finishes playing.  
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
   
   ....... 
   ....... 
   
   // 10. Track the MediaHeartbeat.Event.AdBreakComplete event when all of  
   //     the ads in the midroll pod finish playing. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
   
   ....... 
   ....... 
   
   // Set up mediaObject 
   var mediaInfo = MediaHeartbeat.createMediaObject( 
       Configuration.MEDIA_NAME,  
       Configuration.MEDIA_ID,  
       Configuration.MEDIA_LENGTH,  
       MediaHeartbeat.StreamType.VOD 
   
   ); 
   
   var videoMetadata = { 
       CUSTOM_KEY_1 : CUSTOM_VAL_1,  
       CUSTOM_KEY_2 : CUSTOM_VAL_2,  
       CUSTOM_KEY_3 : CUSTOM_VAL_3 
   
   }; 
   
   // 1. Call trackSessionStart() when Play is clicked or if autoplay  
   //    is used, i.e., when there's an intent to start playback. 
   this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
   
   ...... 
   ...... 
   
   // Preroll 
   var adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
                                        ADBREAK_POSITION,  
                                        ADBREAK_START_TIME); 
   var adInfo =  
     MediaHeartbeat.createAdObject(AD_NAME,  
                                   AD_ID,  
                                   AD_POSITION,  
                                   AD_LENGTH); 
   
   // Custom ad metadata 
   var adMetadata = { 
      CUSTOM_KEY_1 : CUSTOM_VAL_1,  
      CUSTOM_KEY_2 : CUSTOM_VAL_2 
   
   }; 
   
   // 2. Track the MediaHeartbeat.Event.AdBreakStart event when the preroll pod  
   //    starts to play. Note that since this is a preroll, you must track the   
   //    MediaHeartbeat.Event.AdBreakStart event before you call trackPlay(). 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
   
   ....... 
   ....... 
   
   // 3. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's  
   //    ad starts to play. Note that since this is a preroll, you must track   
   //    the MediaHeartbeat.Event.AdStart event before you call trackPlay(). 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 4. Call trackPlay() when the playback actually starts, i.e., when the first  
   //    frame of the main content is rendered on the screen.  
   _mediaHeartbeat.trackPlay(); 
   
   ....... 
   ....... 
   
   // 5. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches  
   //    the end, i.e., when the ad completes and finishes playing. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
   
   ....... 
   ....... 
   
   // 6. Track the MediaHeartbeat.Event.AdBreakComplete event when all  
   //    of the ads in the pod finish playing. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
   
   ....... 
   ....... 
   
   // Mid-roll 
   var adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(MIDROLL_BREAK_NAME, 
                                        MIDROLL_BREAK_POSITION,  
                                        MIDROLL_BREAK_START_TIME); 
   var adInfo =  
     MediaHeartbeat.createAdObject(MIDROLL_AD_NAME,  
                                   MIDROLL_AD_ID,  
                                   MIDROLL_AD_POSITION,  
                                   MIDROLL_AD_LENGTH); 
   
   // Custom ad metadata 
   var adMetadata = { 
      CUSTOM_KEY_1 : CUSTOM_VAL_1,  
      CUSTOM_KEY_2 : CUSTOM_VAL_2 
   
   }; 
   
   // 7. Track the MediaHeartbeat.Event.AdBreakStart event when the midroll  
   //    pod starts to play. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
   
   ....... 
   ....... 
   
   // 8. Track the MediaHeartbeat.Event.AdStart event when the midroll pod's  
   //    ad starts to play. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 9. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches  
   //    the end, i.e., when the ad completes and finishes playing. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
   
   ....... 
   ....... 
   
   // 10. Track the MediaHeartbeat.Event.AdBreakComplete event when all  
   //     of the ads in the midroll pod finish playing. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
   
   ....... 
   ....... 
   
   // Postroll 
   var adBreakInfo = MediaHeartbeat.createAdBreakObject(POSTROLL_BREAK_NAME,  
   POSTROLL_BREAK_POSITION, POSTROLL_BREAK_START_TIME); 
   var adInfo = MediaHeartbeat.createAdObject(POSTROLL_AD_NAME, POSTROLL_AD_ID,  
   POSTROLL_AD_POSITION, POSTROLL_AD_LENGTH); 
   
   // Custom ad metadata 
   var adMetadata = { 
      CUSTOM_KEY_1 : CUSTOM_VAL_1,  
      CUSTOM_KEY_2 : CUSTOM_VAL_2 
   
   }; 
   
   // 11. Track the MediaHeartbeat.Event.AdBreakStart event when the postroll  
   //     pod starts to play. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
   
   ....... 
   ....... 
   
   // 12. Track the MediaHeartbeat.Event.AdStart event when the postroll pod's ad  
   //     starts to play. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
   
   ....... 
   ....... 
   
   // 13. Track the MediaHeartbeat.Event.AdComplete event when the ad reaches   
   //     the end, i.e., when the ad completes and finishes playing. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
   
   ....... 
   ....... 
   
   // 14. Track the MediaHeartbeat.Event.AdBreakComplete event when all of  
   //     the ads in the postroll pod finish playing. 
   this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
   
   ....... 
   ....... 
   
   // 15. Call trackComplete() when the playback reaches the end, i.e., when playback 
   //     completes and finishes playing. 
   this._mediaHeartbeat.trackComplete(); 
   
   ........ 
   ........ 
   
   // 16. Call trackSessionEnd() when the playback session is over. This method must be called  
   //     even if the user does 
   not watch the video to completion. 
   this._mediaHeartbeat.trackSessionEnd(); 
   
   ........ 
   ........ 
   ```
