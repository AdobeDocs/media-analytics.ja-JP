---
title: Player SDK エラーID
description: コンテンツプレーヤーのSDKによって生成された一意のエラーIDをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 7%

---


# Player SDK エラーID

**Player SDK エラーID** ディメンションは、セッション中にContent Player SDKによって生成された一意のエラーIDをレポートします。 プレーヤーは、実装時にエラートラッキング APIを介してコードまたはIDを提供する必要があります。 セッションごとに複数のエラーIDがサポートされています。

## このディメンションの入力方法

プレーヤーは、[error](/help/implementation/events/error.md)件のイベントでPlayer-SDK エラーIDをトラッカーに渡します。 バックエンドでは、セッション全体で一意のIDを収集し、クローズコールでレポートします。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.playerSdkErrors`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoeplayersdkerrors`, `post_videoqoeplayersdkerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.playerSdkErrors` |

## ディメンション項目

各アイテムは、プレイヤーSDKによって生成されたエラーコードまたはIDです。 実装全体で安定した分類法を使用することで、セッション間でエラーIDが正しくロールアップされます。
