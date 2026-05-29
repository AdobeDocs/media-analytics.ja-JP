---
title: 章の位置
description: コンテンツ内の各章のインデックスをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---


# 章の位置

>[!BEGINSHADEBOX]

*このページでは、**章の位置**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[章の位置](/help/implementation/variables/chapters/chapter-position.md)を参照してください。*

>[!ENDSHADEBOX]

**チャプターの位置** ディメンションは、コンテンツ内の各チャプターのインデックスをレポートします。

## このディメンションの入力方法

チャプターの位置は、[&#x200B; チャプター開始](/help/implementation/events/chapters/chapter-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.chapter.position`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | [章](chapter.md) ディメンションの分類 – **[[!UICONTROL メディアチャプター]](/help/reporting/media-reports-enable.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.index`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.chapter.position`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |
| Audience Manager | `c_contextdata.a.media.chapter.position` |

## 分類アプローチ

レポートスイートで&#x200B;**[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)**&#x200B;が有効になっている場合、Adobeはチャプターのポジション分類構造を自動的に作成します。 [分類セット &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチは、各章IDとその位置との間に1:1の保証された関係を提供します。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>チャプターの職階分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.chapter.position`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類のメンテナンスを必要とせずに、章の位置をヒットごとの値としてキャプチャします。

トレードオフは、チャプターの位置と親[&#x200B; チャプター](chapter.md) ディメンションとの間の保証された1:1関係が失われることです。 実装がイベント間で同じ章IDに一貫性のない値を送信する場合、同じ章の下に複数の位置が表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各項目は、[章の開始](/help/implementation/events/chapters/chapter-start.md)で報告された整数位置の値です。
