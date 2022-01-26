---
title: Media Analytics の新機能
description: 新着情報には、新機能と通知に関する情報が含まれています。
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 100%

---


# Media Analytics の新機能{#whats-new}

![バナー](assets/media_analytics_banner.png)


このページでは、Media Analytics の新機能、修正点および重要な注意事項について説明します。また、Media Analytics を最大限に活用するための新しいドキュメント、トレーニングコース、ビデオチュートリアルも紹介しています。


## リリースノート

Adobe Experience Cloud のリリースノート

Adobe Experience Cloud のリリースノートでは、Adobe Experience Cloud での新機能、修正、重要な注意事項について説明しています。 これには、Media Analytics に対する最新の変更が含まれます。 また、Experience Cloud を最大限に活用するための新しいドキュメント、トレーニングコース、ビデオチュートリアルも紹介しています。

## 新機能

| 機能 | [一般公開](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html?lang=ja) - ターゲット日 | 説明 |
| ----------- | ---------- | ---------- |
| [メディア同時ビューアパネル](media-reports/media-workspace-panels/media-concurrent-viewers.md) | 2020 年 9 月 17 日（PT） | Workspace のメディア同時ビューアパネルを使用すると、同時実行のピークが発生した場所やドロップオフが発生した場所を把握できます。コンテンツの質と閲覧者の関与に関する貴重な情報を提供し、ボリュームやスケールのトラブルシューティングや計画に役立ちます。 |
| [サポートされるデバイスとプラットフォーム](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html?lang=ja) | 2020 年 6 月 18 日（PT） | AEP Mobile SDK を含む [!UICONTROL Media Launch 拡張機能]で、以下の OTT デバイスがサポートされるようになりました。<ul><li>Apple TV（tvOS）</li><li>Fire TV（Fire OS）</li><li>Android TV</li></ul> |
| [プレーヤーステートトラッキング](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/player-state-overview.html?lang=ja) | 2020 年 5 月 29 日（PT） | [!UICONTROL Media Analytics] のお客様は、標準的なソリューション変数のセット（フルスクリーン、クローズドキャプション、ミュート、ピクチャインピクチャ、インフォーカス）を使用して、再生中の閲覧者のインタラクションをキャプチャできます。また、カスタムプレーヤー状態を柔軟に作成することもできます。[!UICONTROL Analysis Workspace] のレポートで、[!UICONTROL プレイヤー状態追跡]変数を使用できるようになりました。この機能を使用するには、次のいずれかが必要です。 <ul><li>Media [!DNL JavaScript] SDK 3.0 以降</li><li>[!DNL Adobe Experience Platform]（AEP）SDK で使用する場合：</li><li>[!UICONTROL Media Analytics 拡張機能]（Web 用）：[!UICONTROL Adobe Media Analytics]（3.x SDK）for Audio および Adobe Media Analytics for Video v1.0 以降</li><li>[!UICONTROL Media Analytics Extension]（モバイル用）：[!UICONTROL Adobe Media Analytics for Audio] および Adobe Media Analytics for Video v2.0 以降</li><li>[!UICONTROL メディアコレクション]</li></ul> |


## 重要な通知

| 機能 | [一般公開](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html) - ターゲット日 | 説明 |
| ----------- | ---------- | ---------- |
| [サポートされるデバイスとプラットフォーム](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 2021 年 8 月 31 日（PT） | 2021 年 8 月 31 日（PT）にバージョン 4 のモバイル SDK のサポートが終了するのに伴い、iOS および Android 向けの Media Analytics SDK のサポートも終了します。詳しくは、Media Analytics SDK のサポート終了に関する FAQ を参照してください。 |
| [Media Analytics SDK のサポート終了に関する FAQ](sdk-implement/end-of-support-faqs.md) | 2019 年秋 | iOS および Android 用 Media Analytics SDK の機能の開発は終了しました。2019 年秋から導入された新機能は、Media Analytics 拡張機能とメディアコレクション API を使用して有効化されます。 |
| [メディアの概要](media-overview.md) | 2019 年 2 月 20 日（PT） | アドビは TLS 1.1 以降のみをサポートします。 この変更により、アドビは、TLS 1.0 をデプロイしている古いデバイスや Web ブラウザーを使用するエンドユーザーから情報を収集しなくなります。 |
| [サポートされるデバイスとプラットフォーム](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 2019 年 2 月 19 日（PT） | 各 SDK でサポートされる最小プラットフォームバージョンを以下に示します。 <br>- iOS：iOS 6 以降<br>- Android：Android 5.0 以降 - Lollipop <br>- Chrome：v22 以降<br>- Mozilla：v27 以降<br> - Safari：v7 以降<br>- IE：v1 以降 |
| [オーディオおよびビデオパラメーター](metrics-and-metadata/audio-video-parameters.md) | 2019 年 2 月 7 日（PT） | Adobe Analytics for Video and Audio は指標名の変更をリリースしました。<i>Media Initiates</i> は <i>Media Starts</i> と呼ばれるようになります。この変更は、指標とレポートの業界標準を反映し、レポートで指標を簡単に識別できるようにするためにおこなわれました。 |
| [オーディオおよびビデオパラメーター](metrics-and-metadata/audio-video-parameters.md) | 2018 年 9 月 13 日（PT） | ビデオおよびオーディオ分析のクロスコンテンツトラッキングをおこなえるように、一部のディメンション、指標およびレポートのラベルが変更されています。例えば、ラベルの「*ビデオ開始*」が「*メディア開始*」に、「*ビデオの長さ*」が「*コンテンツの長さ*」に、「*ビデオ名*」が「*コンテンツ名*」に変更されています。Reports and Analytics のすべてのビデオレポートが、「ビデオ」という名前の代わりに「メディア」を使用するように更新されています。ラベルの変更によるデータ収集および履歴データへの影響はありません。Report Builder 内またはこの変更の影響を受ける可能性のある他の外部自動データプルでこれらを使用している場合は、これらの変更に注意してください。 |




<!-- | title | date | description | -->
