---
title: ポッドの位置
description: コンテンツ内の各広告枠のオフセットをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---


# ポッドの位置

>[!BEGINSHADEBOX]

*このページでは、**ポッドの位置**のレポートディメンションについて説明します。 この変数の収集方法については、[Ad break start time](/help/implementation/variables/ads/ad-break-start-time.md)を参照してください。*

>[!ENDSHADEBOX]

**ポッド位置** ディメンションは、コンテンツ内の各広告枠のオフセットを秒単位でレポートします。 プレロールの位置は`0`です。ミッドロールの位置は、再生ヘッドの開始時間に対応しています。

## このディメンションの入力方法

ポッドの位置は、[広告区切り開始](/help/implementation/events/ads/ad-break-start.md)にプレーヤーが設定した[広告区切り開始時間](/help/implementation/variables/ads/ad-break-start-time.md)の値から設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics （処理ルール） | `a.media.ad.podSecond`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Adobe Analytics（分類） | [広告ポッド ](ad-pod.md) ディメンションの分類。 **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeはこの分類を自動的に作成します。 分類値の入力と維持はユーザーの責任です。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| データフィード（処理ルール） | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.ad.podSecond`がマッピングされるeVar） |
| データフィード（分類） | なし – データフィードは分類をサポートしていません。 |
| Audience Manager | `c_contextdata.a.media.ad.podSecond` |

## 分類アプローチ

**[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)**&#x200B;がレポートスイートに対して有効になっている場合、Adobeは自動的にPod position classification構造を作成します。 [分類セット ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)を使用して分類を入力および管理する責任があります。

このアプローチにより、各広告ポッド IDとその位置との間に1:1の関係が保証されます。 分類の更新は、そのIDのすべての履歴データにさかのぼって適用されます。

>[!IMPORTANT]
>
>ポッドの位置分類名は変更しないでください。 名前を変更すると、Adobeで元の分類が再作成され、重複する可能性があります。

## 処理ルールのアプローチ

`a.media.ad.podSecond`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 このアプローチは、分類のメンテナンスを必要とせずに、ポッドの位置をヒットごとの値としてキャプチャします。

トレードオフは、ポッド位置と親[広告ポッド ](ad-pod.md) ディメンションとの間の保証された1:1関係が失われることです。 実装でイベント間で同じポッド IDに一貫性のない値が送信される場合、同じ広告ポッドの下に複数の位置が表示される可能性があります。 値の更新は、今後のデータにのみ適用されます。

## ディメンション項目

各項目は、[ad break start](/help/implementation/events/ads/ad-break-start.md)に報告された整数オフセット値（秒単位）です。
