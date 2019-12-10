---
title: iOS での標準メタデータの実装
description: iOS 上で、標準ビデオおよび広告メタデータがトラッキングコールで送信されるようにする設定を説明します。
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# iOS での標準メタデータの実装 {#implement-standard-metadata-on-ios}

## メタデータ定数

| 定数名 | 説明   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | 標準メタデータを `MediaInfo ADBMediaObject` にアタッチするための定数。 |

## 実装

1. `ADBStandardMetadataKeys` を使用して、標準メタデータのキーと値のペアのディクショナリを作成します。
   [IOS のメタデータキー](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. メタデータの標準メタデータ定数を使用して、`MediaInfo``ADBMediaObject` インスタンスに標準メタデータディクショナリを設定します。

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

