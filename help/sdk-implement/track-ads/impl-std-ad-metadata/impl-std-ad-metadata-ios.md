---
title: iOS での標準広告メタデータの実装
description: iOSでの広告追跡で標準広告メタデータを使用する方法。
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# iOS での標準広告メタデータの実装{#implement-standard-ad-metadata-on-ios}

## 広告定数

| 定数名 | 説明   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## 実装標準広告メタデータ

標準広告メタデータの場合、プラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS のメタデータキー](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
