---
title: Media Analytics SDK のサポート終了に関する FAQ
description: このトピックには、Media Analytics SDK のサポート終了に関する FAQ が含まれています。
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b022bed6b7be0cc97caaaf6b7bbc42474a57b400
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 96%

---

# Media Analytics Mobile SDK のサポート終了に関する FAQ

2021年8月31日にバージョン 4 の Mobile SDK のサポートが終了するのに伴い、iOS および Android 向けの Media Analytics Mobile SDK のサポートも終了します。2021年8月31日（PT）以降、アドビは Media Analytics Mobile SDK の修正、OS 関連の更新プログラム、サポートを提供しません。これらの新しい Experience Platform SDK への移行プロセス中に、Adobe Analytics for Streaming Media を有効にするには、[Media Analytics 拡張機能](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)を実装する必要があることに注意してください。

>[!NOTE]
>Adobe Experience Platform Launch は、Experience Platform のデータ収集テクノロジースイートとしてリブランドされています。その結果、製品ドキュメント全体でいくつかの用語の変更がロールアウトされました。用語の変更点の一覧については、次の[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ja)を参照してください。


## 知っておきたいことトップ 5

1. 2021 年 8 月 31 日（PT）を過ぎると、Mobile v4 SDK はサポートされなくなります。iOS または Android 用 Adobe Experience Platform（AEP）Mobile SDK に移行する必要があります。詳しくは、[バージョン 4 モバイル SDK のサポート終了に関する FAQ](https://developer.adobe.com/client-sdks/documentation/v4-end-of-life-faq/)を参照してください。

1. Analytics for Streaming Media を実装するには AEP Mobile SDK と、Analytics と Media Analytics の拡張機能を使用する必要があります。2021 年 9 月 1 日（PT）以降は、新しい AEP Mobile SDK および拡張機能を使用する必要があります。Media Analytics 拡張機能は、Adobe タグ（データ収集）を使用して設定されます。詳しくは、[スタンドアロンのメディア SDK から Adobe Launch への移行](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)を参照してください。

1. iOS および Android 用 Media Analytics SDK の機能の開発は終了しました。2019 年秋から導入された新機能は、Media Analytics 拡張機能とメディアコレクション API を使用して有効化されます。

1. Analytics for Streaming Media のお客様は引き続き、Roku SDK と Chromecast SDK をご利用いただけます。Roku SDK と Chromecast SDK はスタンドアロンの SDK として引き続き機能強化やサポートが行われます。Media Analytics 用の JS SDK を使用している場合は、引き続きスタンドアロン SDK を使用するか、Adobe データ収集（以前の Adobe Launch）を使用して Media Analytics 拡張機能を有効にすることができます。

1. 2021 年 9 月 1 日（PT）より前に、アドビは独自の裁量により、技術的影響やビジネス上の影響が大きい問題に対する新しい修正を開発する可能性があります。アドビではお客様の意見に基づき、影響や露出の程度、およびその後のアクティビティを判断します。

ご不明な点がある場合は、アドビのカスタマーサクセスマネージャーにお問い合わせください。

## よくある質問（FAQ）

1. **Roku SDK と Chromecast SDK のサポートは影響を受けますか？**

   いいえ。Roku SDK と Chromecast SDK は、当面の間、スタンドアロン SDK として引き続きサポートされます。

1. **Media Analytics JS SDK の実装は、この変更による影響を受けますか？**

   いいえ。Media Analytics 用 JS SDK をお使いのお客様は、引き続き SDK を使用するか、Adobe Launch を介して SDK を有効にすることができます。

1. **Media Analytics 拡張機能への移行のレベルオブエフォート（LOE）はどの程度ですか？**

   LOE は顧客の実装によって異なるので、異なります。  以下の移行ドキュメントを確認した後、コンサルティングを利用するか、カスタマーケアに問い合わせて、追加のサポートを依頼してください。

[Media Analytics 拡張機能：Android 版の移行](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Media Analytics 拡張機能：iOS 版の移行](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Media Analytics 拡張機能：新規実装](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **タグ管理システムとして Launch が必要ですか？Launch を使用したくない場合はどうなりますか？**

   モバイルアプリの使用例では、Launch は、Web の場合とは異なり、タグ管理システムとしては使用されません。SDK 拡張機能を設定するには、Launch UI を使用する必要があります。これは、Adobe Mobile Services UI を使用してモバイル v4 SDK を設定する方法と似ています。インストールに関して Launch を使用するメリットは、選択した拡張機能に基づいて、インストール手順をカスタマイズできる点です。

1. **tvOS 用 SDK は、このサポートの終了の影響を受けますか？**

   はい。tvOS（バージョン 10 以降）の場合、Media Analytics 拡張機能へ移行することをお勧めします。詳しくは、[スタンドアロンの Media SDK から Adobe Launch への移行（iOS）](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)を参照してください。

1. **Fire TV および Android TV 用 SDK は、このサポートの終了の影響を受けますか？**

   はい。Fire TV および Android TV の場合、Media Analytics 拡張機能へ移行することをお勧めします。詳しくは、[スタンドアロンの Media SDK から Adobe Launch への移行（Android）](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)を参照してください。