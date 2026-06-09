---
title: 章の長さ
description: 各章の期間をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---


# 章の長さ

>[!BEGINSHADEBOX]

*このページでは、**章の長さ**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[章の長さ](/help/implementation/variables/chapters/chapter-length.md)を参照してください。*

>[!ENDSHADEBOX]

**章の長さ** ディメンションでは、各章の期間が秒単位でレポートされます。

## このディメンションの入力方法

チャプターの長さは、[&#x200B; チャプター開始](/help/implementation/events/chapters/chapter-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.chapter.length`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | [章](chapter.md) ディメンションの分類。 レポートスイートで&#x200B;**[[!UICONTROL Media Chapters]](/help/reporting/setup/analytics-reporting.md)**&#x200B;が有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.length`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.chapter.length`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |
| Audience Manager | `c_contextdata.a.media.chapter.length` |

## 分類アプローチ

レポートスイートで&#x200B;**[[!UICONTROL Media Chapters]](/help/reporting/setup/analytics-reporting.md)**&#x200B;が有効になっている場合、Adobeはチャプター長の分類構造を自動的に作成します。 [分類セット &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチにより、各章IDとその長さの間に1:1の保証された関係が提供されます。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>章の長さの分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.chapter.length`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類のメンテナンスを必要とせずに、章の長さをヒットごとの値としてキャプチャします。

チャプターの長さと親[&#x200B; チャプター](chapter.md) ディメンションの間の保証された1:1関係が失われることがトレードオフになります。 実装でイベント間で同じ章IDに一貫性のない値が送信される場合、同じ章の下に複数の長さが表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各項目は、[章開始](/help/implementation/events/chapters/chapter-start.md)に報告された整数の長さの値（秒単位）です。
