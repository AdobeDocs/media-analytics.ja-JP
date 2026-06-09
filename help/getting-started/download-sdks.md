---
title: Media SDK、エクステンションおよびAPIを入手
description: Android、iOS、JavaScript、Chromecast および Roku を含む、利用可能なプラットフォームの SDK ダウンロードのリンクです。
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdbid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 625
ht-degree: 30%

---

# Media SDK、エクステンションおよびAPIを入手

## Edgeの実装（推奨） {#edge-sdks}

Edgeでは、一度収集したデータをAdobe Experience Platform Edge Networkを通じて、Adobe Analytics、Customer Journey Analytics、Adobe Journey Optimizer、Real-Time CDPなどの複数の配信先に配信できます。 SDKがネイティブでないプラットフォーム（スマートテレビ、ゲーム機、セットトップボックスなど）の場合は、Media Edge APIを使用します。

| | ドキュメント | サンプル |
|:---:|---|---|
| [![JavaScript アイコン ](assets/javascript-icon.png)](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/install/overview)<br>[Web SDK](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/install/overview) | [ ストリーミングメディア用にWeb SDKを設定](/help/implementation/edge/web-sdk.md) | [ サンプル ](https://github.com/adobe/alloy-samples/blob/main/media-collection/STANDALONE.md) |
| [![拡張機能アイコン ](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html)<br>[Web SDK タグ拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html) | [ ストリーミングメディア用のWeb SDK タグ拡張機能の設定](/help/implementation/edge/web-sdk-tags.md) | [ サンプル ](https://github.com/adobe/alloy-samples/blob/main/media-collection/TAGS_IMPL.md) |
| [![Android アイコン ](assets/android.png)](https://github.com/adobe/aepsdk-media-android)<br>[Android SDK](https://github.com/adobe/aepsdk-media-android) | [ ストリーミングメディア用にAndroidを設定](/help/implementation/edge/android.md) | [ サンプル ](https://github.com/adobe/aepsdk-media-android/tree/main/code/testapp) |
| [![Apple iOS アイコン ](assets/apple.png)](https://github.com/adobe/aepsdk-media-ios)<br>[iOS / tvOS SDK](https://github.com/adobe/aepsdk-media-ios) | [ ストリーミングメディア用にiOSを設定](/help/implementation/edge/ios.md) | [ サンプル ](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| [![拡張機能アイコン ](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Android タグ拡張機能](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [ ストリーミングメディア用のAndroid タグ拡張機能の設定](/help/implementation/edge/android-tags.md) | |
| [![拡張機能アイコン ](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[iOS / tvOS タグ拡張機能](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [ ストリーミングメディア用のiOS タグ拡張機能の設定](/help/implementation/edge/ios-tags.md) | |
| [![Roku icon](assets/roku-icon.png)](https://github.com/adobe/aepsdk-roku)<br>[Roku Edge SDK](https://github.com/adobe/aepsdk-roku) | [ ストリーミングメディア用にRoku Edgeを設定](/help/implementation/edge/roku.md) | [ サンプル ](https://github.com/adobe/aepsdk-roku/tree/main/sample/simple-videoplayer-channel) |
| [![API アイコン ](assets/api.png)](https://developer.adobe.com/data-collection-apis/docs/api/media-edge)<br>[Media Edge API](https://developer.adobe.com/data-collection-apis/docs/api/media-edge) | [Media Edge APIの設定](/help/implementation/edge/media-edge-api.md) | [ サンプル ](https://developer.adobe.com/data-collection-apis/docs/getting-started/media-edge-examples) |

## Analyticsのみの実装 {#analytics-only-sdks}

これらのSDKと拡張機能は、Adobe Analyticsに直接データを送信します。 新しい実装については、上記のEdgeの実装を使用してください。 既存のAnalytics データをCustomer Journey Analyticsまたはその他のExperience Platform アプリケーションに取り込むには、[Analytics ソースコネクタ ](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/analytics)を使用します。

| | ドキュメント | サンプル |
|:---:|---|---|
| [![JavaScript アイコン ](assets/javascript-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2)<br>[Media SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [ ストリーミングメディア用にJavaScriptを設定](/help/implementation/analytics-only/javascript.md) | [ サンプル ](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| [![拡張機能アイコン ](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ja)<br>[ メディア拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ja) | [ ストリーミングメディアのタグを使用したJavaScriptの設定](/help/implementation/analytics-only/javascript-tags.md) | [ サンプル ](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| [![Chromecast icon](assets/chromecast-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3)<br>[Chromecast SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [ ストリーミングメディア用Chromecastの設定](/help/implementation/analytics-only/chromecast.md) | [ サンプル ](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/chromecast/samples/BasicPlayerSample) |
| [![Roku icon](assets/roku-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.7)<br>[Roku SDK 2.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.7) | [ ストリーミングメディア用にRoku 2.xを設定](/help/implementation/analytics-only/roku-2x.md) | [ サンプル ](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/roku/samples) |
| [![API アイコン ](assets/api.png)](/help/implementation/media-collection-api/mc-api-overview.md)<br>[ メディアコレクション API](/help/implementation/media-collection-api/mc-api-overview.md) | [Media Collection APIの設定](/help/implementation/analytics-only/media-collection-api.md) | |
