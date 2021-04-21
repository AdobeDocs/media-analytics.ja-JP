---
title: JavaScript2.x を使用した標準広告メタデータの実装
description: JavaScript 2.x アプリを使用するブラウザーで標準広告メタデータを広告トラッキングに使用する方法。
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
exl-id: b331db87-ab4e-44fa-a97c-9691974cacd4
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '68'
ht-degree: 100%

---

# JavaScript 2.x を使用した標準広告メタデータの実装 {#implement-standard-ad-metadata-on-javascript}

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
