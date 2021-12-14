---
title: 使用可能なストリーミングメディア実装パスを教えてください。
description: Adobe Experience Platformのデータ収集を含む、Adobeストリーミングメディアの実装パスについて説明します。
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f88e8b02bc9723793822fa7647a2ceab9ada45e6
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 79%

---

# 実装パス {#implementation-paths}

Streaming Media Analytics には独自の SKU があり、サーバー呼び出しに基づく価格モデルからビデオのストリーミングに基づくモデルへと変更されているので、お客様は実装パスごとに営業担当者またはアカウントマネージャーに連絡して新たに販売契約を結ぶ必要があります。

## Analytics 拡張機能を使用したAdobe Experience PlatformAdobe Medium収集

>[!NOTE]
>Adobe Experience Platform Launch は、Experience Platform のデータ収集テクノロジースイートとしてリブランドされています。その結果、製品ドキュメント全体でいくつかの用語の変更がロールアウトされました。用語の変更点の一覧については、次の[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ja)を参照してください。


Adobe Experience Platform のタグは、Adobe が提供する次世代のタグ管理機能です。タグを使用すると、関連する顧客体験を強化するために必要なすべての分析、マーケティング、広告などのタグを、簡単にデプロイして管理できます。タグは、Adobe Experience Cloudのお客様に、付属の付加価値機能として提供されます。

タグを使用すると、誰でも拡張機能と呼ばれる独自の統合を作成して使用できます。これらの拡張機能は、Adobe Experience Cloudのお客様自身がアプリストアで利用できるので、タグをすばやくインストール、設定およびデプロイできます。

拡張機能は、タグの機能を拡張するコード（JavaScript、HTML、CSS）のパッケージです。ほぼセルフサービスのインターフェイスを使用して、統合を作成、管理、更新できます。拡張機能は、タスクの遂行に使用するアプリと考えることができます。詳しくは、 *タグの概要* 記事内の [Adobe Experience Platform Documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)

Adobe Media Analytics（MA）の拡張機能により、オーディオおよびビデオ用のコア JavaScript Media SDK（Media 2.x SDK）が追加されます。この拡張機能では、 `MediaHeartbeat` トラッカーインスタンスをデータ収集サイトまたはプロジェクトに追加します。

Media Analytics 拡張機能を使用したAdobeデータ収集には、以下が必要です。
* Adobe Experience Cloud のお客様である必要があります。
* Web ページにデータ収集または DTM 埋め込みコードをデプロイする必要があります。
* [Analytics 拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=ja)
* [Experience Cloud ID 拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=ja)


## クライアント側

これらは Media Analytics のみの統合です。 ビデオハートビート SDK やメディアコレクション API 統合を選択できます。このパスは、Brightcove、Ooyala、Platform など、顧客や OVP プレーヤーを含む任意のビデオプレーヤーで使用できます。

Media Analytics が目的のパスの場合は、[メディア SDK の実装](/help/sdk-implement/setup/setup-overview.md)および[メディアコレクション API](/help/media-collection-api/mc-api-overview.md) を参照してください。

>[!IMPORTANT]
>Media Analytics を使用するには、Adobe Analytics も使用する必要があります。

## Adobe Primetime

Adobe Primetime は、コンテンツプログラマーやディストリビューターが、接続されたすべての画面でメディアを収益化できるようにする Adobe Experience Cloud ソリューションです。

Primetime は、ビデオパブリッシング、広告、パーソナライゼーション、アナリティクス用のモジュール式プラットフォームを提供することで、各種デバイスをまたぐグローバルオーディエンスへのリーチ、収益化、活性化における複雑性を軽減します。さらに、Primetime オファーは、次の点に関するソリューションと価値を提供します。

* 線形および VOD コンテンツタイプの正確な測定のサポート。
* 動的な広告挿入を使用する（または使用しない）広告ブレークの測定をサポートします。
* TVSDK のシームレスな広告挿入モデルを使用すると、広告の再生を直接測定する分析が可能になり、精度が向上します。
* 充実したイベントとメタデータが、QoS バッファー、モバイル接続中断の問題、エンドユーザーのインタラクション（モバイルでのシーク、一時停止、バックグラウンド実行など）に関する正確性を保ちます。
* ID3 メタデータを使用する Nielsen DTVR（線形）および CMS メタデータを使用する DCR の統合サポート。


TVSDK は既に Media Analtyics（ハートビート）SDK と統合されているので、サポートされているすべてのプラットフォームと簡単かつ迅速に統合することができます。 Primetime を最大限に活用するには、[クライアント側](/help/intro-to-ava/implementation-paths/client-side-path.md)に記載されているのと同じガイドラインおよび前提条件に従うと共に、お使いのプラットフォームの [Primetime ユーザーガイド](https://helpx.adobe.com/jp/support/primetime.html)を参照してください。

また、営業担当者またはアカウントマネージャーに連絡して、TVSDK 購入に何が必要かをお問い合わせください。
