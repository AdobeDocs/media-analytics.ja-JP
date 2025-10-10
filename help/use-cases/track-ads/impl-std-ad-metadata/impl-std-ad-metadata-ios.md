---
title: iOS で標準広告メタデータを実装する方法
description: iOS 上の広告トラッキングでの標準広告メタデータの使用方法です。
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# iOS での標準広告メタデータの実装 {#implement-standard-ad-metadata-on-ios}

## 広告定数

| 定数名 | 説明   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | 標準広告メタデータを `AdInfo ADBMediaObject` にアタッチするための定数 |

## 標準広告メタデータの実装

標準広告メタデータの場合、ご利用のプラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS のメタデータキー](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
