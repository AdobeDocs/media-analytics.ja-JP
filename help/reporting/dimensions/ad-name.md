---
title: 広告名
description: 各広告の人間が判読可能なタイトルをレポートします。
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
source-wordcount: '194'
ht-degree: 7%
---

# 広告名

>[!BEGINSHADEBOX]

*このページでは、**広告名**のレポートディメンションについて説明します。 この変数の収集方法については、[Ad name](/help/implementation/variables/ads/ad-name.md)を参照してください。*

>[!ENDSHADEBOX]

**広告名** ディメンションは、各広告の人間が読み取れるタイトルをレポートします。

## このディメンションの入力方法

広告名は、[広告開始](/help/implementation/events/ads/ad-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア広告]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.ad.friendlyName`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

Adobe Analyticsでは、このディメンションは、**Ad name （variable）** （`a.media.ad.friendlyName`から直接収集）と&#x200B;**Ad name** （[Ad](ad.md) ディメンションから派生した分類）の2つの方法で表示されます。 分類を使用する場合は、[分類セット ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して値を入力および維持する責任があります。 **広告名（変数）**&#x200B;を使用する場合、分類のメンテナンスは必要ありませんが、広告名と親[広告](ad.md) ディメンションの間の保証された1:1の関係は失われます。 実装ワークフローで最もサポートされているコンポーネントを使用します。

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md) （例：`"Ford F-150"`）に報告されたリテラル広告タイトルです。
