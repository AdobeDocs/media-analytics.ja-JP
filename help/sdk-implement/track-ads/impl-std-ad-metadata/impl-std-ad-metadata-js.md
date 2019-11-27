---
title: JavaScript での標準広告メタデータの実装
description: ブラウザー（JS）アプリ上の広告トラッキングでの標準広告メタデータの使用方法です。
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# JavaScript での標準広告メタデータの実装 {#implement-standard-ad-metadata-on-javascript}

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

