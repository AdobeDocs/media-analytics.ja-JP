---
title: 広告ポッド
description: 自動生成されたポッド IDでキーを設定した、各一意の広告枠をレポートします。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 8%
---

# 広告ポッド

**広告ポッド** ディメンションは、自動生成されたポッド IDでキーが設定された各一意の広告枠をレポートします。 セッション内のすべての広告は親の広告ポッドに属し、ポッドグループは複数の広告を連続して再生します。 ディメンションを使用して、広告ブレークでエンゲージメントを分割し、[&#x200B; ポッド名](pod-name.md)と[&#x200B; ポッド位置](pod-position.md)の分類の結合キーとして使用します。

## このディメンションの入力方法

広告ポッド IDは、[広告ブレーク開始](/help/implementation/events/ads/ad-break-start.md) イベントが発生したときに、SDKによって自動的に生成されます。 直接API実装では、ブレイクインデックスと開始時間から構築するか、カスタムポッド IDを指定します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.ad.pod`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| データフィード | `videoadpod`, `post_videoadpod` |
| Audience Manager | 該当なし |

## ディメンション項目

各項目は一意の広告ポッド IDです。 このIDは不透明で（通常はセッション ID、コンテンツ ID、区切りインデックスのハッシュ）、フレンドリーラベルの[Pod name](pod-name.md)と組み合わせると、グループ化キーとして最も便利です。
