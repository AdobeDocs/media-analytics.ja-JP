---
title: 章名
description: 人間が読み取れる章のタイトルが表示されます。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---


# 章名

>[!BEGINSHADEBOX]

*このページでは、**章名**のレポートディメンションについて説明します。 この変数の収集方法については、[章名](/help/implementation/variables/chapters/chapter-name.md)を参照してください。*

>[!ENDSHADEBOX]

**章名** ディメンションは、各章の人間が読めるタイトルを表示します（例：`"Pilot Episode - Opening"`）。

## このディメンションの入力方法

チャプター名は、[ チャプター開始](/help/implementation/events/chapters/chapter-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.chapter.friendlyName`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | [章](chapter.md) ディメンションの分類 – **[[!UICONTROL メディアチャプター]](/help/reporting/setup/analytics-reporting.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.chapter.friendlyName`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |
| Audience Manager | `c_contextdata.a.media.chapter.friendlyName` |

## 分類アプローチ

レポートスイートで&#x200B;**[[!UICONTROL Media Chapters]](/help/reporting/setup/analytics-reporting.md)**&#x200B;が有効になっている場合、Adobeはチャプター名の分類構造を自動的に作成します。 [分類セット ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチでは、各章IDとわかりやすい名前との間に1:1の関係が保証されます。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>章名の分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.chapter.friendlyName`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類のメンテナンスを必要とせずに、ヒットごとの値としてわかりやすい名前をキャプチャします。

チャプター名と親[ チャプター](chapter.md) ディメンションの間の保証された1:1関係が失われることがトレードオフになります。 実装でイベント間で同じ章IDに一貫性のない値が送信される場合、同じ章の下に複数の名前が表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各項目は、[章の開始](/help/implementation/events/chapters/chapter-start.md)に報告されたリテラル章タイトルです。
