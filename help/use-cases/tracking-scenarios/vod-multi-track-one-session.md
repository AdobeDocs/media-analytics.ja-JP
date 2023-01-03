---
title: 複数のセッションに対応する 1 つの VOD トラッカー
description: Media SDK を使用して 1 つのトラッカーで複数のセッションをトラッキングする方法の例を示します。
uuid: 355c83f4-52bd-4bdd-92dc-ab506e412d0a
exl-id: 72edb484-0d45-446e-bda3-cda9e2272e7e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '184'
ht-degree: 100%

---

# 複数のセッションに対応する 1 つの VOD トラッカー{#vod-one-tracker-for-multiple-sessions}

## シナリオ {#scenario}

このシナリオでは、`MediaHeartbeat` インスタンスを使用して 2 つの異なるセッションを順に作成します。

このシナリオは、[広告のない VOD 再生](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)シナリオと同じです。

## パラメーター {#parameters}

### ハートビートセッション

| パラメーター | 値 | メモ   |
| --- | --- | --- |
| `s:event:sid` | 一意のセッション ID | `trackSessionEnd` が呼び出されるまで、すべてのハートビートネットワーク呼び出しに存在する一意のセッション ID。 |

## サンプルコード {#sample-code}

![](assets/multi-sessions-one-at-a-time.png)

### Android {#android}

2 つのメディアプレーヤー用に `MediaHeartbeat` の 2 つのインスタンスを作成するには、以下のコードを設定します。

```java
public class MediaAnalyticsProvider implements MediaHeartbeatDelegate { 

  private MediaPlayer _player; 
  private MediaHeartbeat _heartbeat; 

  public MediaAnalyticsProvider(MediaPlayer player) { 
      if (player == null) { 
          throw new IllegalArgumentException("Player reference cannot be null."); 
      } 
  } 

  _player = player;  
  _player.addObserver(this); 

  // Media Heartbeat initialization 
  MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 

  config.trackingServer = HEARTBEAT_TRACKING_SERVER; 
  config.channel = HEARTBEAT_CHANNEL; 
  config.appVersion = HEARTBEAT_SDK; 
  config.ovp = HEARTBEAT_OVP; 
  config.playerName = PLAYER_NAME; 
  config.ssl = false; 
  config.debugLogging = true;  
  _heartbeat = new MediaHeartbeat(this, config); 
} 
```

```java
@Override 
public MediaObject getQoSObject() { 
  return MediaHeartbeat.createQoSObject(BITRATE, STARTUP_TIME, FPS, DROPPED_FRAMES); 
} 

@Override 
public Double getCurrentPlaybackTime() { 
  return _player.getCurrentPlaybackTime(); 
} 
```

```java
@Override 
protected void onCreate(Bundle savedInstanceState) { 
  super.onCreate(savedInstanceState); 
  setContentView(R.layout.activity_main); 

  // Bootstrap the AppMeasurement library.  
  Config.setContext(this.getApplicationContext()); 

  // Create the MediaPlayer instance.  
  _player = new MediaPlayer(); 

  // Create the MediaAnalyticsProvider instance and 
  // attach it to the MediaPlayer instance.  
   _analyticsProvider = new MediaAnalyticsProvider(_player); 

  // Load the main media content.  
   Uri uri = Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.media1);  
   _player.loadContent(uri); 
} 
```

Android で `MediaAnalyticsProvider`（つまり `MediaHeartbeat`）インスタンスを使用して最初のセッションを表示するには、以下のコードを設定します。

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
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

// 3. Call trackComplete() when the playback reaches the end, i.e., when the 
//    media completes and finishes playing. 
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over. This method must  
//    be called even if the user does not watch the media to completion.  
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

2 番目のセッションを表示するには、新しいセッションであることを別にすれば、最初のセッションと同じ `MediaAnalyticsProvider`（`MediaHeartbeat`）インスタンスを使用できます。

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
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

// 3. Call trackComplete() when the playback reaches the end, i.e., when the  
//    media completes and finishes playing. 
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over. This method  
//    must be called even if the user does not watch the media to completion.  
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

### iOS {#ios}

2 つのメディアプレーヤー用に `MediaHeartbeat` の 2 つのインスタンスを作成するには、以下を入力します。

