---
title: JavaScript 3.x を使用した標準広告メタデータの実装
description: JavaScript 3.x アプリを使用するブラウザーで標準広告メタデータを広告トラッキングに使用する方法。
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/hZgQett-bN5iyckYrxK1sGlcB83b0t0va0Rxb1yalWE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 59
ht-degree: 93%

---

# JavaScript 3.x を使用した標準広告メタデータの実装{#implement-standard-ad-metadata-on-javascript}

## 標準的な広告メタデータの実装

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
