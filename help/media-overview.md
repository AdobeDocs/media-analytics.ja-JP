---
title: Adobe Analytics for Streaming Media の概要
description: ストリーミングメディア分析を使用すると、コンテンツ、オーディオおよび広告に関する強力なインサイトを得ることができます。
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 355b3b079d53ae8e83822f61fc79e60e47f6d715
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 72%

---

# Adobe Analytics for Streaming Media の概要

![バナー](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media は、オーディオ、ビデオおよび広告用の強力な測定ツールを提供する Adobe Analytics のアドオンです。ストリーミングメディア用 Analyticsを使用すると、ビデオとオーディオの指標を評価および組み合わせることができる、ほぼリアルタイムできめ細かい期間、停止および開始の詳細を取得できます。 これらのインサイトにより、顧客の視聴習慣を把握し、高度にパーソナライズされたレコメンデーションでエンゲージメントを強化できます。

Adobe Analytics for Streaming Media を使用すれば、サイトやストリーミングアプリ全体での完全なカスタマージャーニーを追跡できます。Streaming Media 指標を、Audience Analytics、モバイル分析、クロスデバイス分析などの他の Adobe Analytics 機能と組み合わせることができます。この指標は、Adobe Analytics Reports や他の Adobe Experience Platform 製品と容易に統合できます。メディア測定を使用すれば、データを複数のディメンションやセグメントに分類し、完全で詳細な分析をおこなうのに必要なメタデータをすべてキャプチャできます。その後、データを分析し、成功基準を、完全に消費されたメディア、平均滞在時間、完了した広告に関連付けることができます。

ドロップフレーム数、バッファリングに費やされた時間、平均ビットレートなど、エクスペリエンスの品質（QoE）に関する重要な配信指標を測定できます。また、この指標を web サイトやアプリのデータと組み合わせて、顧客のパスや関心を視覚化し、Adobe Experience Platform を使用してレコメンデーションの強化やエクスペリエンスのパーソナライズを実現できます。

## 仕組み

ストリーミングメディアトラッキングデータは、Media for Edge Network SDK/Extension、タグ付きメディア拡張機能、メディア SDK、メディアエッジ API、メディアコレクション API のいずれかを使用して、プレーヤーから収集されます。

すべての詳細なデータ（最大 10 秒）が、( [実装方法](/help/implementation/overview.md) ( ) を選択し、個々の再生セッションごとにデータを収集して処理します。

再生セッションが終了した後、計算されたトラッキングデータは、保存とレポート作成のためにAdobe AnalyticsまたはCustomer Journey Analyticsに送信されます。

>[!NOTE]
>
>Customer Journey Analyticsの実装では、Experience Edge を使用するか、Analytics Data Connector(ADC) を使用して、データをCustomer Journey Analyticsに送信できます。


詳しくは、 [ストリーミングメディアのAdobe AnalyticsまたはCustomer Journey Analyticsへの実装](/help/implementation/overview.md) を参照してください。

## 機能

Adobe Analytics for Streaming Media のメリットには、リアルタイム監視、詳細分析、施策につながるインサイト、収益化の機会などがあります。

* **リアルタイム分析**：複数のチャネルにわたり、メディア開始などの主要パフォーマンス指標を利用して、アクションにつながる意思決定をリアルタイムで行います。

* **エンゲージメントの促進**：バッファリングイベントを減らしコンテンツ内で広告を再生する場所とタイミングを把握することによりユーザーエンゲージメントを強化して、繰り返し訪問を実現する、押し付けがましくないスムーズなエクスペリエンスを提供します。

* **全体像の把握**：すべてのコンテンツディストリビューターにわたる複数のデータポイントを統合して、すべてのメディアアクティビティの全体像を把握します。Federated Analytics 機能を通じて、可能なあらゆるチャネルにわたるエンゲージメントと視聴を測定します。

* **精度の向上**：個々の訪問者の時間帯や分単位の同時視聴者数、コンテンツの平均視聴時間など、非常に詳細なレベルで視聴行動を評価します。

* **正確な計測**：OTT、スマートフォン、タブレット、デスクトップなど、メディア視聴に使用されたあらゆるデバイス全体でデータを計測し、利用状況のパターンや傾向を監視します。

* **セグメント化**：プレーヤー、デバイス、ジャンル、チャプターおよび番組に分類を適用し、全体的な視聴回数、コンテンツ、オーディオおよび広告（またはその組み合わせ）に対するそれぞれの影響度を把握します。
