---
title: 作成者
description: コンテンツの作成者またはプロダクションスタジオを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---


# 作成者

>[!BEGINSHADEBOX]

*このページでは、**発信元**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[発信元](/help/implementation/variables/standard-metadata/originator.md)を参照してください。*

>[!ENDSHADEBOX]

**Originator** ディメンションは、コンテンツの作成者または実稼動スタジオをレポートします（例：`"Warner Brothers"`または`"Sony"`）。 コンテンツ所有者や権利者のエンゲージメントを比較するために利用できます。

## このディメンションの入力方法

発信元は、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.originator`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | [&#x200B; コンテンツ（ID） &#x200B;](content.md) ディメンションの分類 – **[[!UICONTROL ビデオメタデータ]](/help/reporting/media-reports-enable.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.originator`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.originator`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |
| Audience Manager | `c_contextdata.a.media.originator` |

## 分類アプローチ

レポートスイートで&#x200B;**[[!UICONTROL ビデオメタデータ]](/help/reporting/media-reports-enable.md)**&#x200B;が有効になっている場合、Adobeは発信元の分類構造を自動的に作成します。 [分類セット &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチでは、各コンテンツ IDと作成者との間に1:1の関係が保証されます。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>発信元の分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.originator`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類の保守を必要とせずに、発信者をヒットごとの値としてキャプチャします。

トレードオフは、発信元と親[&#x200B; コンテンツ（ID） &#x200B;](content.md) ディメンションとの間の保証された1:1関係が失われることです。 実装でイベント間で同じコンテンツ IDに一貫性のない値が送信される場合、同じコンテンツの下に複数の作成者が表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各アイテムは、セッション開始時に報告されるリテラルの発信元の値です。 スタジオごとに安定した明確な名前を使用することで、無関係なエンティティ間でエンゲージメントが崩れるのを防ぎます。
