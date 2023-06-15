---
title: Adobe Streaming Media SDK の実装方法
description: Media SDK を使用したストリーミングメディア用 Adobe Analytics の実装について説明します。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: dc1b9fe0-6c75-4f93-a558-a3f3186bcf22
source-git-commit: 1e4babe0df218342fc4836155139d908ba113510
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Media SDK の概要 {#implementation-overview}

Streaming Media SDK をビデオプレーヤーフレームワークとビデオアプリに実装して、web、モバイルおよび OTT プラットフォームのストリーミングメディアデータを収集します。 収集した主要指標は、クラス最高のメディア SDK および API コレクションを使用して、簡単に共有、セグメント化および確認できます。より深く掘り下げるには - ストリーミングメディア指標を、他の Adobe Analytics ソリューションや、オーディエンス分析またはモバイルアプリ訪問指標と人物指標などのデータポイントと組み合わせます。

## サポートされるストリーミングメディアプラットフォーム

### Web 実装

| Platform | バージョン |
|:----:|:----|
| <img src="assets/javascript-icon.png"> | [JavaScript v3.x 用 Media SDK](../../getting-started/download-sdks.md#web-implementation-download-web-sdk) |
| <img src="assets/javascript-icon.png"> | [JavaScript v3.x 用のタグ付き Adobe Media Analytics 拡張機能（データ収集）](../../getting-started/download-sdks.md#web-implementation-download-web-sdk) |
| <img src="assets/javascript-icon.png"> | [Experience Platformエッジ](../../getting-started/download-sdks.md#web-implementation-download-web-sdk) （近日公開） |

### Mobile の実装

| Platform | バージョン |
|:----:|:----|
| <img src="assets/android-icon.png"> | [タグ付き Adobe Experience Platform Media Analytics 拡張機能（データ収集）](../../getting-started/download-sdks.md#mobile-implementation-get-mobile-extension) |
| <img src="assets/apple-ios-icon.png"> | [タグ付き Adobe Experience Platform Media Analytics 拡張機能（データ収集）](../../getting-started/download-sdks.md#mobile-implementation-get-mobile-extension) |
| <img src="assets/android-icon.png"> | [Experience Platformエッジ](../../getting-started/download-sdks.md#mobile-implementation-get-mobile-extension) |
| <img src="assets/apple-ios-icon.png"> | [Experience Platformエッジ](../../getting-started/download-sdks.md#mobile-implementation-get-mobile-extension) |

* iOS Media Analytics for Audio and Video 拡張機能は、iOS、iPadOS および tvOS をサポートします。

### オーバーザトップ実装

| Platform | バージョン |
|:------:|:-----|
| <img src="assets/chromecast-icon.png"> | [Chromecast v3.x 用 Media SDK](../../getting-started/download-sdks.md#over-the-top-implementation-download-ott-libraries) |
| <img src="assets/roku-icon.png"> | [Roku v2.x 用 Media SDK](../../getting-started/download-sdks.md#over-the-top-implementation-download-ott-libraries) |


## 追加情報

サポートされるデバイスとプラットフォームについて詳しくは、[サポートされるデバイスとプラットフォーム](/help/getting-started/supported-devices.md)を参照してください。

SDK をダウンロードするには、[Media SDKs、タグを使用した拡張機能、OTT SDK の取得](/help/getting-started/download-sdks.md)を参照してください。
