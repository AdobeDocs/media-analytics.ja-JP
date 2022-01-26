---
title: Android での標準メタデータの実装方法
description: Android で標準ビデオメタデータや標準広告メタデータをトラッキングコールで送信するように設定する方法を説明します。
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 100%

---

# Android での標準メタデータの実装{#implement-standard-metadata-on-android}

## 標準メタデータの定数

| 定数名 | 説明   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | 標準メタデータを `MediaObject` にアタッチするための定数。 |

## メタデータキー API リファレンス

* 標準メタデータのキーと値のペアの `HashMap` を作成します。
   * [ビデオのメタデータキー](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [オーディオのメタデータキー](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* メタデータの標準メタデータ定数を使用して、`HashMap` に標準メタデータ `MediaInfo` を設定します。
* `trackSessionStart()` API を呼び出すと同時に、この `MediaInfo` オブジェクトを提供します。

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
