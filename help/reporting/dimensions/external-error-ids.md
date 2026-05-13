---
title: 外部エラーID
description: CDN エラーなどの外部ソースから一意のエラーIDをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 6%

---


# 外部エラーID

**外部エラーID** ディメンションは、Player SDK以外のソース（CDN エラーなど）からの一意のエラーIDをレポートします。 プレーヤーは、実装時にエラートラッキング APIを介してコードまたはIDを提供する必要があります。 セッションごとに複数のエラーIDがサポートされています。

## このディメンションの入力方法

プレーヤーは外部エラーIDを`media.error` イベントのトラッカーに渡します。 バックエンドでは、セッション全体で一意のIDを収集し、クローズコールでレポートします。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.externalErrors`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoeextneralerrors` |

## ディメンション項目

各アイテムは、プレーヤーが提供するエラーコードまたはIDです。 実装全体で安定した分類法を使用することで、セッション間でエラーIDが正しくロールアップされます。
