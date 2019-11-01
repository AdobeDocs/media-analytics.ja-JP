---
title: 実装パス
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 実装パス {#implementation-paths}

Media Analytics（ハートビート）は、アドビの標準化されたビデオソリューションです。 従来のアドビのマイルストーンモデルの後継モデルです。

Media Analyticsには一意のSKUがあり、ビデオストリームに基づくサーバーコールに基づく価格モデルからの変更があるので、これらの各実装パスについて、顧客は担当の営業またはアカウントマネージャーに連絡して新しい販売注文に署名する必要があります。

* **クライアント側 —** Media Analytics専用の統合です。 ビデオハートビート SDK やメディアコレクション API の統合を選択できます。このパスは、お客様のプレーヤーや、Brightcove、Ooyala、thePlatform などの OVP プレーヤーで使用できます。

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Media Analyticsを使用するには、Adobe Analyticsも使用する必要があります。

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launchは、Dynamic Tag Managementの後継製品で、プレーヤーへのビデオトラッキングの導入を容易にするMedia Analytics Launch Extensionを備えています。

   エクスペリエンスプラットフォームの発表について詳しくは、以下を参照してください。オー [ディオおよびビデオ拡張用Adobe Media Analytics](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
* **Adobe Primetime -** Adobe Primetimeは、接続されたすべての画面でコンテンツプログラマーや配布者がメディアを収益化するのに役立つAdobe Experience cloudソリューションです。

   Primetime は、ビデオパブリッシング、広告、パーソナライゼーション、アナリティクス用のモジュール式プラットフォームを提供することで、各種デバイスをまたぐグローバルオーディエンスへのリーチ、収益化、活性化における複雑性を軽減します。また、Primetime は以下を中心としたソリューションと価値を提供します。

   * 線形および VOD コンテンツタイプの正確な測定のサポート。
   * 動的広告挿入を使用した（または使用しない）広告ブレーク測定のサポート。
   * TVSDK のシームレスな広告挿入モデルにより、広告再生の直接測定が可能になり、精度が向上します。
   * 充実したイベントとメタデータが、QoS バッファー、モバイル接続中断の問題、エンドユーザーのインタラクション（モバイルでのシーク、一時停止、バックグラウンド実行など）に関する正確性を保ちます。
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDKは、Media Analytics（ハートビート）SDKと既に統合されています。これにより、サポートされるすべてのプラットフォームで実装がより簡単で高速になります。 <!--Primetime also supports the partnership with Nielsen.--> Primetimeを活用するには、お使いのプラットフォームに関する以下のドキュメントと共に、 [クライアント](/help/intro-to-ava/implementation-paths/client-side-path.md) 側で見つかったのと同じガイドラインおよび前提条件に従ってください。Primetimeユ [ーザーガイドを参照してください。](https://helpx.adobe.com/primetime/user-guide.html)

また、営業担当者またはアカウントマネージャーに連絡して、TVSDK 購入に何が必要かをお問い合わせください。
