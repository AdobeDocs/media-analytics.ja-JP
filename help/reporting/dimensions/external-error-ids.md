---
title: 外部エラーID
description: CDN エラーなどの外部ソースから一意のエラーIDをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 7%

---


# 外部エラーID

**外部エラーID** ディメンションは、Player SDK以外のソース（CDN エラーなど）からの一意のエラーIDをレポートします。 プレーヤーは、実装時にエラートラッキング APIを介してコードまたはIDを提供する必要があります。 セッションごとに複数のエラーIDがサポートされています。

## このディメンションの入力方法

プレーヤーは、[ エラー](/help/implementation/events/error.md)件のイベントで外部エラーIDをトラッカーに渡します。 バックエンドでは、セッション全体で一意のIDを収集し、クローズコールでレポートします。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.externalErrors`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoeextneralerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.externalErrors` |

## ディメンション項目

各アイテムは、プレーヤーが提供するエラーコードまたはIDです。 実装全体で安定した分類法を使用することで、セッション間でエラーIDが正しくロールアップされます。
