---
title: タイプを表示
description: コンテンツ形式（完全なエピソード、プレビュー、クリップなど）をレポートします。
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
source-wordcount: '145'
ht-degree: 11%
---

# タイプを表示

>[!BEGINSHADEBOX]

*このページでは、**タイプを表示**レポート ディメンションについて説明します。 この変数の収集方法については、[ タイプを表示](/help/implementation/variables/standard-metadata/show-type.md)を参照してください。*

>[!ENDSHADEBOX]

**Show type** ディメンションは、文字列整数コードを使用してコンテンツ形式をレポートします。 このツールを使用すると、エンゲージメントを測定する際に、トレーラーやクリップなどの短編コンテンツからプログラム全体の表示を分離できます。

## このディメンションの入力方法

表示タイプは、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  ビデオメタデータ ]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.type`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoshowtype`, `post_videoshowtype` |
| Audience Manager | `c_contextdata.a.media.type` |

## ディメンション項目

| 値 | 説明 |
| --- | --- |
| `0` | 完全エピソード |
| `1` | プレビューまたは予告編 |
| `2` | クリップ |
| `3` | その他 |

値は文字列としてレポートされます。 カスタム値は受け入れられますが、4つの組み込みバケットにロールアップされません。
