---
title: 平均ビットレート（ディメンション）
description: 各セッションのバケット化された平均ビットレートを100 kbps間隔でレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 6%

---


# 平均ビットレート（ディメンション）

>[!BEGINSHADEBOX]

*このページでは、各セッションのバケット化されたビットレートを報告する&#x200B;**平均ビットレート**&#x200B;ディメンションについて説明します。 生の加重平均指標については、[平均ビットレート （指標） &#x200B;](/help/reporting/metrics/average-bitrate.md)を参照してください。 この変数の収集方法については、[&#x200B; ビットレート &#x200B;](/help/implementation/variables/quality/bitrate.md)を参照してください。*

>[!ENDSHADEBOX]

**平均ビットレート** ディメンションは、セッションごとの平均再生ビットレートを100 kbps間隔でグループ化してレポートします。 バックエンドでは、セッション全体のすべてのビットレート値の加重平均として値を計算し、それをバケットに割り当てます。 ディメンションを使用して、エンゲージメントと品質をビットレート階層別に分割します。

## このディメンションの入力方法

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bitrateAverageBucket`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoebitrateaverageevar, post_videoqoebitrateaverageevar` |

## ディメンション項目

各項目はビットレートバケットラベルです（例：`800-899`、`3200-3299`）。 バケット化されたディメンションではなく、生の重み付けされた平均値に対して[平均ビットレート（指標） &#x200B;](/help/reporting/metrics/average-bitrate.md)を使用します。
