---
title: 平均ビットレート（ディメンション）
description: 各セッションのバケット化された平均ビットレートを100 kbps間隔でレポートします。
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
source-wordcount: '170'
ht-degree: 8%
---

# 平均ビットレート（ディメンション）

>[!BEGINSHADEBOX]

*このページでは、各セッションのバケット化されたビットレートを報告する&#x200B;**平均ビットレート**ディメンションについて説明します。 生の加重平均指標については、[平均ビットレート （指標） ](/help/reporting/metrics/average-bitrate.md)を参照してください。 この変数の収集方法については、[ ビットレート ](/help/implementation/variables/quality/bitrate.md)を参照してください。*

>[!ENDSHADEBOX]

**平均ビットレート** ディメンションは、セッションごとの平均再生ビットレートを100 kbps間隔でグループ化してレポートします。 バックエンドでは、セッション全体のすべてのビットレート値の加重平均として値を計算し、それをバケットに割り当てます。 ディメンションを使用して、エンゲージメントと品質をビットレート階層別に分割します。

## このディメンションの入力方法

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bitrateAverageBucket`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoebitrateaverageevar`, `post_videoqoebitrateaverageevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverageBucket` |

## ディメンション項目

各項目はビットレートバケットラベルです（例：`800-899`、`3200-3299`）。 バケット化されたディメンションではなく、生の重み付けされた平均値に対して[平均ビットレート（指標） ](/help/reporting/metrics/average-bitrate.md)を使用します。
