---
title: Roku で標準メタデータを実装する方法
description: Roku で標準ビデオメタデータや標準広告メタデータをトラッキングコールで送信するように設定する方法を説明します。
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 69%

---

# Roku での標準メタデータの実装 {#implement-standard-metadata-on-roku}

標準メタデータオブジェクトをインスタンス化し、必要な変数を設定して、Media Heartbeat オブジェクトにメタデータオブジェクトを設定します。

**ビデオ:**

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

ビデオメタデータの包括的なリストについては、[オーディオおよびビデオパラメーター](/help/implementation/variables/audio-video-parameters.md)を参照してください。
