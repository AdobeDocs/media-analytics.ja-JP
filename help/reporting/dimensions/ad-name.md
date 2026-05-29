---
title: 広告名
description: 各広告の人間が判読可能なタイトルをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 6%

---


# 広告名

>[!BEGINSHADEBOX]

*このページでは、**広告名**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[Ad name](/help/implementation/variables/ads/ad-name.md)を参照してください。*

>[!ENDSHADEBOX]

**広告名** ディメンションは、各広告の人間が読み取れるタイトルをレポートします。

## このディメンションの入力方法

広告名は、[広告開始](/help/implementation/events/ads/ad-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.friendlyName`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

Adobe Analyticsでは、このディメンションは、**Ad name （variable）** （`a.media.ad.friendlyName`から直接収集）と&#x200B;**Ad name** （[Ad](ad.md) ディメンションから派生した分類）の2つの方法で表示されます。 分類を使用する場合は、[分類セット &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して値を入力および維持する責任があります。 **広告名（変数）**&#x200B;を使用すると、分類のメンテナンスは必要ありませんが、広告名と親[広告](ad.md) ディメンションとの間の保証された1:1関係が失われます。 実装ワークフローで最もサポートされているコンポーネントを使用します。

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md) （例：`"Ford F-150"`）に報告されたリテラル広告タイトルです。
