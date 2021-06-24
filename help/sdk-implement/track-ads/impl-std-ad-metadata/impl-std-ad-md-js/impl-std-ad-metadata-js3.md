---
title: JavaScript 3.xを使用した標準広告メタデータの実装について説明します。
description: JavaScript 3.x アプリを使用するブラウザーで標準広告メタデータを広告トラッキングに使用する方法。
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 84%

---

# JavaScript 3.x を使用した標準広告メタデータの実装{#implement-standard-ad-metadata-on-javascript}

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
