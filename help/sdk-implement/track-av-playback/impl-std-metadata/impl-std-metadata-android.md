---
title: Android での標準メタデータの実装
description: Androidでトラッキングコールと共に送信される標準ビデオおよび広告メタデータの設定について説明します。
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Android での標準メタデータの実装{#implement-standard-metadata-on-android}

## 標準メタデータ定数

| 定数名 | 説明   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | 標準メタデータを `MediaObject` にアタッチするための定数。 |

## メタデータキーAPIリファレンス

* 標準メタデータ `HashMap` のキーと値のペアの作成。
   * [ビデオメタデータキー](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [オーディオメタデータキー](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* メタデータの標準メタデータ定数を使用して、`HashMap` に標準メタデータ `MediaInfo` を設定します。
* Provide this `MediaInfo` object while invoking the `trackSessionStart()` API.

## 実装例

### ビデオ

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### Audio

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```
