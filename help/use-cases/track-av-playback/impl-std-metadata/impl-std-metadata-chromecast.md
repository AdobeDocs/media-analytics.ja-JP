---
title: Chromecast で標準メタデータを実装する方法
description: Chromecast で標準ビデオメタデータや標準広告メタデータを設定する方法を説明します。
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
exl-id: 052ede4b-ea8a-4ca6-bf02-0aab22a8bcda
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# Chromecast での標準メタデータの実装{#implement-standard-metadata-on-chromecast}

標準メタデータオブジェクトをインスタンス化し、必要な変数を設定して、メディアハートビートオブジェクトでメタデータオブジェクトを設定します。次に例を示します。

```js
var standardVideoMetadata = {};
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show";
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season";

mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {};
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist";
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album";

mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

オーディオおよびビデオメタデータの包括的なリストについては、[オーディオおよびビデオパラメーター](/help/implementation/variables/audio-video-parameters.md)を参照してください。
