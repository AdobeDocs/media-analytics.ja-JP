---
title: 使用可能なストリーミングメディア実装パスを教えてください。
description: Adobe Experience Platform のデータ収集を含む、Adobe Streaming Media の実装パスについて説明します。
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 9ba64b68efec5dd8b52010ac1a13afd7703448d0
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 98%

---

# 実装パス {#implementation-paths}

**このコンテンツは現在の実装パスファイルに移動されました**

Streaming Media Analytics には独自の SKU があり、サーバー呼び出しに基づく価格モデルからビデオのストリーミングに基づくモデルに変更されるため、顧客は実装パスごとに営業担当者／アカウントマネージャーに連絡して新しい販売注文にサインする必要があります。

## Adobe Media Analytics 拡張機能を使用した Adobe Experience Platform のデータ収集

>[!NOTE]
>Adobe Experience Platform Launch は、Experience Platform のデータ収集テクノロジースイートとしてリブランドされています。その結果、製品ドキュメント全体でいくつかの用語の変更がロールアウトされました。用語の変更点の一覧については、次の[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ja)を参照してください。


Adobe Experience Platform のタグは、Adobe が提供する次世代のタグ管理機能です。タグを使用すると、関連する顧客体験を強化するために必要なすべての分析、マーケティング、広告などのタグを、簡単にデプロイして管理できます。タグは、標準装備の付加価値機能として Adobe Experience Cloud のお客様に提供されます。

タグを使用すると、拡張機能と呼ばれる独自の統合機能を誰でも構築および維持できます。これらの拡張機能は、Adobe Experience Cloud のお客様がアプリストアエクスペリエンスで利用できるため、タグを迅速にインストール、設定およびデプロイできます。

拡張機能は、タグの機能を拡張するコード（JavaScript、HTML、CSS）のパッケージです。ほぼセルフサービスのインターフェイスを使用して、統合を作成、管理、更新できます。拡張機能は、タスクを実行するために使用するアプリのようなものです。詳しくは、[Adobe Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)の&#x200B;*タグの概要*&#x200B;の記事を参照してください。

Adobe Media Analytics（MA）の拡張機能により、オーディオおよびビデオ用のコア JavaScript Media SDK（Media 2.x SDK）が追加されます。この拡張機能では、データ収集サイトまたはプロジェクトに `MediaHeartbeat` トラッカーインスタンスを追加する機能を提供します。

Media Analytics 拡張機能を備えた Adobe Data Collection では、以下が必要です。
* Adobe Experience Cloud のお客様である必要があります。
* Web ページにデータ収集または DTM 埋め込みコードをデプロイする必要があります。
* [Analytics 拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=ja)
* [Experience Cloud ID 拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=ja)


## クライアントサイド

Media Analytics のみの統合です。ビデオハートビート SDK やメディアコレクション API 統合を選択できます。このパスは、Brightcove、Ooyala、Platform など、顧客や OVP プレーヤーを含む任意のビデオプレーヤーで使用できます。

Media Analytics が目的のパスの場合は、[メディア SDK の実装](/help/legacy/setup/legacy-setup-overview.md)および[メディアコレクション API](/help/implementation/media-collection-api/mc-api-overview.md) を参照してください。

>[!IMPORTANT]
>Media Analytics を使用するには、Adobe Analytics も使用する必要があります。

## Adobe Primetime

Adobe Primetime は、コンテンツのプログラマーや提供者が、接続されたすべての画面でメディアを収益化することを支援する Adobe Experience Cloud ソリューションです。

Primetime は、ビデオパブリッシング、広告、パーソナライゼーション、アナリティクス用のモジュール式プラットフォームを提供することで、各種デバイスをまたぐグローバルオーディエンスへのリーチ、収益化、活性化における複雑性を軽減します。さらに、Primetime オファーは、次の点に関するソリューションと価値を提供します。

* 線形および VOD コンテンツタイプの正確な測定のサポート。
* 動的な広告挿入を使用する（または使用しない）広告ブレークの測定をサポートします。
* TVSDK のシームレスな広告挿入モデルを使用すると、広告の再生を直接測定する分析が可能になり、精度が向上します。
* 充実したイベントとメタデータが、QoS バッファー、モバイル接続中断の問題、エンドユーザーのインタラクション（モバイルでのシーク、一時停止、バックグラウンド実行など）に関する正確性を保ちます。
* ID3 メタデータを使用する Nielsen DTVR（線形）および CMS メタデータを使用する DCR の統合サポート。


TVSDK は既に Media Analytics（Heartbeats）SDK と統合されており、サポートされているすべてのプラットフォームで、簡単かつ迅速に実装できます。Primetime を活用するには、[クライアントサイド](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md)に記載されているガイドライン、前提条件およびプラットフォームに関するドキュメント「[Primetime ユーザーガイド](https://helpx.adobe.com/jp/support/primetime.html)」に従ってください。

また、TVSDK を購入するために必要なことについては、営業担当者またはアカウントマネージャーにもお問い合わせください。
