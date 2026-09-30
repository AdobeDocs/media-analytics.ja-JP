---
title: Media Analytics タグ拡張機能の設定
description: Adobe Media Analytics （3.x SDK）のオーディオおよびビデオタグ拡張機能を使用して、Analyticsのみのストリーミングメディアを実装します。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 14%
---
# Media Analytics タグ拡張機能の設定

Adobe Media Analytics （3.x SDK）の音声および動画用タグ拡張機能は、Media SDK JavaScript（3.x）をタグ経由でデプロイします。JavaScriptを手動でインストールする必要はありません。 このページでは、タグ設定について説明します。 代わりにコードにSDKをインストールするには、[&#x200B; ストリーミングメディア用にJavaScriptを設定](javascript.md)を参照してください。 新しい実装の場合は、推奨される[Web SDK タグ拡張機能](/help/implementation/edge/web-sdk-tags.md) Edge パスを検討してください。

* **前提条件**: [Analyticsのみの実装の概要](overview.md)を完了します。

## 拡張機能のインストールと設定

データ収集UIで拡張機能をインストールして設定することで、タグ対応サイトにMedia Tracker インスタンスを追加します。 インストールと設定の詳細については、[Adobe Media Analytics （3.x SDK） for Audio and Video拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ja)を参照してください。

## メディアイベントの追跡

拡張機能を設定した状態で、トラッカー方式を使用して各メディアイベントを追跡します。 正確な呼び出しについては、各[event](/help/implementation/events/overview.md)および[variable](/help/implementation/variables/overview.md) ページの&#x200B;**Media SDK JS 3.x** タブを参照してください。

## 次の手順

実装が完了したら、[Analyticsのみの実装用のレポートを設定できます](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [&#x200B; オーディオおよびビデオ拡張機能のAdobe Media Analytics （3.x SDK） &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ja)
>* [&#x200B; ストリーミングメディア用にJavaScriptを設定する（コード内） &#x200B;](javascript.md)
>* [&#x200B; イベントの概要](/help/implementation/events/overview.md)
