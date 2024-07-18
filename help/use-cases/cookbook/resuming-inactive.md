---
title: 非アクティブなセッションの再開
description: 非アクティブなセッションの再開を処理する方法を説明します。
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 100%

---

# 非アクティブなセッションの再開{#resuming-inactive-sessions}

## 長時間の一時停止

メディア SDK は、メディア再生が以下のいずれかの非アクティブな状態である時間を自動的に追跡します。

* 一時停止
* シーク
* Stalled
* バッファー

メディアトラッキングセッションが 30 分以上非アクティブな状態のままの場合、セッションは自動的に閉じられます。以前非アクティブになったビデオトラッキングセッションの後にユーザーが再開（`trackPlay`）した場合、メディアハートビートは、以前使用したビデオ情報およびメタデータを使用して新しいビデオセッションを自動的に作成し、再開ハートビートイベントを送信します。詳しくは、[オーディオおよびビデオパラメーター](/help/implementation/variables/audio-video-parameters.md)を参照してください。


## 以前終了したセッションの手動での再開

メディア SDK は、アプリケーションが閉じられていない場合、自動でのみ再開します。アプリケーションがユーザーデータを格納し、以前閉じたメディアを再開する機能がある場合、再開イベントを手動でトリガーできます。ビデオトラッキングセッションを開始するときに、オプションのビデオ再開プロパティを設定します。

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
