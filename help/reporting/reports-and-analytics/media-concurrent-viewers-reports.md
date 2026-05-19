---
title: メディア同時閲覧者数
description: 1日の間に同時視聴者を表示するために使用されるメディア同時視聴者ダッシュボードについて説明します。 データは、コンテンツ、デバイスの種類、国などでフィルタリングできます。
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: Streaming Media, Workspace Basics
role: User, Admin
TQID: https://experienceleague.adobe.com/8pqoGpVCRXvovD-cNPNOvFQFvJco3sWUq3SuXEOVeJI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e38cbddc-1633-4cd5-bed5-9f289f2a6029
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 299
ht-degree: 91%

---

# メディア同時ビューアレポート {#media-concurrent-viewers}

メディア同時閲覧者数ダッシュボードには、1 日の同時閲覧者が表示されます。 データは、コンテンツ、デバイスタイプまたは国でフィルターできます。

>[!TIP]
>
> このレポートは、同時にアクティブなメディアセッションに基づいています。  ユニーク訪問者ごとの同時視聴者を表示し、セグメントを適用し、分解して比較するには、[Analysis Workspace のメディア同時視聴者数パネル](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=ja)を使用します。
>

![](assets/video-concurrent-viewers.png)

## レポートの各機能 {#report-features}

このレポートには、次のような機能があります。

* リアルタイムではありません。 通常の Adobe Analytics の遅延があります。
* このレポートは 24 時間の期間を対象としています。 X 軸は、レポートスイートのタイムゾーンに基づく時間帯です。
* 分単位の詳細度で同時視聴者数を表示します。
* *メディア同時閲覧者数レポート*&#x200B;には、すべてのコンテンツの視聴者数が表示されます。
* *メディアの詳細*&#x200B;レポート内には同時閲覧者数レポートがあります。このレポートは、1 つの特定のメディアアイテムの視聴者数を示します。
* レポートの対象期間は 1 日のみです。
* お客様は、過去の同時ビューアレポートを参照できます（1 日に制限）。

## 制限事項 {#limitations}

このレポートの主な制限事項は次のとおりです。

* 選択したインターバルが 1 日ではない場合、データは表示されません。
* ReportBuilder などのデータをエクスポートすることはできません。
* データは表形式では表示できません。
* 電子メールでレポートを送信することはできません。
* 広告を追跡しない場合でも、メディアトラッキングを再度有効にしてメディア広告モジュールを選択する必要があります。
* この機能では、一時停止トラッキング機能を含むメディアハートビートライブラリを使用すると、正確なデータを参照できます。
