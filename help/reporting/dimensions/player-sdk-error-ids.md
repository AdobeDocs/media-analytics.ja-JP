---
title: Player SDK エラーID
description: コンテンツプレーヤーのSDKによって生成された一意のエラーIDをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 6%

---


# Player SDK エラーID

**Player SDK エラーID** ディメンションは、セッション中にContent Player SDKによって生成された一意のエラーIDをレポートします。 プレーヤーは、実装時にエラートラッキング APIを介してコードまたはIDを提供する必要があります。 セッションごとに複数のエラーIDがサポートされています。

## このディメンションの入力方法

プレーヤーは、`media.error`件のイベントでPlayer-SDK エラーIDをトラッカーに渡します。 バックエンドでは、セッション全体で一意のIDを収集し、クローズコールでレポートします。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.playerSdkErrors`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoeplayersdkerrors, post_videoqoeplayersdkerrors` |

## ディメンション項目

各アイテムは、プレイヤーSDKによって生成されたエラーコードまたはIDです。 実装全体で安定した分類法を使用することで、セッション間でエラーIDが正しくロールアップされます。
