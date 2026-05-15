---
title: 広告の長さ
description: 各広告のデュレーションを秒単位でレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# 広告の長さ

>[!BEGINSHADEBOX]

*このページでは、**広告の長さ**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[Ad length](/help/implementation/variables/ads/ad-length.md)を参照してください。*

>[!ENDSHADEBOX]

**Ad length** ディメンションは、各広告の期間を秒単位でレポートします。

## このディメンションの入力方法

広告の長さは、[広告開始](/help/implementation/events/ads/ad-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.length`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadlength`, `post_videoadlength` |
| Audience Manager | `c_contextdata.a.media.ad.length` |

Adobe Analyticsでは、このディメンションは、**Ad length （variable）** （`a.media.ad.length`から直接収集）と&#x200B;**Ad length** （[Ad](ad.md) ディメンションから派生した分類）の2つの方法で表示されます。 分類を使用する場合は、[分類セット &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して値を入力および維持する責任があります。 **広告の長さ（変数）**&#x200B;を使用すると、分類のメンテナンスは必要ありませんが、広告の長さと親[広告](ad.md) ディメンションとの間の保証された1:1関係が失われます。 実装ワークフローで最もサポートされているコンポーネントを使用します。

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告されたリテラル広告長の値（秒単位）です。
