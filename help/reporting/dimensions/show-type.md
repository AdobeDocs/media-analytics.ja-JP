---
title: タイプを表示
description: コンテンツ形式（完全なエピソード、プレビュー、クリップなど）をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 9%

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
| Adobe Analytics | [[!UICONTROL  ビデオメタデータ ]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.type`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videoshowtype, post_videoshowtype` |

## ディメンション項目

| 値 | 説明 |
| --- | --- |
| `0` | 完全エピソード |
| `1` | プレビューまたは予告編 |
| `2` | クリップ |
| `3` | その他 |

値は文字列としてレポートされます。 カスタム値は受け入れられますが、4つの組み込みバケットにロールアップされません。
