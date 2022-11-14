---
title: Adobe Analytics for Streaming Media の概要
description: ストリーミングメディア分析を使用して、コンテンツ、オーディオおよび広告に関する強力なインサイトを得ます。
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 16%

---

# Adobe Analytics for Streaming Media の概要

![バナー](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media は、オーディオ、ビデオおよび広告用の強力な測定ツールを提供する Adobe Analytics のアドオンです。Analytics for Streaming Media を使用すると、ビデオとオーディオの指標を評価および組み合わせることができる、ほぼリアルタイムできめ細かい期間、停止および開始の詳細を取得できます。 これらのインサイトにより、顧客の視聴習慣を把握し、高度にパーソナライズされたレコメンデーションによるエンゲージメントを強化できます。

Adobe Analytics for Streaming Media を使用すると、サイトおよびストリーミングアプリをまたいで、完全なカスタマージャーニーを追跡できます。 ストリーミングメディア指標を、Audience Analytics、モバイル、クロスデバイス分析などの他のAdobe Analytics機能と組み合わせることができます。 この指標は、Adobe Analytics Reports や他のAdobe Experience Platform製品と簡単に統合できます。 メディア測定を使用すれば、データを複数のディメンションやセグメントに分類し、完全で詳細な分析をおこなうのに必要なメタデータをすべてキャプチャできます。その後、データを分析し、成功基準を、完全に消費されたメディア、平均滞在時間、完了した広告に関連付けることができます。

ドロップフレーム、バッファリングに費やされた時間、平均ビットレートなど、Quality of Experience(QoE) に関する重要な配信指標を測定できます。 また、指標を Web サイトやアプリのデータと組み合わせて、顧客のパスや興味を視覚化し、Adobe Experience Platformを使用してレコメンデーションの強化や顧客体験のパーソナライズを実現できます。

## 仕組み

ストリーミングメディアトラッキングデータは、メディア SDK、メディアコレクション API、またはメディア拡張機能（タグ付き）を使用して、プレーヤーから収集されます。 個々の再生セッションごとにデータを収集して処理する、すべての詳細なデータ（最大 10 秒）が Media Analytics サービスに送信されます。 再生セッションが終了すると、計算したトラッキングデータがAdobe Analyticsに送信され、保存とレポートがおこなわれます。 Adobe Customer Journey Analytics(CJA) 実装では、Analytics Data Connector(ADC) を使用してデータを CJA に送信できるので、お客様が CJA をレポートツールとして使用できます。

<!-- ![streaming media process](./assets/streaming-process1.png) -->

<div style="text-align: center;">
<img src="./assets/streaming-process1.png" alt="ストリーミングメディアプロセス" width="75%">
</div>

## 機能

Adobe Analytics for Streaming Media のメリットには、リアルタイム監視、詳細分析、施策につながるインサイト、収益化の機会などがあります。

* **リアルタイム分析**:複数のチャネルにわたるメディア開始などの主要なパフォーマンス指標を利用して、リアルタイムで実用的な決定を下します。

* **エンゲージメントの促進**:バッファリングイベントを減らし、コンテンツ内の広告を再生する場所とタイミングを把握して、繰り返し訪問を提供するスムーズで控えめなエクスペリエンスを提供します。

* **全体像**:すべてのコンテンツ配信業者の複数のデータポイントを組み合わせて、すべてのメディアアクティビティを完全に把握できます。Federated Analytics機能を使用して、あらゆるチャネルでエンゲージメントと視聴を測定します。

* **精度の向上**:個々の訪問者の時間帯や分単位の同時視聴者数、コンテンツの平均視聴時間など、非常に詳細なレベルで視聴行動を評価します。

* **正確な測定**:OTT、スマートフォン、タブレット、デスクトップなど、メディア視聴に使用された複数のデバイスをまたいで測定し、ユーザーのエンゲージメントのパターンや傾向を監視できます。

* **セグメント化**:プレーヤー、デバイス、ジャンル、チャプターおよび番組に分類を適用し、全体的な視聴回数、コンテンツ、オーディオおよび広告（またはその組み合わせ）に対するそれぞれの影響度を把握できます。
