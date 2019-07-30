---
seo-title: 実装パス
title: 実装パス
uuid: 8400c938- e77e-4c88- b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 実装パス {#implementation-paths}

Media Analytics（ハートビート）は、アドビの標準化されたビデオソリューションです。従来のアドビのマイルストーンモデルの後継モデルです。

これらの実装パスごとに、お客様は、新しい販売注文をMedia Analyticsに連絡する必要があります。これには、新しいSKUと、ビデオストリームに基づくモデルへのサーバーコールに基づく価格モデルからの変更に関する、新しいSKUおよび価格モデルへの変更が必要です。

* **クライアント側-** これらはMedia Analyticsのみの統合です。ビデオハートビート SDK やメディアコレクション API の統合を選択できます。このパスは、お客様のプレーヤーや、Brightcove、Ooyala、thePlatform などの OVP プレーヤーで使用できます。

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Media Analyticsを使用するには、Adobe Analyticsも使用する必要があります。

* **Adobe Experience Platform Launch-** Adobe Experience Platform Launch（継続製品のDynamic Tag Management）を使用すると、プレーヤーでビデオトラッキングを導入するためのMedia Analytics Launch Extension機能を利用できます。

   You can learn more about Experience Platform Launch here: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime-** Adobe Primetimeは、コンテンツプログラマーや販売店が接続されたすべての画面でメディアを収益化するためのAdobe Experience Cloudソリューションです。

   Primetime は、ビデオパブリッシング、広告、パーソナライゼーション、アナリティクス用のモジュール式プラットフォームを提供することで、各種デバイスをまたぐグローバルオーディエンスへのリーチ、収益化、活性化における複雑性を軽減します。また、Primetime は以下を中心としたソリューションと価値を提供します。

   * 線形および VOD コンテンツタイプの正確な測定のサポート。
   * 動的広告挿入を使用した（または使用しない）広告ブレーク測定のサポート。
   * TVSDK のシームレスな広告挿入モデルにより、広告再生の直接測定が可能になり、精度が向上します。
   * 充実したイベントとメタデータが、QoS バッファー、モバイル接続中断の問題、エンドユーザーのインタラクション（モバイルでのシーク、一時停止、バックグラウンド実行など）に関する正確性を保ちます。
   * ID3 メタデータを使用する Nielsen DTVR（線形）および CMS メタデータを使用する DCR の統合サポート。
   TVSDKは、既にMedia Analtyics（ハートビート） SDKと統合されており、サポートされているすべてのプラットフォームで、実装をより簡単かつ高速に実行できます。また、Primetime は Nielsen とのパートナーシップをサポートしています。Primetime を最大限に活用するには、以下に挙げる各プラットフォームのドキュメントに加え、[クライアント側](/help/intro-to-ava/implementation-paths/client-side-path.md)に記載されているガイドラインと前提条件を参照してください。[Primetimeユーザーガイドを参照してください。](https://helpx.adobe.com/primetime/user-guide.html)

   また、営業担当者またはアカウントマネージャーに連絡して、TVSDK 購入に何が必要かをお問い合わせください。
