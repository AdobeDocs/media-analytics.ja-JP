---
title: 測定のオプション
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 47b4c7fe09da0d38c8faae1c3b4293ce48552bdc

---


# 測定のオプション

Adobe Media Analytics拡張機能、メディアSDK、またはメディアコレクションAPIを備えたAdobe Launchを使用して、オーディオおよびビデオのトラッキングを有効にできます。

## Adobe Media Analytics拡張機能を使用したAdobe Launch

Adobe Launchは、アドビが提供する次世代のタグ管理ソリューションです。 Launchは、関連する顧客エクスペリエンスを強化するために必要なすべての解析、マーケティングおよび広告タグを、シンプルにデプロイおよび管理する方法を提供します。 独自のLaunchとの統合を構築し、維持するには、拡張機能を使用します。 拡張機能は、JavaScript、HTML、CSSパッケージで、起動UIとクライアント機能を拡張します。 詳しくは、『 [Experience Platform Launch User Guide』を参照してください](https://docs.adobe.com/content/help/ja-JP/launch/using/overview.html)

Adobe Media Analytics(MA)の拡張機能により、オーディオおよびビデオ用のコアJavaScript Media SDK(Media 2.x SDK)が追加されます。 この拡張機能では、Launch サイトまたはプロジェクトに `MediaHeartbeat` トラッカーインスタンスを追加する機能を提供します。

Media Analytics拡張機能を使用したAdobe Launchでは、以下が必要です。
* Adobe Experience Cloudのお客様である必要があります。
* LaunchまたはDTM埋め込みコードをWebページにデプロイする必要があります。
* [Analytics 拡張機能](https://docs.adobe.com/content/help/ja-JP/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID 拡張機能](https://docs.adobe.com/content/help/ja-JP/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## メディア SDK

Media SDKは、最も一般的に使用されるメディアプレイヤーと統合されます。

## メディアコレクションAPI(RESTful API)

SDKをサポートしていないプレーヤー、またはSDK統合が不要な場合に統合します。<br>v2.2.0リリース以降、オーディオおよびビデオトラッキングをサポートするため、ビデオハートビートライブラリ(VHL)SDKの名前がMedia Analytics SDKに変更されました。 Media 2.2.0 SDKは、VHL 2.x SDKシリーズと完全に下位互換性があります。 名前の変更は、命名規則の変更に過ぎず、機能の変更を表すものではありません。
