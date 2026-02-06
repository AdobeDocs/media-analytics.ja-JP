---
title: Android で標準広告メタデータを実装する方法
description: Android 上の広告トラッキングでの標準広告メタデータの使用方法です。
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 93%

---

# Android での標準広告メタデータの実装 {#implement-standard-ad-metadata-on-android}

## 広告定数

| 定数名 | 説明   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | 標準広告メタデータを Ad `MediaObject` にアタッチするための定数。 |

## 標準広告メタデータの実装

標準広告メタデータの場合、ご利用のプラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```
