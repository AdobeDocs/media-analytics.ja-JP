---
title: iOSでの標準メタデータの実装方法を説明します。
description: iOS上で、標準ビデオおよび広告メタデータがトラッキングコールで送信されるように設定する方法を説明します。
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 75%

---

# iOS での標準メタデータの実装{#implement-standard-metadata-on-ios}

## メタデータ定数

| 定数名 | 説明   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | 標準メタデータを `MediaInfo ADBMediaObject` にアタッチするための定数。 |

## 実装

1. `ADBStandardMetadataKeys` を使用して、標準メタデータのキーと値のペアのディクショナリを作成します。
   [IOS のメタデータキー](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. メタデータの標準メタデータ定数を使用して、`MediaInfo` `ADBMediaObject` インスタンスに標準メタデータディクショナリを設定します。

1. `trackSessionStart` API を呼び出すと同時に、この `MediaInfo` オブジェクトを提供します。

### 実装例

標準メタデータオブジェクトをインスタンス化し、必要な変数を設定して、メディアハートビートオブジェクトでメタデータオブジェクトを設定します。例：

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```
