---
title: Media Analytics SDKサポート終了FAQ
description: このトピックには、Media Analytics SDKのサポート終了に関するFAQが含まれています。
translation-type: tm+mt
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 2%

---


# Media Analytics SDKサポート終了FAQ

2021年8月31日にバージョン4のモバイルSDKのサポートが終了すると、アドビはiOSおよびAndroid用のMedia Analytics SDKのサポートも終了します。 2021年8月31日以降、アドビでは、Media Analytics SDKの修正、OS関連の更新、サポートを提供しません。  これらの新しいエクスペリエンスプラットフォームSDKへの移行のプロセス中に、Adobe Analyticsのオーディオおよびビデオを有効にするには、 [Media Analytics拡張機能](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) が実装されている必要があることに注意してください。

## 知りたいことのトップ5

1. Mobile v4 SDKは、2021年8月31日を過ぎるとサポートされなくなります。 iOSおよびAndroid向けのAdobe Experience Platform(AEP)SDKに移行する必要があります。

1. オーディオとビデオの分析の導入には、AEP SDKが必要で、AnalyticsとMedia Analyticsの拡張機能を使用する必要があります。 2021年9月1日から、新しいAEP SDKおよび拡張機能を使用する必要があります。  Media Analytics拡張機能は、「Adobe Launch」を使用して設定されます。  詳しくは、「スタンドアロンメディアSDKからAdobe Launchへの [移行」を参照してください。](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. iOSおよびAndroid用のMedia Analytics SDKの機能の開発は終了しました。  2019年秋から導入された新機能は、Media Analytics拡張機能とメディアコレクションAPIを使用して有効になります。

1. Roku SDKとChromecast SDKは、オーディオおよびビデオのAnalyticsのお客様が引き続き利用できます。 Roku SDKとChromecast SDKは引き続き強化され、スタンドアロンSDKとしてサポートされます。  Media Analytics用のJS SDKを使用する場合、引き続きスタンドアロンSDKを使用するか、Adobe Launchを使用してMedia Analytics拡張機能を有効にすることができます。

1. 2021年9月1日より前に、アドビは、独自の裁量で、高い技術的影響またはビジネス上の影響を及ぼす問題に対する新しい修正を開発することができます。 顧客の入力に基づいて、影響度、露出度、およびその結果生じるアクティビティがアドビによって判断されます。

ご質問がある場合は、アドビのカスタマーサクセスマネージャーにお問い合わせください。

## よくある質問（FAQ）

1. **Roku SDKとChromecast SDKのサポートは影響を受け&#x200B;ますか。**

   いいえ。Roku SDKとChromecast SDKは、当面、スタンドアロンSDKとして引き続きサポートされ&#x200B;ま&#x200B;す。
1. **Media Analytics JS SDKの導入は、この変更によって影響を受け&#x200B;ますか。**

   いいえ。Media Analytics用のJS SDKを使用するお客様は、引き続きSDKを使用するか、Adobe Launchを介してSDKを有効にすることができます。
&#x200B;
1. **Media Analytics拡張機能への移行の取り組みレベルはど&#x200B;れですか。**

   LOEは顧客の実装に依存するので、異なります。  以下の移行ドキュメントを確認した後、コンサルティングやカスタマーケアに問い合わせて、追加のサポートを依頼してください。

   [Media Analytics拡張機能： Androidへの移行](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics拡張機能： iOSの移行](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics拡張機能： 新規実装](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **タグ管理システムとして起動する必要があるか 「起動」を使用しない場合はどうしますか？**

   モバイルの場合、Mobile Services UIなどのメディア拡張機能を設定するには、「起動」が必要です。 モバイルアプリの使用例では、タグ管理システムとしては使用されません。

1. **このサポートの終了は、tvOS用SDKに影響を与えますか。**

   はい。tvOS（バージョン10以降）の場合、推奨される実装は、Media Analytics拡張機能に移行することです。  AEP SDKのサポートとMedia Analytics Extensionのサポートは、2020年6月に予定されています。  詳しくは、スタンドアロンのメディアSDKからAdobe Launch - iOSへの [移行を参照してください](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)。

1. **このサポートの終了は、FireTVおよびAndroidTV用SDKに影響を与えま&#x200B;すか。**

   はい。FireTVおよびAndroidTVの場合、推奨される実装は、Media Analytics Extensionsへの移行です。  AEP SDKのサポートとMedia Analytics Extensionのサポートは、2020年6月に予定されています。  詳しくは、スタンドアロンのメディアSDKからAdobe Launch - Androidへの [移行を参照してください](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)。
