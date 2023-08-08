---
title: Adobe Analytics for Streaming Media の概要
description: ストリーミングメディア分析を使用すると、コンテンツ、オーディオおよび広告に関する強力なインサイトを得ることができます。
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: ht
source-wordcount: '590'
ht-degree: 100%

---

# ストリーミングメディア用 Adobe Analytics の概要

![バナー](./assets/media_analytics_banner.png)

ストリーミングメディア用 Adobe Analytics は、オーディオ、ビデオおよび広告用の強力な測定ツールを提供します。Streaming Media 指標を、Audience Analytics、モバイル分析、クロスデバイス分析などの他の Adobe Analytics 機能と組み合わせることができます。

ストリーミングメディアは、Adobe Analytics<!-- update this when SKUs are available for other AEP products --> のアドオンとして購入でき、ストリーミングメディアの指標は、次の Adobe Experience Platform 製品に簡単に統合できます。

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Adobe Analytics ストリーミングメディアを実装するには、アドビ営業担当またはアドビのアカウントチームに連絡して、ストリーミングメディアが製品ポートフォリオに含まれていることを確認してください。

## 主な特長

ストリーミングメディア用 Adobe Analytics のメリットには、リアルタイム監視、詳細分析、実用的なインサイト、収益化の機会などが含まれます。

* **リアルタイム分析**：複数のチャネルにわたり、メディア開始などの主要パフォーマンス指標を利用して、アクションにつながる意思決定をリアルタイムで行います。

  ストリーミングメディア用 Analyticsを使用すると、ビデオ指標とオーディオ指標を評価および組み合わせることができる、期間、停止および開始に関するほぼリアルタイムのきめ細かい詳細情報を取得できます。これらのインサイトにより、顧客の視聴習慣を把握し、高度にパーソナライズされたレコメンデーションでエンゲージメントを強化できます。

* **エンゲージメントの促進**：バッファリングイベントを減らしコンテンツ内で広告を再生する場所とタイミングを把握することによりユーザーエンゲージメントを強化して、繰り返し訪問を実現する、押し付けがましくないスムーズなエクスペリエンスを提供します。

* **全体像の把握**：すべてのコンテンツディストリビューターにわたる複数のデータポイントを統合して、すべてのメディアアクティビティの全体像を把握します。可能なあらゆるチャネルにわたるエンゲージメントと視聴を測定します。

  ストリーミングメディア用 Adobe Analytics を使用すると、サイトとストリーミングアプリ全体のカスタマージャーニーを完全に追跡して、顧客のパスや関心を視覚化し、レコメンデーションの強化や顧客体験のパーソナライズを実現できます。メディア測定を使用すれば、データを複数のディメンションやセグメントに分類し、完全で詳細な分析をおこなうのに必要なメタデータをすべてキャプチャできます。その後、データを分析し、成功基準を、完全に消費されたメディア、平均滞在時間、完了した広告に関連付けることができます。

* **重要な指標**：ドロップフレーム数、バッファリングに費やされた時間、平均ビットレートなど、エクスペリエンスの品質（QoE）に関する重要な配信指標を測定します。

* **精度の向上**：個々の訪問者の時間帯や分単位の同時視聴者数、コンテンツの平均視聴時間など、非常に詳細なレベルで視聴行動を評価します。

* **正確な計測**：OTT、スマートフォン、タブレット、デスクトップなど、メディア視聴に使用されたあらゆるデバイス全体でデータを計測し、利用状況のパターンや傾向を監視します。

* **セグメント化**：プレーヤー、デバイス、ジャンル、チャプターおよび番組に分類を適用し、全体的な視聴回数、コンテンツ、オーディオおよび広告（またはその組み合わせ）に対するそれぞれの影響度を把握します。


## 仕組み

ストリーミングメディアトラッキングデータは、Edge Network 用 Media SDK／拡張機能、タグ付きメディア拡張機能、Media SDK、Media Edge API、Media Collection API を使用してプレーヤーから収集されます。

すべての詳細なデータ（最大 10 秒）は、Media Analytics Service または Experience Edge（選択した[実装方式](/help/implementation/overview.md)に応じて）に送信され、個々の再生セッションごとにデータが収集および処理されます。

再生セッションが終了すると、計算したトラッキングデータが Adobe Analytics または Customer Journey Analytics に送信され、保存とレポートが行われます。

>[!NOTE]
>
>Customer Journey Analytics を実装すると、Experience Edge または Analytics Data Connector（ADC）を使用してデータを Customer Journey Analytics に送信できます。


様々な実装方法について詳しくは、[Adobe Analytics または Customer Journey Analytics 用のストリーミングメディアの実装](/help/implementation/overview.md)を参照してください。
