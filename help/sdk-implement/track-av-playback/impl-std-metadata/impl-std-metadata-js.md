---
description: 'null'
seo-description: 'null'
seo-title: JavaScript での標準メタデータの実装
title: JavaScript での標準メタデータの実装
uuid: 523d29e3-0a62-40d7- ac74- da645024cdcb
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# JavaScript での標準メタデータの実装{#implement-standard-metadata-on-javascript}

## メタデータ定数

| 定数名 | 説明   |
| --- | --- |
| `StandardMediaMetadata` | Constant for attaching standard metadata on `MediaObject` |

## 実装

標準メタデータオブジェクトをインスタンス化し、必要な変数を設定して、メディアハートビートオブジェクトでメタデータオブジェクトを設定します。次に例を示します。

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

