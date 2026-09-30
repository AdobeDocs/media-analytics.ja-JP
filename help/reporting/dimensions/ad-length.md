---
title: 広告の長さ
description: 各広告のデュレーションを秒単位でレポートします。
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
source-wordcount: '195'
ht-degree: 7%
---

# 広告の長さ

>[!BEGINSHADEBOX]

*このページでは、**広告の長さ**のレポートディメンションについて説明します。 この変数の収集方法については、[Ad length](/help/implementation/variables/ads/ad-length.md)を参照してください。*

>[!ENDSHADEBOX]

**Ad length** ディメンションは、各広告の期間を秒単位でレポートします。

## このディメンションの入力方法

広告の長さは、[広告開始](/help/implementation/events/ads/ad-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア広告]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.ad.length`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadlength`, `post_videoadlength` |
| Audience Manager | `c_contextdata.a.media.ad.length` |

Adobe Analyticsでは、このディメンションは、**Ad length （variable）** （`a.media.ad.length`から直接収集）と&#x200B;**Ad length** （[Ad](ad.md) ディメンションから派生した分類）の2つの方法で表示されます。 分類を使用する場合は、[分類セット ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して値を入力および維持する責任があります。 **広告の長さ（変数）**&#x200B;を使用する場合、分類のメンテナンスは必要ありませんが、広告の長さと親[広告](ad.md) ディメンションの間の保証された1:1の関係は失われます。 実装ワークフローで最もサポートされているコンポーネントを使用します。

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告されたリテラル広告長の値（秒単位）です。
