---
title: ストリーム形式
description: 各セッションの品質層（通常はHDまたはSD）をレポートします。
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
| Adobe Analytics | `a.media.format`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.format`がマッピングされるeVar） |
| Audience Manager | `c_contextdata.a.media.format` |

## ディメンション項目

各項目は、セッション開始時にレポートされるリテラル形式の値です。 安定した値セット （`HD`、`SD`、`4K`、`UHD`）を使用して、スペルのバリエーション間で行アイテムが断片化しないようにします。
