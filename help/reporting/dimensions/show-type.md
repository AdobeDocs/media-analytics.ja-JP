---
title: タイプを表示
description: コンテンツ形式（完全なエピソード、プレビュー、クリップなど）をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# タイプを表示

>[!BEGINSHADEBOX]

*このページでは、**タイプを表示**&#x200B;レポート ディメンションについて説明します。 この変数の収集方法については、[&#x200B; タイプを表示](/help/implementation/variables/standard-metadata/show-type.md)を参照してください。*

>[!ENDSHADEBOX]

**Show type** ディメンションは、文字列整数コードを使用してコンテンツ形式をレポートします。 このツールを使用すると、エンゲージメントを測定する際に、トレーラーやクリップなどの短編コンテンツからプログラム全体の表示を分離できます。

## このディメンションの入力方法

表示タイプは、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; ビデオメタデータ &#x200B;]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.type`から自動的に収集されます。 |
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
