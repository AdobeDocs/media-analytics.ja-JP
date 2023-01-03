---
title: メディアストリーミングAdobeSDK の実装方法
description: メディア SDK を使用したストリーミングメディア用 Adobe Analyticsの実装について説明します。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: dc1b9fe0-6c75-4f93-a558-a3f3186bcf22
source-git-commit: 85e1d5223cec7168bbf592d941e6a5aece249459
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 6%

---

# メディア SDK の概要 {#implementation-overview}

ストリーミングメディア SDK をビデオプレーヤーフレームワークおよびビデオアプリに実装して、Web、モバイル、および OTT プラットフォーム用のストリーミングメディアデータを収集します。  収集した主要指標は、クラス最高のメディア SDK および API コレクションを使用して、簡単に共有、セグメント化および確認できます。 より深く掘り下げるには — ストリーミングメディア指標を、他のAdobe Analyticsソリューションや、オーディエンス分析やモバイルアプリ訪問指標や人物指標などのデータポイントと組み合わせます。

## サポートされるストリーミングメディアプラットフォーム

### Web 実装

| Platform | バージョン |
|:----:|:----|
| <img src="assets/javascript-icon.png"> | [JavaScript 用メディア SDK v3.x](../../getting-started/download-sdks.md#web-implementation-download-web-sdk) |
| <img src="assets/javascript-icon.png"> | [JavaScript v3.x のタグ付きAdobe MediumAnalytics 拡張機能（データ収集）](../../getting-started/download-sdks.md#web-implementation-download-web-sdk) |

### Mobile の実装

| Platform | バージョン |
|:----:|:----|
| <img src="assets/android-icon.png"> | [タグ付きAdobe Experience Platform Media Analytics 拡張機能（データ収集）](../../getting-started/download-sdks.md#mobile-implementation-get-mobile-extension) |
| <img src="assets/apple-ios-icon.png"> | [タグ付きAdobe Experience Platform Media Analytics 拡張機能（データ収集）](../../getting-started/download-sdks.md#mobile-implementation-get-mobile-extension) |

* iOS Media Analytics for Audio and Video 拡張機能は、iOS、iPadOS および tvOS をサポートします。

### オーバーザトップ実装

| Platform | バージョン |
|:------:|:-----|
| <img src="assets/chromecast-icon.png"> | [Chromecast 用メディア SDK v3.x](../../getting-started/download-sdks.md#over-the-top-implementation-download-ott-libraries) |
| <img src="assets/roku-icon.png"> | [Roku 用メディア SDK v2.x](../../getting-started/download-sdks.md#over-the-top-implementation-download-ott-libraries) |


## 追加情報

サポートされるデバイスとプラットフォームについて詳しくは、 [サポートされるデバイスとプラットフォーム](/help/getting-started/supported-devices.md).

SDK をダウンロードするには、 [タグを使用したメディア SDK、拡張機能、OTT SDK の取得](/help/getting-started/download-sdks.md).
