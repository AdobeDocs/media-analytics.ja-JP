---
title: 初回放送日
description: コンテンツが最初にテレビで放映された日付を報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---


# 初回放送日

>[!BEGINSHADEBOX]

*このページでは、**最初のエア日**&#x200B;のレポート ディメンションについて説明します。 この変数を収集する方法については、[最初の通気日](/help/implementation/variables/standard-metadata/first-air-date.md)を参照してください。*

>[!ENDSHADEBOX]

**最初の放送日** ディメンションは、コンテンツがテレビで最初に放送された日付をレポートします。 新規リリースのエンゲージメントと古いコンテンツのエンゲージメントを分けるために使用できます。

## このディメンションの入力方法

初回放送日は、セッション開始時にプレイヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.airDate`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | [&#x200B; コンテンツ（ID） &#x200B;](content.md) ディメンションの分類 – **[[!UICONTROL ビデオメタデータ]](/help/reporting/media-reports-enable.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.airDate`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |

## 分類アプローチ

**[[!UICONTROL ビデオメタデータ]](/help/reporting/media-reports-enable.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeは自動的に最初の日付の分類構造を作成します。 [分類セット &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチにより、各コンテンツ IDと最初の放送日との間に1:1の関係が保証されます。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>最初のエア日付分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.airDate`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類メンテナンスを必要とせずに、ヒットごとの値として最初のエア日をキャプチャします。

トレードオフは、最初のエア日付と親[&#x200B; コンテンツ（ID） &#x200B;](content.md) ディメンションとの間の保証された1:1関係が失われることです。 実装でイベント間で同じコンテンツ IDに一貫性のない値が送信される場合、同じコンテンツの下に複数の最初の日付が表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラル日付文字列です。 実装全体で一貫した形式を使用。 Adobeでは`YYYY-MM-DD`をお勧めします。
