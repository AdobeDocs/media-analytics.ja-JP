---
title: Media Analytics SDK をダウンロードするためのアクセスリンク
description: Android、iOS、JavaScript、Chromecast および Roku を含む、利用可能なプラットフォームの SDK ダウンロードのリンクです。
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 81%

---

# Media SDK、タグを使用した拡張機能、OTT SDK の取得 {#download-sdks}

このページの情報には、現在の Media SDK をダウンロードし、タグを使用するメディア拡張機能を取得するためのリンクが含まれています。

Adobe Experience Platform のタグは、アドビが提供する次世代型の web サイトタグおよび Mobile SDK の管理機能です。タグを使用すると、関連する顧客体験を強化するために必要な分析、マーケティング、広告などのソリューションを、簡単にデプロイして管理できます。タグについて詳しくは、[タグの概要](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=ja)を参照してください。


>[!NOTE]
>
>レガシー SDK のダウンロードについて詳しくは、[レガシー - SDK のダウンロード](/help/legacy/legacy-download-sdks.md)を参照してください。<br>
>サポート終了に関する重要な情報については、[サポート終了に関する FAQ](/help/additional-resources/end-of-support-faqs.md) を参照してください。

## Media SDK と Mobile ライブラリ {#media-sdks-libraries}

### Web 実装 {#download-web-sdk}

| サポートされるプラットフォーム | サポートされるソリューション | 実装方法 | バージョン |  API   |  ドキュメント  |  サンプル  |
|:---:|---|---|---|---| ---| ---|
| ![JavaScript アイコン ](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | Analytics のみ | Web - [JS 用 Media SDK v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [JavaScript API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [JavaScriptを使用した Media SDK のインストール ](/help/implementation/media-sdk/setup/web-implementation.md) | [JS 用 Media SDK v3.0.2 のサンプル](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript アイコン ](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | Analytics のみ | Web - メディア拡張機能 |  | [Adobe Medium Analytics (3.x SDK) for Audio and Video 拡張機能 — タグ（データ収集）を使用](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ja) | [Adobe Media Analytics (3.x SDK) for Audio and Video 拡張機能のサンプル](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web -Experience PlatformEdge |  | [Edge Networkを使用した Streaming Media Collection アドオンの実装 ](/help/implementation/edge/implementation-edge.md) <p>と</p><p>[Adobe Experience Platform Web SDK を使用したEdgeへの web データの送信 ](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Mobile の実装 {#get-mobile-extension}

| サポートされるプラットフォーム | サポートされるソリューション | 実装方法 | バージョン |  ドキュメント   |  サンプル  |
|:---:|---|---|---|---|---|
| ![Androidアイコン ](assets/android-icon.png)</br>**Android** | Adobe Analytics | Analytics のみ | Android - メディア拡張機能 | [Mobile SDK ドキュメント](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Media Analytics for Audio and Video のサンプル](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS アイコン&#x200B;](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Analytics のみ | iOS／tvOS - メディア拡張機能 | [Mobile SDK ドキュメント](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Media Analytics for Audio and Video のサンプル](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Androidアイコン ](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android - Experience Platform Edge | [JavaScriptを使用した Media SDK のインストール ](/help/implementation/edge/implementation-edge.md) | |
| ![Apple iOS アイコン&#x200B;](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS／tvOS - Experience Platform Edge | [JavaScriptを使用した Media SDK のインストール ](/help/implementation/edge/implementation-edge.md) |  |

### オーバーザトップ実装 {#download-ott-libraries}

| サポートされるプラットフォーム | サポートされるソリューション | 実装方法 | バージョン |  API   |  ドキュメント  |
|:---:|---|---|---|---|---|
| ![Chromecast アイコン ](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Analytics のみ | [Chromecast 用 SDK v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Chromecast API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Chromecast 用 Mobile SDK v3.x のセットアップ](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku icon ](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | Analytics のみ | [Roku 用 SDK v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [Roku 用 Mobile SDK v2.x のセットアップ](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![Roku icon ](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [JavaScriptを使用した Media SDK のインストール ](/help/implementation/edge/implementation-edge.md) |
