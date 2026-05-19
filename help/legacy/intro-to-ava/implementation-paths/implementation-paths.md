---
title: 使用可能なストリーミングメディア実装パスを教えてください。
description: Adobe Experience Platform のデータ収集を含む、Adobe Streaming Media の実装パスについて説明します。
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/U9PBQc7dHNmONZc06t1Xi7EITkveGUkzcst6Sakqqzo
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 676
ht-degree: 87%

---

# 実装パス {#implementation-paths}

**このコンテンツは現在の実装パスファイルに移動されました**

Customer Journey Analytics Streaming Media CollectionおよびAdobe Analytics for Streaming Mediaには、固有のSKUと、サーバーコールに基づく価格モデルからビデオストリームに基づくモデルへの変更があるため、実装パスごとに、セールス担当者またはAdobe アカウントチームに連絡して、新しいセールスオーダーに署名する必要があります。

## Adobe Media Analytics 拡張機能を使用した Adobe Experience Platform のデータ収集

>[!NOTE]
>Adobe Experience Platform Launch は、Experience Platform のデータ収集テクノロジースイートとしてリブランドされています。 その結果、製品ドキュメント全体でいくつかの用語の変更がロールアウトされました。 用語の変更点の一覧については、次の[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ja)を参照してください。


Adobe Experience Platform のタグは、Adobe が提供する次世代のタグ管理機能です。 タグを使用すると、関連する顧客体験を強化するために必要なすべての分析、マーケティング、広告などのタグを、簡単にデプロイして管理できます。 タグは、標準装備の付加価値機能として Adobe Experience Cloud のお客様に提供されます。

タグを使用すると、拡張機能と呼ばれる独自の統合機能を誰でも構築および維持できます。 これらの拡張機能は、Adobe Experience Cloud のお客様がアプリストアエクスペリエンスで利用できるため、タグを迅速にインストール、設定およびデプロイできます。

拡張機能は、タグの機能を拡張するコード（JavaScript、HTML、CSS）のパッケージです。 ほぼセルフサービスのインターフェイスを使用して、統合を作成、管理、更新できます。 拡張機能は、タスクを実現するために使用するアプリと考えることができます。詳しくは、[Adobe Experience Platform ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)の「*Tags overview*」を参照してください

Adobe Media Analytics（MA）の拡張機能により、オーディオおよびビデオ用のコア JavaScript Media SDK（Media 2.x SDK）が追加されます。 この拡張機能では、データ収集サイトまたはプロジェクトに `MediaHeartbeat` トラッカーインスタンスを追加する機能を提供します。

Media Analytics 拡張機能を備えた Adobe Data Collection では、以下が必要です。
* Adobe Experience Cloud のお客様である必要があります。
* Web ページにデータ収集または DTM 埋め込みコードをデプロイする必要があります。
* [Analytics 拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=ja)
* [Experience Cloud ID 拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=ja)


## クライアントサイド

Media Analytics のみの統合です。 ビデオハートビート SDK やメディアコレクション API 統合を選択できます。 このパスは、Brightcove、Ooyala、Platform など、顧客や OVP プレーヤーを含む任意のビデオプレーヤーで使用できます。

Media Analytics が目的のパスの場合は、[メディア SDK の実装](/help/legacy/setup/legacy-setup-overview.md)および[メディアコレクション API](/help/implementation/media-collection-api/mc-api-overview.md) を参照してください。

>[!IMPORTANT]
>Media Analytics を使用するには、Adobe Analytics も使用する必要があります。

## Adobe Primetime

Adobe Primetime は、接続されたすべての画面でメディアを収益化できるようコンテンツのプログラマーや提供者を支援する 、Adobe Experience Cloud ソリューションです。

Primetime は、ビデオパブリッシング、広告、パーソナライゼーション、アナリティクス用のモジュール式プラットフォームを提供することで、各種デバイスをまたぐグローバルオーディエンスへのリーチ、収益化、活性化における複雑性を軽減します。 さらに、Primetime オファーは、次の点に関するソリューションと価値を提供します。

* 線形および VOD コンテンツタイプの正確な測定のサポート。
* 動的な広告挿入を使用する（または使用しない）広告ブレークの測定をサポートします。
* TVSDK のシームレスな広告挿入モデルを使用すると、広告の再生を直接測定する分析が可能になり、精度が向上します。
* 充実したイベントとメタデータが、QoS バッファー、モバイル接続中断の問題、エンドユーザーのインタラクション（モバイルでのシーク、一時停止、バックグラウンド実行など）に関する正確性を保ちます。
* Nielsen DTVR （linear）のID3 メタデータとDCRのCMSメタデータの統合サポート。


TVSDK は既に Media Analytics（Heartbeats）SDK と統合されており、サポートされているすべてのプラットフォームで、簡単かつ迅速に実装できます。 Primetime を活用するには、[クライアントサイド](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md)に記載されているガイドライン、前提条件およびプラットフォームに関するドキュメント「[Primetime ユーザーガイド](https://helpx.adobe.com/jp/support/primetime.html)」に従ってください。

また、TVSDK を購入するために必要なことについては、営業担当者またはアカウントマネージャーにもお問い合わせください。
