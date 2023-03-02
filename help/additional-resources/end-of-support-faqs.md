---
title: Media Analytics SDK のサポート終了に関する FAQ
description: このトピックには、Media Analytics SDK のサポート終了に関する FAQ が含まれています。
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b955b20495a504020a214c3a9e32b676701ee4cc
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 79%

---

# Media Analytics Mobile SDK のサポート終了に関する FAQ

2021 年 8 月 31 日にバージョン 4 のモバイル SDK のサポートが終了すると共に、AdobeはiOSおよび Android 用の Media Analytics Mobile SDK のサポートを終了しました。 ( これには、Web 用 Media Analytics SDK(JS) や、Chromecast や Roku などの OTT プラットフォームは含まれません（まだサポートされています）。

つまり、Adobeは Media Analytics Mobile SDK の修正、OS 関連の更新、サポートを提供しなくなりました。 新しいExperience PlatformSDK に移行する際は、 [Media Analytics 拡張機能](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) ストリーミングメディア用 Adobe Analyticsを有効にするには、を実装する必要があります。


## 知っておきたいことトップ 5

1. 2021 年 8 月 31 日以降、Mobile v4 SDK はサポートされなくなりました。 iOS または Android 用 Adobe Experience Platform（AEP）Mobile SDK に移行する必要があります。詳しくは、[バージョン 4 モバイル SDK のサポート終了に関する FAQ](https://developer.adobe.com/client-sdks/documentation/v4-end-of-life-faq/)を参照してください。

1. Analytics for Streaming Media を実装するには AEP Mobile SDK と、Analytics と Media Analytics の拡張機能を使用する必要があります。2021 年 9 月 1 日以降は、新しい AEP Mobile SDK および拡張機能を使用する必要があります。  Media Analytics 拡張機能は、アドビタグ（データ収集）を使用して設定されます。詳しくは、[スタンドアロンの Media SDK から Adobe Launch への移行](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)を参照してください。

1. iOS および Android 用 Media Analytics SDK の機能の開発は終了しました。2019 年秋から導入された新機能は、Media Analytics 拡張機能とメディアコレクション API を使用して有効化されます。

1. Analytics for Streaming Media のお客様は引き続き、Roku SDK と Chromecast SDK をご利用いただけます。Roku SDK と Chromecast SDK はスタンドアロンの SDK として引き続き機能強化やサポートが行われます。Media Analytics 用の JS SDK を使用している場合は、引き続きスタンドアロン SDK を使用するか、Adobe データ収集（以前の Adobe Launch）を使用して Media Analytics 拡張機能を有効にすることができます。

ご質問がある場合は、Adobeアカウントチームにお問い合わせください。

## よくある質問（FAQ）

1. **Roku SDK と Chromecast SDK のサポートは影響を受けますか？**

   いいえ。Roku SDK と Chromecast SDK は、当面の間、スタンドアロン SDK として引き続きサポートされます。

1. **Media Analytics JS SDK の実装は、この変更による影響を受けますか？**

   いいえ。Media Analytics 用 JS SDK をお使いのお客様は、引き続き SDK を使用するか、Adobe Launch を介して SDK を有効にすることができます。

1. **Media Analytics 拡張機能への移行のレベルオブエフォート（LOE）はどの程度ですか？**

   LOE は顧客の実装によって様々です。以下の移行ドキュメントを確認した後、コンサルティングを利用するか、カスタマーケアに問い合わせて、追加のサポートを依頼してください。

[Media Analytics 拡張機能：Android 版の移行](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Media Analytics 拡張機能：iOS 版の移行](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Media Analytics 拡張機能：新規実装](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **タグ管理システムとして Launch が必要ですか？Launch を使用したくない場合はどうなりますか？**

   モバイルアプリのユースケースでは、Launch は、web の場合とは異なり、タグ管理システムとしては使用されません。SDK 拡張機能を設定するには、Launch UI を使用する必要があります。これは、Adobe Mobile Services UI を使用してモバイル v4 SDK を設定する方法と似ています。インストールに関して Launch を使用するメリットは、選択した拡張機能に基づいて、インストール手順をカスタマイズできる点です。

1. **tvOS 用 SDK は、このサポートの終了の影響を受けますか？**

   はい。tvOS（バージョン 10 以降）の場合、Media Analytics 拡張機能へ移行することをお勧めします。詳しくは、[スタンドアロンの Media SDK から Adobe Launch への移行（iOS）](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)を参照してください。

1. **Fire TV および Android TV 用 SDK は、このサポートの終了の影響を受けますか？**

   はい。Fire TV および Android TV の場合、Media Analytics 拡張機能へ移行することをお勧めします。詳しくは、[スタンドアロンの Media SDK から Adobe Launch への移行（Android）](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)を参照してください。
