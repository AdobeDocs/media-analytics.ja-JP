---
title: コンテンツの評価
description: テレビの保護者ガイドラインまたは地域の評価システムで定義された視聴者の評価を報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---


# コンテンツの評価

>[!BEGINSHADEBOX]

*このページでは、**コンテンツの評価**&#x200B;のレポート ディメンションについて説明します。 この変数の収集方法については、[&#x200B; コンテンツの評価](/help/implementation/variables/standard-metadata/content-rating.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツ評価** ディメンションは、各セッションのオーディエンス評価を報告します。 これを使用して、評価階層をまたいでエンゲージメントと広告の負荷を比較します。

## このディメンションの入力方法

コンテンツの評価は、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.rating`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | [&#x200B; コンテンツ（ID） &#x200B;](content.md) ディメンションの分類 – **[[!UICONTROL ビデオメタデータ]](/help/reporting/media-reports-enable.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.rating`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.rating`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |

## 分類アプローチ

レポートスイートで&#x200B;**[[!UICONTROL ビデオメタデータ]](/help/reporting/media-reports-enable.md)**&#x200B;が有効になっている場合、Adobeは自動的にコンテンツレーティング分類構造を作成します。 [分類セット &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチにより、各コンテンツ IDと評価の間に1:1の関係が保証されます。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>コンテンツレーティング分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.rating`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類の保守を必要とせずに、コンテンツレーティングをヒットごとの値として取得します。

トレードオフは、コンテンツレーティングと親[&#x200B; コンテンツ（ID） &#x200B;](content.md) ディメンションとの間の保証1:1関係が失われることです。 実装でイベント間で同じコンテンツ IDに一貫性のない値が送信される場合、同じコンテンツの下に複数の評価が表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各項目は、セッション開始時に報告されるリテラルの評定値です（例：`"TVY"`、`"TVG"`、`"TVPG"`、`"TVMA"`）。 評価システムごとに固定の値セットに固定して、行アイテムの断片化を避けます。
