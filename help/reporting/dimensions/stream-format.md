---
title: ストリーム形式
description: 各セッションの品質層（通常はHDまたはSD）をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 6%

---


# ストリーム形式

>[!BEGINSHADEBOX]

*このページでは、**ストリーム形式**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; ストリーム形式](/help/implementation/variables/standard-metadata/stream-format.md)を参照してください。*

>[!ENDSHADEBOX]

**ストリーム形式** ディメンションは、各セッションの品質層（通常は`"HD"`または`"SD"`）をレポートしますが、任意の文字列を使用できます）。 配信品質レベルをまたいで、エンゲージメント、完了率、品質を比較できます。

## このディメンションの入力方法

ストリーム形式は、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.format`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.format`がマッピングされるeVar） |

## ディメンション項目

各項目は、セッション開始時にレポートされるリテラル形式の値です。 安定した値セット （`HD`、`SD`、`4K`、`UHD`）を使用して、スペルのバリエーション間で行アイテムが断片化しないようにします。
