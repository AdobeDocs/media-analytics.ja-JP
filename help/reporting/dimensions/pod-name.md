---
title: ポッド名
description: 各広告枠のわかりやすい名前をレポートします。 分類またはカスタム処理ルールを使用して、Adobe Analyticsで収集します。
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---


# ポッド名

>[!BEGINSHADEBOX]

*このページでは、**ポッド名**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[Ad break name](/help/implementation/variables/ads/ad-break-name.md)を参照してください。*

>[!ENDSHADEBOX]

**ポッド名** ディメンションは、各広告枠のわかりやすい名前をレポートします（例：`"pre-roll"`、`"mid-roll-1"`）。 Customer Journey Analyticsでは、実装変数から直接入力された個別のディメンションです。 Adobe Analyticsでは、[Ad ポッド &#x200B;](ad-pod.md) ディメンションの分類と、処理ルールを使用して設定されたeVarの2つのアプローチを通じて利用できます。

## このディメンションの入力方法

ポッド名は、プレーヤーが`media.adBreakStart`に設定した[Ad break name](/help/implementation/variables/ads/ad-break-name.md)の値から取得されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.ad.podFriendlyName`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | 広告ポッドディメンションの分類 – **[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.ad.podFriendlyName`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |

## 分類アプローチ

**[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)**&#x200B;がレポートスイートに対して有効になっている場合、AdobeはPod名の分類構造を自動的に作成します。 [分類セット &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチでは、各ポッド IDとそのフレンドリ名との間に1:1の関係が保証されます。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>ポッド名の分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.ad.podFriendlyName`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類のメンテナンスを必要とせずに、ヒットごとの値としてわかりやすい名前をキャプチャします。

トレードオフは、ポッド名と親[広告ポッド &#x200B;](ad-pod.md) ディメンションとの間の保証された1:1関係が失われることです。 実装でイベント間で同じポッド IDに一貫性のない値が送信される場合、同じ広告ポッドの下に複数の名前が表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各項目は、`media.adBreakStart`に報告されたリテラル広告分割名です。
