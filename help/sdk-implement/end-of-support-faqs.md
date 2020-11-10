---
title: Media Analytics SDK のサポート終了に関する FAQ
description: このトピックには、Media Analytics SDK のサポート終了に関する FAQ が含まれています。
translation-type: tm+mt
source-git-commit: fdec4da99a43d889690638f1ff3579e145548b69
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 90%

---


# Media Analytics SDK のサポート終了に関する FAQ

2021 年 8 月 31 日にバージョン 4 のモバイル SDK のサポートが終了するのに伴い、iOS および Android 向けの Media Analytics SDK のサポートも終了します。2021 年 8 月 31 日以降、アドビは Media Analytics SDK の修正、OS 関連の更新プログラム、サポートを提供しません。これらの新しいExperience PlatformSDKへの移行プロセス中は、 [メディア分析拡張機能](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) は、ストリーミングメディア用にAdobe Analyticsを有効にするために実装する必要があります。

## 知っておきたいことトップ 5

1. 2021 年 8 月 31 日を過ぎると、Mobile v4 SDK はサポートされなくなります。iOS または Android 用 Adobe Experience Platform（AEP）SDK に移行する必要があります。詳しくは、[バージョン 4 モバイル SDK のサポート終了に関する FAQ](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq)を参照してください。

1. Analytics for Steaming Mediaの導入には、AEP SDKが必要で、AnalyticsおよびMedia Analytics拡張機能が使用されている必要があります。 2021 年 9 月 1 日以降は、新しい AEP SDK および拡張機能を使用する必要があります。Media Analytics 拡張機能は、Adobe Launch を使用して設定されます。詳しくは、[スタンドアロンのメディア SDK から Adobe Launch への移行](https://docs.adobe.com/content/help/ja-JP/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)を参照してください。

1. iOS および Android 用 Media Analytics SDK の機能の開発は終了しました。2019 年秋から導入された新機能は、Media Analytics 拡張機能とメディアコレクション API を使用して有効化されます。

1. Roku SDKとChromecast SDKは、Analytics for Steaming Mediaのお客様が引き続きご利用いただけます。 Roku SDK と Chromecast SDK はスタンドアロンの SDK として引き続き機能強化やサポートがおこなわれます。Media Analytics 用の JS SDK を使用している場合は、引き続きスタンドアロン SDK を使用するか、Adobe Launch を使用して Media Analytics 拡張機能を有効にすることができます。

1. 2021 年 9 月 1 日より前に、アドビは独自の裁量により、技術的影響やビジネス上の影響が大きい問題に対する新しい修正を開発する可能性があります。アドビではお客様の意見に基づき、影響や露出の程度、およびその後のアクティビティを判断します。

ご不明な点がある場合は、アドビのカスタマーサクセスマネージャーにお問い合わせください。

## よくある質問（FAQ）

1. **Roku SDK と Chromecast SDK のサポートは影響を受けますか？**

   いいえ。Roku SDK と Chromecast SDK は、当面の間、スタンドアロン SDK として引き続きサポートされます。

1. **Media Analytics JS SDK の実装は、この変更による影響を受けますか？**

   いいえ。Media Analytics 用 JS SDK をお使いのお客様は、引き続き SDK を使用するか、Adobe Launch を介して SDK を有効にすることができます。

1. **Media Analytics 拡張機能への移行のレベルオブエフォート（LOE）はどの程度ですか？**

   LOE は顧客の実装によって様々です。以下の移行ドキュメントを確認した後、コンサルティングを利用するか、カスタマーケアに問い合わせて、追加のサポートを依頼してください。

   [Media Analytics 拡張機能：Android 版の移行](https://docs.adobe.com/content/help/ja-JP/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics 拡張機能：iOS 版の移行](https://docs.adobe.com/content/help/ja-JP/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics 拡張機能：新規実装](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **タグ管理システムとして Launch が必要ですか？Launch を使用したくない場合はどうなりますか？**

   モバイルアプリの使用例では、Launch は、Web の場合とは異なり、タグ管理システムとしては使用されません。SDK 拡張機能を設定するには、Launch UI を使用する必要があります。これは、Adobe Mobile Services UI を使用してモバイル v4 SDK を設定する方法と似ています。インストールに関して Launch を使用するメリットは、選択した拡張機能に基づいて、インストール手順をカスタマイズできる点です。

1. **tvOS 用 SDK は、このサポートの終了の影響を受けますか？**

   はい。tvOS（バージョン 10 以降）の場合、Media Analytics 拡張機能へ移行することをお勧めします。詳しくは、[スタンドアロンのメディア SDK から Adobe Launch への移行（iOS）](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)を参照してください。

1. **FireTV および AndroidTV 用 SDK は、このサポートの終了の影響を受けますか？**

   はい。FireTV および AndroidTV の場合、Media Analytics 拡張機能へ移行することをお勧めします。詳しくは、[スタンドアロンのメディア SDK から Adobe Launch への移行（Android）](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)を参照してください。
