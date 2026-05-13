---
title: 広告名
description: 各広告の人間が判読可能なタイトルをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---


# 広告名

>[!BEGINSHADEBOX]

*このページでは、**広告名**のレポートディメンションについて説明します。 この変数の収集方法については、[Ad name](/help/implementation/variables/ads/ad-name.md)を参照してください。*

>[!ENDSHADEBOX]

**広告名** ディメンションは、各広告の人間が読み取れるタイトルをレポートします。

## このディメンションの入力方法

広告名は、`media.adStart` イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.friendlyName`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadname, post_videoadname` |

Adobe Analyticsでは、このディメンションは、**Ad name （variable）** （`a.media.ad.friendlyName`から直接収集）と&#x200B;**Ad name** （[Ad](ad.md) ディメンションから派生した分類）の2つの方法で表示されます。 分類を使用する場合は、[分類セット ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して値を入力および維持する責任があります。 **広告名（変数）**&#x200B;を使用すると、分類のメンテナンスは必要ありませんが、広告名と親[広告](ad.md) ディメンションとの間の保証された1:1関係が失われます。 実装ワークフローで最もサポートされているコンポーネントを使用します。

## ディメンション項目

各項目は、`media.adStart` （例：`"Ford F-150"`）に報告されたリテラル広告タイトルです。
