---
title: ライブメインコンテンツ
description: Media SDKを使用してライブコンテンツを追跡する方法の例です。
uuid: e92e99f4-c395-48aa-8a30-cbd2f5fc07c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# ライブメインコンテンツ{#live-main-content}

## シナリオ {#scenario}

このシナリオでは、ライブストリームに参加後、40 秒間広告が再生されていない、1 つのライブアセットがあります。

| トリガー | ハートビートメソッド | ネットワーク呼び出し | メモ   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Analytics Content Start、Heartbeat Content Start | これは、**[!UICONTROL 再生]をクリックするユーザーか、自動再生イベントである可能性があります。** |
| メディア再生の最初のフレーム。 | `trackPlay` | Heartbeat Content Play | このメソッドは、タイマーをトリガーします。ハートビートは、再生が続く限り、10 秒ごとに送信されます。 |
| コンテンツが再生される。 |  | Content Heartbeats |  |
| セッションが終了する。 | `trackSessionEnd` |  | `SessionEnd` は、表示セッションの終端を意味します。このAPIは、ユーザーがメディアを消費せずに完了する場合でも呼び出す必要があります。 |

## パラメーター {#parameters}

Adobe Analytics Content Start 呼び出し時に確認される同じ値の多くは、Heartbeat Content Start 呼び出し時にも確認されます。また、Adobe Analyticsの様々なメディアレポートに入力するためにアドビが使用するその他のパラメーターの多くも確認できます。 ここではすべては取り上げません。本当に重要なものだけを示します。

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
| `s:meta:*` | オプション | メディア上のカスタムメタデータセット |

## Content Heartbeats {#content-heartbeats}

メディアの再生中に、1つ以上のハートビート(ping)を、メインコンテンツに10秒ごと、広告に1秒ごとに送信するタイマーがあります。 それらのハートビートには、再生、広告、バッファーおよびその他多くに関する情報が含まれます。各ハートビートの厳密なコンテンツは、このドキュメントの範囲外であり、検証に重要なことは、ハートビートは、再生が続く間、常にトリガーされるということです。

Content Heartbeats では、いくつかの特定の事柄を探します。

| パラメーター | 値 | メモ |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;再生ヘッドの位置&gt; 例：50、60、70 | これは、再生ヘッドの現在の位置を反映する必要があります。 |

## Heartbeat Content Complete {#heartbeat-content-complete}

このシナリオでは、ライブストリームが完了しなかったので、完了呼び出しは行われません。

## 再生ヘッドの値の設定

LIVEストリームの場合は、プログラミング開始時からのオフセットに再生ヘッドを設定する必要があります。これにより、レポートで、アナリストは、ユーザーが24時間ビュー内でLIVEストリームに参加して離脱する時点を判断できます。

### 開始時

LIVEメディアの場合、ユーザーがストリームの再生を開始するときに、現在のオフセットを秒 `l:event:playhead` 単位で設定する必要があります。 これは、再生ヘッドを「0」に設定するVODとは異なります。

例えば、LIVEストリーミングイベントが午前0時に開始し、24時間(`a.media.length=86400`; `l:asset:length=86400`)。 次に、ユーザーが午後12時にそのLIVEストリームの再生を開始したとします。 このシナリオでは、43200(ストリ `l:event:playhead` ームが開始してから12時間)に設定する必要があります。

### 一時停止時

再生を一時停止したときに、再生の開始時に適用したのと同じ「ライブ再生ヘッド」ロジックを適用する必要があります。 ユーザーがLIVEストリームの再生に戻ったら、ユーザーがLIVEストリームを一時停止したポイントではなく、新しいオフセット再生ヘッ `l:event:playhead` ド __ （位置）に値を設定する必要があります。

## サンプルコード {#sample-code}

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

