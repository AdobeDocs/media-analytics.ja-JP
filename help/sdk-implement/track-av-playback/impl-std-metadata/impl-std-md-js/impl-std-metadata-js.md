---
title: JavaScript 2.xを使用した標準メタデータの実装について説明します。
description: ブラウザーアプリ(JS 2.x)で、標準ビデオおよび広告メタデータがトラッキングコールで送信されるように設定する方法を説明します。
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
exl-id: 889c294b-ac45-4e82-abb3-88ab70abbc3d
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '69'
ht-degree: 59%

---

# JavaScript 2.x を使用した標準メタデータの実装{#implement-standard-metadata-on-javascript}

## メタデータ定数

| 定数名 | 説明   |
| --- | --- |
| `StandardMediaMetadata` | 標準メタデータを `MediaObject` にアタッチするための定数。 |

## 実装

標準メタデータオブジェクトをインスタンス化し、必要な変数を設定して、メディアハートビートオブジェクトでメタデータオブジェクトを設定します。例：

```js
_onVideoLoad = function () {
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                       <MEDIA_ID,  
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";

    //Set standard Audio Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label";

    mediaInfo.setValue(MediaObjectKey.StandardMediaMetadata, standardMediaMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```
