---
description: 'null'
seo-description: 'null'
seo-title: JavaScript での標準広告メタデータの実装
title: JavaScript での標準広告メタデータの実装
uuid: 4ea10c5a- ae2b-45d0- aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# JavaScript での標準広告メタデータの実装{#implement-standard-ad-metadata-on-javascript}

## 広告定数

| 定数名 | 説明   |
|---|---|
| `StandardAdMetadata` | 標準広告メタデータを広告オブジェクトにアタッチするための定数 |

## 実装標準広告メタデータ

標準広告メタデータの場合、プラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。

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

