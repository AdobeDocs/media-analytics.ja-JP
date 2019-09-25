---
description: 'null'
seo-description: 'null'
seo-title: Android での標準広告メタデータの実装
title: Android での標準広告メタデータの実装
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Android での標準広告メタデータの実装{#implement-standard-ad-metadata-on-android}

## 広告定数

| 定数名 | 説明   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | 標準広告メタデータを Ad `MediaObject` にアタッチするための定数。 |

## 実装標準広告メタデータ

標準広告メタデータの場合、プラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

