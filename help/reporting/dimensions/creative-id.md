---
title: クリエイティブ ID
description: 広告クリエイティブ IDをレポートします。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 3%
---

# クリエイティブ ID

>[!BEGINSHADEBOX]

*このページでは、**Creative ID**のレポートディメンションについて説明します。 この変数の収集方法については、[Creative ID](/help/implementation/variables/ads/creative-id.md)を参照してください。*

>[!ENDSHADEBOX]

**Creative ID** ディメンションは、広告クリエイティブ IDをレポートします。 ディメンションを使用して、クリエイティブを共有する広告全体でエンゲージメントをロールアップします。

## このディメンションの入力方法

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.ad.creative`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | [Ad](ad.md) ディメンションの分類。 **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.ad.creative`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |
| Audience Manager | `c_contextdata.a.media.ad.creative` |

## 分類アプローチ

**[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)**&#x200B;がレポートスイートに対して有効になっている場合、AdobeはCreative ID分類構造を自動的に作成します。 [分類セット ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチにより、各広告IDとクリエイティブ IDの間に、1対1の関係を保証できます。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>Creative ID分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.ad.creative`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類の保守を必要とせずに、クリエイティブ IDをヒットごとの値としてキャプチャします。

トレードオフは、クリエイティブ IDと親[Ad](ad.md) ディメンションの間の保証された1:1の関係が失われることです。 実装でイベント間で同じ広告IDに一貫性のない値が送信される場合、同じ広告の下に複数のクリエイティブ IDが表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各アイテムは一意のクリエイティブ IDです。 クリエイティブごとに安定した識別子を使用することで、同じクリエイティブをキャンペーンをまたいで1行のアイテムまでロールアップできます。
