---
seo-title: ライブメインコンテンツ
title: ライブメインコンテンツ
uuid: e92e99f4- c395-48aa-8a30- cbdd2f5fc07c
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# ライブメインコンテンツ{#live-main-content}

## シナリオ {#section_13BD203CBF7546D2A6AD0129B1EEB735}

このシナリオでは、ライブストリームに参加後、40 秒間広告が再生されていない、1 つのライブアセットがあります。

| トリガー | ハートビートメソッド | ネットワーク呼び出し | メモ   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Analytics Content Start、Heartbeat Content Start | これは、**[!UICONTROL 再生]をクリックするユーザーか、自動再生イベントである可能性があります。** |
| メディアの最初のフレームが再生されます。 | `trackPlay` | Heartbeat Content Play | このメソッドは、タイマーをトリガーします。ハートビートは、再生が続く限り、10 秒ごとに送信されます。 |
| コンテンツが再生される。 |  | Content Heartbeats |  |
| セッションが終了する。 | `trackSessionEnd` |  | `SessionEnd` は、表示セッションの終端を意味します。このAPIは、ユーザーがメディアを完了しない場合でも呼び出す必要があります。 |

## パラメーター {#section_D52B325B99DA42108EF560873907E02C}

Adobe Analytics Content Start 呼び出し時に確認される同じ値の多くは、Heartbeat Content Start 呼び出し時にも確認されます。Adobe Analyticsの様々なメディアレポートに入力するためにアドビが使用する他のパラメーターも多数表示されます。ここではすべては取り上げません。本当に重要なものだけを示します。

### Heartbeat Content Start

| パラメーター | 値 | メモ |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe レポートスイート ID&gt; |  |
| `s:sc:tracking_serve` | &lt;Analytics トラッキングサーバー URL&gt; |  |
| `s:user:mid` | `s:user:mid` | Adobe Analytics Content Start 呼び出しの mid 値と一致する必要がある |
| `s:event:type` | "start" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt;メディア名&gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | オプション | メディアに設定されたカスタムメタデータ |

## Content Heartbeats {#section_7B387303851A43E5993F937AE2B146FE}

メディアの再生中に、メインコンテンツの10秒ごと、および広告の1秒ごとに1つ以上のハートビート（ping）を送信するタイマーがあります。それらのハートビートには、再生、広告、バッファーおよびその他多くに関する情報が含まれます。各ハートビートの厳密なコンテンツは、このドキュメントの範囲外であり、検証に重要なことは、ハートビートは、再生が続く間、常にトリガーされるということです。

Content Heartbeats では、いくつかの特定の事柄を探します。

| パラメーター | 値 | メモ |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;再生ヘッドの位置&gt; 例：50、60、70 | これは、再生ヘッドの現在の位置を反映する必要があります。 |

## Heartbeat Content Complete {#section_2CA970213AF2457195901A93FC9D4D0D}

ライブストリームが完了していないので、このシナリオでは完全な呼び出しはありません。

## 再生ヘッドの値の設定

LIVEストリームの場合、プログラミングが開始された時点からのオフセットに再生ヘッドを設定する必要があります。これにより、レポートでは、ユーザーが24時間表示内でどの時点でライブストリームを結合して離脱するかを判断できます。

### 開始時

LIVEメディアの場合、ユーザーがストリームの再生を開始したときに、現在のオフセット `l:event:playhead` を秒単位で設定する必要があります。VODとは対照的に、再生ヘッドを"0"に設定します。

例えば、LIVEストリーミングイベントが午前0時から開始し、24時間（`a.media.length=86400`; `l:asset:length=86400`）を参照してください。その後、ユーザーが午後12時にLIVEストリームの再生を開始したとします。このシナリオでは、43200（ストリームの12時間） `l:event:playhead` に設定する必要があります。

### 一時停止時

再生開始時に適用される「ライブ再生ヘッド」ロジックは、ユーザーが再生を一時停止したときに適用する必要があります。ユーザーがLIVEストリームの再生に戻るとき、ユーザーがLIVEストリーム `l:event:playhead` を一時停止した時点で _はなく_ 、新しいオフセット再生ヘッド位置に値を設定する必要があります。

## サンプルコード {#section_vct_j2j_x2b}

![](assets/live-content-playback.png)

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
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
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
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

以下に、期待される API 呼び出し順序を示します。

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

