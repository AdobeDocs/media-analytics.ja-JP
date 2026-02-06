---
title: Adobe streaming media の概要
description: Adobe Streaming Media ソリューションを使用すると、コンテンツ、オーディオおよび広告に関する強力なinsightを取得できます。
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 59%

---

# Adobe streaming media services の概要

![バナー](./assets/media_analytics_banner.png)

Adobe ストリーミングメディアサービスは、オーディオ、ビデオ、ストリーミングメディアプロバイダー向けの広告など、ストリーミングメディアコンテンツ用の強力な収集、測定およびパーソナライゼーションツールを提供します。 ストリーミングメディア指標を、Audience Analytics、モバイル、クロスデバイス分析などの機能と組み合わせることができます。

ストリーミングメディアデータは、次のAdobe Experience Platform製品と容易に統合できます。

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>ストリーミングメディアサービスを実装するには、Adobe営業担当またはAdobe アカウントチームに連絡して、Customer Journey Analytics Streaming Media Collection アドオンまたは Adobe Analytics for Streaming Media アドオンが商品ポートフォリオに含まれていることを確認してください。

## 主な特長

ストリーミングメディアサービスの利点には、リアルタイム監視、詳細な分析、実用的なインサイト、収益化の機会などが含まれます。

* **リアルタイム分析**：複数のチャネルにわたり、メディア開始などの主要パフォーマンス指標を利用して、アクションにつながる意思決定をリアルタイムで行います。

  ストリーミングメディアサービスを使用すると、ビデオ指標とオーディオ指標を評価および組み合わせることができる、期間、停止および開始に関するほぼリアルタイムのきめ細かい詳細情報を取得できます。 これらのインサイトにより、顧客の視聴習慣を把握し、高度にパーソナライズされたレコメンデーションでエンゲージメントを強化できます。

* **エンゲージメントの促進**：バッファリングイベントを減らしコンテンツ内で広告を再生する場所とタイミングを把握することによりユーザーエンゲージメントを強化して、繰り返し訪問を実現する、押し付けがましくないスムーズなエクスペリエンスを提供します。

* **全体像の把握**：すべてのコンテンツディストリビューターにわたる複数のデータポイントを統合して、すべてのメディアアクティビティの全体像を把握します。可能なあらゆるチャネルにわたるエンゲージメントと視聴を測定します。

  ストリーミングメディアサービスを使用すると、サイトやストリーミングアプリ全体で完全なカスタマージャーニーを追跡して、顧客のパスと関心を視覚化し、レコメンデーションを強化して、顧客体験をパーソナライズできます。  メディア測定を使用すれば、データを複数のディメンションやセグメントに分類し、完全で詳細な分析をおこなうのに必要なメタデータをすべてキャプチャできます。その後、データを分析し、成功基準を、完全に消費されたメディア、平均滞在時間、完了した広告に関連付けることができます。

* **重要な指標**：ドロップフレーム数、バッファリングに費やされた時間、平均ビットレートなど、エクスペリエンスの品質（QoE）に関する重要な配信指標を測定します。

* **精度の向上**：個々の訪問者の時間帯や分単位の同時視聴者数、コンテンツの平均視聴時間など、非常に詳細なレベルで視聴行動を評価します。

* **正確な計測**：OTT、スマートフォン、タブレット、デスクトップなど、メディア視聴に使用されたあらゆるデバイス全体でデータを計測し、ユーザーエンゲージメントのパターンや傾向を監視します。

* **セグメント化**：プレーヤー、デバイス、ジャンル、チャプターおよび番組に分類を適用し、全体的な視聴回数、コンテンツ、オーディオおよび広告（またはその組み合わせ）に対する顧客エンゲージメントを把握します。


## 仕組み

ストリーミングメディアサービスのトラッキングデータは、Media for Edge Network SDK/Extension、Media Extension with Tags、Media SDK、Media Edge API または Media Collection API を使用してプレーヤーから収集されます。

すべての詳細なデータ（最大 10 秒）は、Media Analytics Service または Experience Edge（選択した[実装方式](/help/implementation/overview.md)に応じて）に送信され、個々の再生セッションごとにデータが収集および処理されます。

再生セッションが終了すると、計算したトラッキングデータが Adobe Analytics または Customer Journey Analytics に送信され、保存とレポートが行われます。

>[!NOTE]
>
>Customer Journey Analytics を実装すると、Experience Edge または Analytics Data Connector（ADC）を使用してデータを Customer Journey Analytics に送信できます。


様々な実装方法について詳しくは、[Adobe AnalyticsまたはCustomer Journey Analyticsのストリーミングメディアサービスの実装 &#x200B;](/help/implementation/overview.md) を参照してください。
