---
title: JavaScript 3.x を使用した標準広告メタデータの実装
description: JavaScript 3.x アプリを使用するブラウザーで標準広告メタデータを広告トラッキングに使用する方法。
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '54'
ht-degree: 100%

---

# JavaScript 3.x を使用した標準広告メタデータの実装 {#implement-standard-ad-metadata-on-javascript}

## 標準広告メタデータの実装

標準広告メタデータの場合、ご利用のプラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。

```js
var adObject =
ADB.Media.createAdObject(<AD_NAME>,
                              <AD_ID>,
                              <POSITION>,
                              <LENGTH>);

// Set standard Ad Metadata
var adMetadata = {};
adMetadata[MediaHeartbeat.AdMetadataKeys.Advertiser] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CampaignId] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