```
@interface MediaAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 

@end    

@implementation { 
  MediaPlayer *_player; 
} 

- (instancetype)initWithPlayer:(AVPlayer *)player { 
  if (self = [super init]) { 
      _player = player; 

      ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
      config.trackingServer = HEARTBEAT_TRACKING_SERVER; 
      config.channel = HEARTBEAT_CHANNEL; 
      config.appVersion = HEARTBEAT_SDK_VERSION; 
      config.playerName = PLAYER_NAME; 
      config.ssl = SSL_SETTING; 
      config.debugLogging = DEBUG_SETTING; 

      ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];       
      _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
        
      [self setupPlayerNotifications]; 
  } 

  return self; 
} 

- (ADBMediaObject *)getQoSInfo { 
  return [ADBMediaHeartbeat createQoSObjectWithBitrate:CURRENT_BITRATE_VALUE  
                            startupTime:CALCULATED_STARTED_TIME  
                            fps:CALCULATED_FPS  
                            droppedFrames:DROPPED_FRAMES_COUNT]; 
} 

- (NSTimeInterval)getCurrentPlaybackTime { 
  return CMTimeGetSeconds(_player.currentTime); 
} 

@end 
```

```
- (void)viewDidAppear:(BOOL)animated { 
  [super viewDidAppear:animated]; 
  [ADBMobile setDebugLogging:YES]; 

  // Setup the first media player 
  NSURL *streamUrl = [NSURL URLWithString:CONTENT_URL]; 

  if (!self.mediaPlayer) { 
      self.mediaPlayer = [[MediaPlayer alloc] initWithContentURL:streamUrl]; 
      //setup player 
  } 

  // Create the MediaAnalyticsProvider instance and attach it to the first  
  // MediaPlayer instance. 
  if (!self.mediaAnalyticsProvider) { 
      self.mediaAnalyticsProvider =  
        [[MediaAnalyticsProvider alloc] initWithPlayerDelegate:self.mediaPlayer]; 
  } 
} 
```

iOS で `MediaAnalyticsProvider`（つまり `MediaHeartbeat`）インスタンスを使用して最初のセッションを表示するには、以下のコードを設定します。

```
// Set up mediaObject 
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
....... 
....... 
 
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackComplete when the playback reaches the end, i.e., when the 
//    media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 
  
// 4. Call trackSessionEnd when the playback session is over. This method  
//    must be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
....... 
....... 
```

2 番目のセッションを表示するには、新しいセッションであることを別にすれば、最初のセッションと同じ `MediaAnalyticsProvider`（`MediaHeartbeat`）インスタンスを使用できます。

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 
   
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
  
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
....... 
....... 
 
// 2. Call trackPlay when the playback actually starts, i.e. when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackComplete when the playback reaches the end, i.e., when the 
//    media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 
  
// 4. Call trackSessionEnd when the playback session is over. This method  
//    must be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
....... 
....... 
```

### JavaScript {#javascript}

```js
var MediaHeartbeat = ADB.va.MediaHeartbeat; 
var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 

function MediaAnalyticsProvider(player) { 
  if (!player) { 
      throw new Error("Illegal argument. Player reference cannot be null.") 
  }   
  this._player = player; 

  // Media Heartbeat initialization 
  var mediaConfig = new MediaHeartbeatConfig(); 
  mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
  mediaConfig.playerName = Configuration.PLAYER.NAME; 
  mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
  mediaConfig.debugLogging = true; 
  mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
  mediaConfig.ssl = false; 
  mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 

  var mediaDelegate = new MediaHeartbeatDelegate(); 

  mediaDelegate.getCurrentPlaybackTime = function() { 
      return player.getCurrentPlaybackTime(); 
  }; 

  mediaDelegate.prototype.getQoSObject = function() { 
      return player.getQoSInfo(); 
  }; 

  this._mediaHeartbeat =  
    new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
} 
```

```js
// Create the first MediaPlayer instance.  
var _player1 = new MediaPlayer(); 

// Create the first MediaAnalyticsProvider instance and 
// attach it to the MediaPlayer instance.  
analyticsProvider1 = new MediaAnalyticsProvider(_player1); 

// Load the main media content.  
_player1.loadContent(URL_TO_MEDIA_1);
```
