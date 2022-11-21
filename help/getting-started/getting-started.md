---
title: はじめに
description: ストリーミングメディア用Adobe Analyticsの概要
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 6%

---

# はじめに {#getting-started}

Adobe Analytics for Streaming Media には、メディア SDK とメディアコレクション API の 2 つの主な実装方法が用意されています。

![メソッド](assets/getting-started2.png)

組み込みロジックの使用 **メディア SDK**&#x200B;を使用すると、Web サイト、携帯電話、接続されたテレビ、タブレット、OTT デバイス、セットトップボックス、ゲームコンソールなど、複数のメディアプラットフォームを正確に測定できます。 ダウンロードされたコンテンツも測定できます。 ユーザーに対するエンゲージメントの閲覧に深く関わるインサイトを活用して、閲覧者の関与する期間、日時、場所を把握できます。 メディア SDK は、 **メディアコレクション API** 追跡用。 アプリケーションでカスタムトラッキング機能が必要な場合は、メディアコレクション API をカスタマイズできます。 メディア SDK でサポートされていないデバイスの場合は、メディアコレクション API を使用できます。

Adobe Analyticsストリーミングメディアソリューションは、次のメディアプラットフォームに対して提供されます。

* Web
* モバイル
* 上
* ストリーミングメディアやサーバ間の統合に使用できる接続済みデバイス

詳しくは、 [サポートされるデバイスとプラットフォーム](#_Supported_devices_and).

>[!IMPORTANT]
>
>Adobe Analytics Streaming Media を実装するには、Adobeの営業担当またはアカウントマネージャーに連絡して、Streaming Media が製品ポートフォリオに含まれていることを確認してください。

## ストリーミングメディア用メディア SDK {#media-sdks}

ストリーミングメディア用のメディア SDK は、JavaScript、Android、iOS、tvOS、Chromecast、Roku の各プラットフォームで使用できます。

メディア SDK のダウンロードとインストールについて詳しくは、 [タグを使用したメディア SDK、拡張機能、OTT SDK の取得](/help/getting-started/download-sdks.md).


## メディアコレクション API {#media-collection-apis}

この **メディアコレクション API** media analytics の実装をカスタマイズできます。 Adobeコレクション API を使用してメディアのサーバーを直接呼び出し、SDK などを使用して実行できるほとんどすべてのアクションを実行します。 データ収集をカスタマイズして、ストリーミングメディアデータに関する重要な質問に回答するレポートを作成します。

メディアコレクション API の使用について詳しくは、 [ストリーミングメディア API ドキュメント](/help/implementation/media-collection-api/mc-api-overview.md).

## アドビ拡張機能 {#adobe-extensions}

* この [**Adobe MediumAnalytics for Audio and Video 拡張機能**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) （Media Analytics 拡張機能）、iOSおよび tvOS 実装で必要です。 タグサイトまたはプロジェクトにトラッカーインスタンスを追加する機能を提供します。 MA 拡張機能には、Analytics 拡張機能とExperience CloudID 拡張機能も必要です。

* [Analytics 拡張機能 v1.6 以降](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en) — この拡張機能を使用すると、Adobe Experience Platform Web SDK Javascript ライブラリを読み込んで、データをAdobeソリューションに送信できます。

* [Experience CloudID 拡張](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en) — この拡張機能は、すべてのExperience Cloudソリューションをまたいで訪問者を識別するExperience CloudID サービスを実装します。 Experience CloudID サービスは、Adobe Experience Platformのパーソナライズ機能の拡張機能です。
