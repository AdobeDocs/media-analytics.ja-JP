---
title: アセット ID
description: 基になるメディアアセットの安定した業界識別子をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---


# アセット ID

>[!BEGINSHADEBOX]

*このページでは、**アセット ID**のレポートディメンションについて説明します。 この変数の収集方法については、[Asset ID](/help/implementation/variables/standard-metadata/asset-id.md)を参照してください。*

>[!ENDSHADEBOX]

**アセット ID** ディメンションは、基になるメディアアセットの安定した業界識別子をレポートします（通常、EIDR、TMS/Gracenote、またはRovi IDですが、独自のIDも使用できます）。

## このディメンションの入力方法

アセット IDは、セッション開始時にプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.asset`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | [ コンテンツ（ID） ](content.md) ディメンションの分類 – **[[!UICONTROL ビデオメタデータ]](/help/reporting/media-reports-enable.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.asset`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |
| Audience Manager | `c_contextdata.a.media.asset` |

## 分類アプローチ

**[[!UICONTROL ビデオメタデータ]](/help/reporting/media-reports-enable.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeは自動的にAsset ID分類構造を作成します。 [分類セット ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチにより、各コンテンツ IDとアセット IDとの間に1:1の関係が保証されます。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>アセット IDの分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.asset`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類の保守を必要とせずに、アセット IDをヒットごとの値として取得します。

トレードオフは、アセット IDと親[ コンテンツ （ID） ](content.md) ディメンションの間の保証された1:1関係が失われることです。 実装でイベント間で同じコンテンツ IDに一貫性のない値が送信される場合、同じコンテンツの下に複数のアセット IDが表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各項目は、レポート期間中にレポートされる一意のアセット ID値です。 すべての配信プラットフォームで、アセットごとに単一の安定した識別子を使用することで、同じコンテンツが単一の行アイテムまでロールアップされます。
