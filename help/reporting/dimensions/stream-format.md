---
title: ストリーム形式
description: 各セッションの品質層（通常はHDまたはSD）をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

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
| Adobe Analytics | `a.media.format`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.format`がマッピングされるeVar） |
| Audience Manager | `c_contextdata.a.media.format` |

## ディメンション項目

各項目は、セッション開始時にレポートされるリテラル形式の値です。 安定した値セット （`HD`、`SD`、`4K`、`UHD`）を使用して、スペルのバリエーション間で行アイテムが断片化しないようにします。
