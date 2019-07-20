---
description: 'null'
seo-description: 'null'
seo-title: Roku での標準メタデータの実装
title: Roku での標準メタデータの実装
uuid: ae14d809-343f-452c-832a- f94bd3d83a90
translation-type: tm+mt
source-git-commit: c6c7afee72d21c832be77c723750ae0551793613

---


# Roku での標準メタデータの実装{#implement-standard-metadata-on-roku}

標準メタデータオブジェクトをインスタンス化し、必要な変数を設定して、メディアハートビートオブジェクトでメタデータオブジェクトを設定します。

**Video:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

**Audio:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

ビデオメタデータの包括的なリストについては、[オーディオおよびビデオパラメーター](../../../metrics-and-metadata/audio-video-parameters.md)を参照してください。

