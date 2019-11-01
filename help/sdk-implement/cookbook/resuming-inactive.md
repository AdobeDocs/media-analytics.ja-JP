---
title: 非アクティブなセッションの再開
description: 非アクティブなセッションの再開の処理方法。
uuid: 3ff1205d-7be-4016-9bd7-6e34b7862c4c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 非アクティブなセッションの再開{#resuming-inactive-sessions}

## 長時間の一時停止

Media SDKは、次の非アクティブ状態のいずれかのメディア再生がどれだけの時間あるかを自動的に追跡します。

* 一時停止
* シーク
* 停止
* バッファー

メディアトラッキングセッションが30分以上非アクティブな状態のままの場合、セッションは自動的に閉じられます。 以前非アクティブになったビデオトラッキングセッションの後にユーザーが再開（`trackPlay`）した場合、メディアハートビートは、以前使用したビデオ情報およびメタデータを使用して新しいビデオセッションを自動的に作成し、再開ハートビートイベントを送信します。For more information, see [Audio and video parameters.](/help/metrics-and-metadata/audio-video-parameters.md)

## 以前終了したセッションの手動での再開

Media SDKは、アプリケーションが閉じられていない場合にのみ、セッションを自動的に再開します。 アプリケーションがユーザーデータを保存し、以前閉じたメディアを再開する機能を持つ場合は、再開イベントを手動でトリガーできます。 ビデオトラッキングセッションを開始するときに、オプションのビデオ再開プロパティを設定します。

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true 
public void onmediaLoad(Observable observable, Object data) { 

  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Set to true if this is a resume playback scenario 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);
   
  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification { 
  //Replace <MEDIA_NAME> with the media name. 
  //Replace <MEDIA_ID> with a media unique identifier. 
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                       mediaId:<MEDIA_ID> 
                       length:<MEDIA_LENGTH> 
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 

  //Set to YES if this user is resuming a previously closed media session 
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata]; 
} 
```

### JavaScript

```js
_onmediaLoad = function () { 
  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session 
  mediaObject.setValue(MediaObjectKey.mediaResumed, true); 
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
};
```

