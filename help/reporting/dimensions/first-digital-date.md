---
title: 最初のデジタル日付
description: コンテンツがデジタルプラットフォームに最初に表示された日付をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# 最初のデジタル日付

>[!BEGINSHADEBOX]

*このページでは、**最初のデジタル日付**&#x200B;レポート ディメンションについて説明します。 この変数の収集方法については、[最初のデジタル日付](/help/implementation/variables/standard-metadata/first-digital-date.md)を参照してください。*

>[!ENDSHADEBOX]

**最初のデジタル日付** ディメンションは、コンテンツがデジタルプラットフォームに最初に表示された日付をレポートします。 [初回放送日](first-air-date.md)と併用して、デジタルリリースのタイミングと元の放送を比較できます。

## このディメンションの入力方法

最初のデジタル日付は、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.digitalDate`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | [&#x200B; コンテンツ（ID） &#x200B;](content.md) ディメンションの分類 – **[[!UICONTROL ビデオメタデータ]](/help/reporting/media-reports-enable.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.digitalDate`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |
| Audience Manager | `c_contextdata.a.media.digitalDate` |

## 分類アプローチ

レポートスイートで&#x200B;**[[!UICONTROL ビデオメタデータ]](/help/reporting/media-reports-enable.md)**&#x200B;が有効になっている場合、Adobeは最初のデジタル日付分類構造を自動的に作成します。 [分類セット &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチにより、各コンテンツ IDと最初のデジタル日付との間に1:1の関係が保証されます。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>最初のデジタル日付分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.digitalDate`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類の保守を必要とせずに、最初のデジタル日付をヒットごとの値として取得します。

トレードオフは、最初のデジタル日付と親[&#x200B; コンテンツ（ID） &#x200B;](content.md) ディメンションとの間の保証された1:1関係が失われることです。 実装でイベント間で同じコンテンツ IDに一貫性のない値が送信される場合、同じコンテンツの下に複数の最初のデジタル日付が表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラル日付文字列です。 実装全体で一貫した形式を使用。 Adobeでは`YYYY-MM-DD`をお勧めします。
