---
title: 実装パス
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: ht
source-git-commit: 0bc3928b8e3076feb8e9a16e005cd0415f723408
workflow-type: ht
source-wordcount: '489'
ht-degree: 100%

---


# 実装パス {#implementation-paths}

Media Analytics には独自の SKU があり、サーバー呼び出しに基づく価格モデルからビデオのストリーミングに基づくモデルに変更されているので、実装パスごとにお客様は営業担当者またはアカウントマネージャーに連絡して新たに販売契約を結ぶ必要があります。

* **Adobe Media Analytics 拡張機能を備えた Adobe Launch**

   Launch は、アドビが提供する次世代タグ管理ソリューションです。Launch は、顧客体験の実現に必要なすべての分析、マーケティングおよび広告のタグをデプロイおよび管理するためのシンプルな手段を提供します。Launch との統合を構築して維持するには、拡張機能を使用します。拡張機能は、Launch UI とクライアント機能を拡張する JavaScript、HTML および CSS のパッケージです。詳しくは、[Experience Platform Launch ユーザーガイド](https://docs.adobe.com/content/help/ja-JP/launch/using/overview.html)を参照してください

   Adobe Media Analytics（MA）の拡張機能により、オーディオおよびビデオ用のコア JavaScript Media SDK（Media 2.x SDK）が追加されます。この拡張機能では、Launch サイトまたはプロジェクトに `MediaHeartbeat` トラッカーインスタンスを追加する機能を提供します。

   Media Analytics 拡張機能を備えた Adobe Launch では、以下が必要です。
   * Adobe Experience Cloud のお客様である必要があります。
   * Web ページに Launch または DTM 埋め込みコードをデプロイする必要があります。
   * [Analytics 拡張機能](https://docs.adobe.com/content/help/ja-JP/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Experience Cloud ID 拡張機能](https://docs.adobe.com/content/help/ja-JP/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **クライアントサイド -** これは Media Analytics のみの統合です。ビデオハートビート SDK やメディアコレクション API 統合を選択できます。このパスは、Brightcove、Ooyala、Platform など、顧客や OVP プレーヤーを含む任意のビデオプレーヤーで使用できます。

   Media Analytics が目的のパスの場合は、[メディア SDK の実装](/help/sdk-implement/setup/setup-overview.md)および[メディアコレクション API](/help/media-collection-api/mc-api-overview.md) を参照してください。

   >[!IMPORTANT]
   >
   >Media Analytics を使用するには、Adobe Analytics も使用する必要があります。

* **Adobe Primetime -** Adobe Primetime は、コンテンツプログラマーやディストリビューターが、接続されたすべての画面でメディアを収益化できるようにする Adobe Experience Cloud ソリューションです。

   Primetime は、ビデオパブリッシング、広告、パーソナライゼーション、アナリティクス用のモジュール式プラットフォームを提供することで、各種デバイスをまたぐグローバルオーディエンスへのリーチ、収益化、活性化における複雑性を軽減します。さらに、Primetime オファーは、次の点に関するソリューションと価値を提供します。

   * 線形および VOD コンテンツタイプの正確な測定のサポート。
   * 動的な広告挿入を使用する（または使用しない）広告ブレークの測定をサポートします。
   * TVSDK のシームレスな広告挿入モデルを使用すると、広告の再生を直接測定する分析が可能になり、精度が向上します。
   * 充実したイベントとメタデータが、QoS バッファー、モバイル接続中断の問題、エンドユーザーのインタラクション（モバイルでのシーク、一時停止、バックグラウンド実行など）に関する正確性を保ちます。
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK は既に Media Analtyics（ハートビート）SDK と統合されているので、サポートされているすべてのプラットフォームと簡単かつ迅速に統合することができます。<!--Primetime also supports the partnership with Nielsen.--> Primetime を最大限に活用するには、[クライアント側](/help/intro-to-ava/implementation-paths/client-side-path.md)に記載されているのと同じガイドラインおよび前提条件に従うと共に、お使いのプラットフォームの [Primetime ユーザーガイド](https://helpx.adobe.com/jp/support/primetime.html)を参照してください。

また、営業担当者またはアカウントマネージャーに連絡して、TVSDK 購入に何が必要かをお問い合わせください。
