---
title: Media Analytics SDK をダウンロードするためのアクセスリンク
description: Android、iOS、JavaScript、Chromecast および Roku を含む、利用可能なプラットフォームの SDK ダウンロードのリンクです。
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 522
ht-degree: 81%

---

# Media SDK、タグを使用した拡張機能、OTT SDK の取得 {#download-sdks}

このページの情報には、現在の Media SDK をダウンロードし、タグを使用するメディア拡張機能を取得するためのリンクが含まれています。

Adobe Experience Platform のタグは、アドビが提供する次世代型の web サイトタグおよび Mobile SDK の管理機能です。 タグを使用すると、関連する顧客体験を強化するために必要な分析、マーケティング、広告などのソリューションを、簡単にデプロイして管理できます。 タグについて詳しくは、[タグの概要](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=ja)を参照してください。

## Media SDK と Mobile ライブラリ {#media-sdks-libraries}

### Web 実装 {#download-web-sdk}

| サポートされるプラットフォーム | サポートされるソリューション | 実装方法 | バージョン |  API   |  ドキュメント  |  サンプル  |
|:---:|---|---|---|---| ---| ---|
| ![JavaScript アイコン &#x200B;](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | Analytics のみ | Web - [JS 用 Media SDK v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [JavaScript API リファレンス](/help/implementation/media-sdk/setup/js-3x-api-reference.md) | [JavaScriptを使用してMedia SDKをインストール &#x200B;](/help/implementation/media-sdk/setup/web-implementation.md) | [JS 用 Media SDK v3.0.2 のサンプル](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript アイコン &#x200B;](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | Analytics のみ | Web - メディア拡張機能 |  | [Adobe Medium Analytics (3.x SDK) for Audio and Video 拡張機能 — タグ（データ収集）を使用](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ja) | [Adobe Media Analytics (3.x SDK) for Audio and Video 拡張機能のサンプル](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web - Experience Platform Edge |  | [Edge Networkを使用してCustomer Journey Analytics Streaming Media Collectionを実装](/help/implementation/edge/implementation-edge.md) <p>と</p><p>[Adobe Experience Platform Web SDKを使用してEdgeにWeb データを送信](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Mobile の実装 {#get-mobile-extension}

| サポートされるプラットフォーム | サポートされるソリューション | 実装方法 | バージョン |  ドキュメント   |  サンプル  |
|:---:|---|---|---|---|---|
| ![Android アイコン &#x200B;](assets/android-icon.png)</br>**Android** | Adobe Analytics | Analytics のみ | Android - メディア拡張機能 | [Mobile SDK ドキュメント](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Media Analytics for Audio and Video のサンプル](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS アイコン&#x200B;](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Analytics のみ | iOS／tvOS - メディア拡張機能 | [Mobile SDK ドキュメント](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Media Analytics for Audio and Video のサンプル](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Android アイコン &#x200B;](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android - Experience Platform Edge | [JavaScriptを使用してMedia SDKをインストール &#x200B;](/help/implementation/edge/implementation-edge.md) | |
| ![Apple iOS アイコン&#x200B;](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS／tvOS - Experience Platform Edge | [JavaScriptを使用してMedia SDKをインストール &#x200B;](/help/implementation/edge/implementation-edge.md) |  |

### オーバーザトップ実装 {#download-ott-libraries}

| サポートされるプラットフォーム | サポートされるソリューション | 実装方法 | バージョン |  API   |  ドキュメント  |
|:---:|---|---|---|---|---|
| ![Chromecast アイコン &#x200B;](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Analytics のみ | [Chromecast 用 SDK v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Chromecast API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Chromecast SDKの設定](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md) |
| ![Roku アイコン &#x200B;](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform六SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [JavaScriptを使用してMedia SDKをインストール &#x200B;](/help/implementation/edge/implementation-edge.md) |
