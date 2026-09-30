---
title: Player SDK エラーID
description: コンテンツプレーヤーのSDKによって生成された一意のエラーIDをレポートします。
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
source-wordcount: '159'
ht-degree: 8%
---

# Player SDK エラーID

**Player SDK エラーID** ディメンションは、セッション中にContent Player SDKによって生成された一意のエラーIDをレポートします。 プレーヤーは、実装時にエラートラッキング APIを介してコードまたはIDを提供する必要があります。 セッションごとに複数のエラーIDがサポートされています。

## このディメンションの入力方法

プレーヤーは、[error](/help/implementation/events/error.md)件のイベントでPlayer-SDK エラーIDをトラッカーに渡します。 バックエンドでは、セッション全体で一意のIDを収集し、クローズコールでレポートします。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.playerSdkErrors`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoeplayersdkerrors`, `post_videoqoeplayersdkerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.playerSdkErrors` |

## ディメンション項目

各アイテムは、プレイヤーSDKによって生成されたエラーコードまたはIDです。 実装全体で安定した分類法を使用することで、セッション間でエラーIDが正しくロールアップされます。
