---
title: Media Analytics SDK のサポート終了に関する FAQ
description: このトピックには、Media Analytics SDK のサポート終了に関する FAQ が含まれています。
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/qfM2-x6s-SPf4gw2FpLlg7mPI-h-xZ3Y1TeeVALn3fQ
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
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 639
ht-degree: 61%

---

# Media Analytics Mobile SDKのサポート終了に関するFAQ

2021年8月31日にバージョン 4 Mobile SDKのサポートが終了すると、AdobeはiOSおよびAndroidのMedia Analytics Mobile SDKのサポートも終了しました。 （これには、Adobe Media Analytics SDK for web （JS）や、サポートされているChromecastやRokuなどのOTT プラットフォームは含まれません）。

つまり、Adobeでは、Media Analytics Mobile SDKの修正、OS関連のアップデート、サポートは提供されなくなりました。 新しいExperience Platform SDKに移行する場合は、Adobe ストリーミングメディアサービスを有効にするために[Media Analytics拡張機能](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)を実装する必要があることに注意してください。


## 知っておきたいことトップ 5

1. モバイル v4 SDKは、2021年8月31日をもってサポートされなくなりました。 IOSおよびAndroid用のAdobe Experience Platform（AEP）モバイル SDKに移行する必要があります。

1. Adobe ストリーミングメディアサービスの実装には、AEP Mobile SDKと、AnalyticsおよびMedia Analytics拡張機能の使用が必要です。 2021年9月1日（PT）以降、新しいAEP Mobile SDKと拡張機能を使用する必要があります。  Media Analytics 拡張機能は、アドビタグ（データ収集）を使用して設定されます。 詳しくは、[スタンドアロンの Media SDK から Adobe Launch への移行](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)を参照してください。

1. iOS および Android 用 Media Analytics SDK の機能の開発は終了しました。 2019 年秋から導入された新機能は、Media Analytics 拡張機能とメディアコレクション API を使用して有効化されます。

1. RokuおよびChromecast SDKは、Adobe Analytics for Streaming Media アドオンおよびCustomer Journey Analytics Streaming Media Collection アドオンで引き続きご利用いただけます。 Roku SDK と Chromecast SDK はスタンドアロンの SDK として引き続き機能強化やサポートが行われます。 Media Analytics 用の JS SDK を使用している場合は、引き続きスタンドアロン SDK を使用するか、Adobe データ収集（以前の Adobe Launch）を使用して Media Analytics 拡張機能を有効にすることができます。

ご不明な点がある場合は、Adobeアカウントチームにお問い合わせください。

## よくある質問（FAQ）

1. **Roku SDK と Chromecast SDK のサポートは影響を受けますか？**

   いいえ。  RokuとChromecast SDKは、当面の間、スタンドアロン SDKとして引き続きサポートされる&#x200B;
&#x200B;
1. **Media Analytics JS SDK の実装は、この変更による影響を受けますか？**

   いいえ。  JS SDK for Media Analyticsを使用しているお客様は、引き続きSDKを使用するか、Adobe Launchで有効にすることができます。
&#x200B;
1. **Media Analytics 拡張機能への移行のレベルオブエフォート（LOE）はどの程度ですか？**

   LOE は顧客の実装によって様々です。  以下の移行ドキュメントを確認した後、コンサルティングを利用するか、カスタマーケアに問い合わせて、追加のサポートを依頼してください。

   [Media Analytics 拡張機能：Android 版の移行](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

   [Media Analytics 拡張機能：iOS 版の移行](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Media Analytics拡張機能：新しい実装](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **タグ管理システムとして Launch が必要ですか？ Launch を使用したくない場合はどうなりますか？**

   モバイルアプリのユースケースでは、Launch は、web の場合とは異なり、タグ管理システムとしては使用されません。 SDK 拡張機能を設定するには、Launch UI を使用する必要があります。 これは、Adobe Mobile Services UI を使用してモバイル v4 SDK を設定する方法と似ています。 インストールに関して Launch を使用するメリットは、選択した拡張機能に基づいて、インストール手順をカスタマイズできる点です。

1. **tvOS 用 SDK は、このサポートの終了の影響を受けますか？**

   はい。tvOS（バージョン 10 以降）の場合、Media Analytics 拡張機能へ移行することをお勧めします。 詳しくは、[スタンドアロンの Media SDK から Adobe Launch への移行（iOS）](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)を参照してください。

1. **Fire TV および Android TV 用 SDK は、このサポートの終了の影響を受けますか？**

   はい。Fire TV および Android TV の場合、Media Analytics 拡張機能へ移行することをお勧めします。 詳しくは、[スタンドアロンの Media SDK から Adobe Launch への移行（Android）](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)を参照してください。
