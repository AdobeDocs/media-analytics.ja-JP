---
title: 実装パス
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 実装パス {#implementation-paths}

Media Analytics（ハートビート）は、アドビの標準化されたビデオソリューションです。従来のアドビのマイルストーンモデルの後継モデルです。

Media Analytics には独自の SKU があり、サーバー呼び出しに基づく価格モデルからビデオのストリーミングに基づくモデルに変更されているので、実装パスごとにお客様は営業担当者またはアカウントマネージャーに連絡して新たに販売契約を結ぶ必要があります。

* **クライアント側 -** これは Media Analytics のみの統合です。ビデオハートビート SDK やメディアコレクション API の統合を選択できます。このパスは、お客様のプレーヤーや、Brightcove、Ooyala、thePlatform などの OVP プレーヤーで使用できます。

   Media Analytics が目的のパスの場合は、[メディア SDK の実装](/help/sdk-implement/setup/setup-overview.md)および[メディアコレクション API](/help/media-collection-api/mc-api-overview.md) を参照してください。

   >[!IMPORTANT]
   >
   >Media Analytics を使用するには、Adobe Analytics も使用する必要があります。

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch は Dynamic Tag Management の後継製品で、各プレーヤーへのビデオトラッキングの実装を容易にする Media Analytics Launch 拡張機能を備えています。

   Experience Platform Launch について詳しくは、[Adobe Media Analytics for Audio and Video 拡張機能](https://docs.adobe.com/content/help/ja-JP/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)を参照してください。
* **Adobe Primetime -** Adobe Primetime は、コンテンツプログラマーやディストリビューターが、接続されたすべての画面でメディアを収益化できるようにする Adobe Experience Cloud ソリューションです。

   Primetime は、ビデオパブリッシング、広告、パーソナライゼーション、アナリティクス用のモジュール式プラットフォームを提供することで、各種デバイスをまたぐグローバルオーディエンスへのリーチ、収益化、活性化における複雑性を軽減します。また、Primetime は以下を中心としたソリューションと価値を提供します。

   * 線形および VOD コンテンツタイプの正確な測定のサポート。
   * 動的広告挿入を使用した（または使用しない）広告ブレーク測定のサポート。
   * TVSDK のシームレスな広告挿入モデルにより、広告再生の直接測定が可能になり、精度が向上します。
   * 充実したイベントとメタデータが、QoS バッファー、モバイル接続中断の問題、エンドユーザーのインタラクション（モバイルでのシーク、一時停止、バックグラウンド実行など）に関する正確性を保ちます。
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK は既に Media Analtyics（ハートビート）SDK と統合されているので、サポートされているすべてのプラットフォームと簡単かつ迅速に統合することができます。<!--Primetime also supports the partnership with Nielsen.--> Primetime を最大限に活用するには、[クライアント側](/help/intro-to-ava/implementation-paths/client-side-path.md)に記載されているのと同じガイドラインおよび前提条件に従うと共に、お使いのプラットフォームの [Primetime ユーザーガイド](https://helpx.adobe.com/jp/primetime/user-guide.html)を参照してください。

また、営業担当者またはアカウントマネージャーに連絡して、TVSDK 購入に何が必要かをお問い合わせください。
