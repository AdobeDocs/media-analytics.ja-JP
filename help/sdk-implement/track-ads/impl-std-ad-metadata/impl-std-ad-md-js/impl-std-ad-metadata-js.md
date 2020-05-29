---
title: JavaScript 2.xを使用した標準広告メタデータの実装
description: JavaScript 2.xアプリを使用するブラウザーで、標準広告メタデータを広告追跡に使用する方法。
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 55%

---


# JavaScript 2.xを使用した標準広告メタデータの実装{#implement-standard-ad-metadata-on-javascript}

## 広告定数

| 定数名 | 説明   |
|---|---|
| `StandardAdMetadata` | 標準広告メタデータを広告オブジェクトにアタッチするための定数 |

## 標準広告メタデータの実装

標準広告メタデータの場合、ご利用のプラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>);

// Set standard Ad Metadata
var standardAdMetadata = {};
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```
