---
title: 実装パス
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0bc3928b8e3076feb8e9a16e005cd0415f723408
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 64%

---


# 実装パス {#implementation-paths}

Media Analyticsには一意のSKUがあり、サーバー呼び出しに基づく価格モデルからビデオストリームに基づくモデルに変更があるので、導入パスごとに、顧客は担当の営業またはアカウントマネージャーに連絡して、新しい販売注文に署名する必要があります。

* **Adobe Media Analytics拡張機能を使用したAdobe Launch**

   Adobe Launchは、アドビが提供する次世代のタグ管理ソリューションです。 Launchは、関連する顧客エクスペリエンスを強化するために必要なすべての解析、マーケティングおよび広告タグを、シンプルにデプロイおよび管理する方法を提供します。 独自のLaunchとの統合を構築し、維持するには、拡張機能を使用します。 拡張機能は、JavaScript、HTML、CSSパッケージで、起動UIとクライアント機能を拡張します。 詳しくは、『 [Experience Platform Launch User Guide』を参照してください](https://docs.adobe.com/content/help/ja-JP/launch/using/overview.html)

   Adobe Media Analytics(MA)の拡張機能により、オーディオおよびビデオ用のコアJavaScript Media SDK(Media 2.x SDK)が追加されます。 この拡張機能では、Launch サイトまたはプロジェクトに `MediaHeartbeat` トラッカーインスタンスを追加する機能を提供します。

   Media Analytics拡張機能を使用したAdobe Launchでは、以下が必要です。
   * Adobe Experience Cloudのお客様である必要があります。
   * LaunchまたはDTM埋め込みコードをWebページにデプロイする必要があります。
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

TVSDK は既に Media Analtyics（ハートビート）SDK と統合されているので、サポートされているすべてのプラットフォームと簡単かつ迅速に統合することができます。<!--Primetime also supports the partnership with Nielsen.--> Primetime を最大限に活用するには、[クライアント側](/help/intro-to-ava/implementation-paths/client-side-path.md)に記載されているのと同じガイドラインおよび前提条件に従うと共に、お使いのプラットフォームの [Primetime ユーザーガイド](https://helpx.adobe.com/jp/primetime/user-guide.html)を参照してください。

また、営業担当者またはアカウントマネージャーに連絡して、TVSDK 購入に何が必要かをお問い合わせください。
