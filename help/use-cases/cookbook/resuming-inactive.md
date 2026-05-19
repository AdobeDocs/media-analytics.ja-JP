---
title: 非アクティブなセッションの再開
description: 非アクティブなセッションの再開を処理する方法を説明します。
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/KT7NfrYlagrMwAjsrbSNR8YUbj5d-ihU8AfJ6wcbgOA
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 38%

---

# 非アクティブなセッションの再開{#resuming-inactive-sessions}

## 長時間の一時停止

メディア SDK は、メディア再生が以下のいずれかの非アクティブな状態である時間を自動的に追跡します。

* 一時停止
* シーク
* Stalled
* バッファリング

メディアトラッキングセッションが 30 分以上非アクティブな状態のままの場合、セッションは自動的に閉じられます。 以前非アクティブになったビデオトラッキングセッションの後にユーザーが再開（`trackPlay`）した場合、メディアハートビートは、以前使用したビデオ情報およびメタデータを使用して新しいビデオセッションを自動的に作成し、再開ハートビートイベントを送信します。

## 再開フラグを使用したクロスデバイスのハンドオフ

シングルアプリセッションの継続を処理する同じ再開メカニズムは、視聴者がデバイス間で再生を転送する場合（携帯電話からテレビやChromecast受信機へのビデオのキャストなど）にも適用されます。 各デバイスは独自のMedia SDK インスタンスを実行するため、デフォルトでは複数のセッションが作成されます。 再開フラグを使用して、それらを論理的な連続性に結合し、Analyticsが個別のメディアの開始ではなく、単一のエンゲージメントとして結合された表示をレポートするようにします。

**実装方法：**

1. **ソースデバイス** （電話など）で、ビューアがキャストを開始したときに`trackSessionEnd`に電話します。 `trackComplete`を呼び出さないでください。コンテンツは完了していません。別のデバイスに移動中です。
2. **宛先デバイス** （例：Chromecast）で、再開フラグを`true`に設定し、ソースデバイスで使用されているのと同じコンテンツメタデータ（名前、ID、長さ）で`trackSessionStart`を呼び出します。 ソースデバイスでビューアが中断した位置に再生ヘッドの位置を渡します。
3. ビューアが後でソースデバイスに再生を返す場合は、宛先で同じパターン `trackSessionEnd`を繰り返し、ソースで再開フラグを使用して`trackSessionStart`を繰り返します。

再開フラグを設定すると、Adobe Analyticsは、ハンドオフの2番目以降のレッグに対して[Media starts](/help/reporting/metrics/media-starts.md)ではなく[Content resumes](/help/reporting/metrics/content-resumes.md)を増分します。 SDK インスタンス間でセッション IDを共有する組み込みメカニズムはないので、再開フラグはクライアントサイドの宣言です。ビューアが以前のセッションを続けていることがわかっている場合は、アプリケーションロジックに基づいて渡します。

## 以前終了したセッションの手動での再開

メディア SDK は、アプリケーションが閉じられていない場合、自動でのみ再開します。 アプリケーションがユーザーデータを格納し、以前閉じたメディアを再開する機能がある場合、再開イベントを手動でトリガーできます。 ビデオトラッキングセッションを開始するときに、オプションのビデオ再開プロパティを設定します。

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
