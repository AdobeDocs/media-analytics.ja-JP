---
title: コンテンツの長さ
description: セッション開始時に設定された各メディアセッションの合計時間を秒単位でレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 6%

---


# コンテンツの長さ

>[!BEGINSHADEBOX]

*このページでは、**コンテンツの長さ**のレポートディメンションについて説明します。 この変数の収集方法については、[ コンテンツの長さ](/help/implementation/variables/core/content-length.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツ長** ディメンションは、セッション開始時に設定された各メディアセッションの合計期間を秒単位でレポートします。 [進行状況マーカー](/help/reporting/metrics/progress-markers.md)および[毎分平均オーディエンス ](/help/reporting/metrics/average-minute-audience.md)を含むバックエンド指標を強化します。

## このディメンションの入力方法

コンテンツの長さは、セッション開始時にプレーヤーによって設定されます。 報告される値は、アセットの経過時間ではなく、秒単位の全期間です。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.length`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videolength, post_videolength` |

>[!NOTE]
>
>Adobe Analyticsでは、この値は[Content](content.md) ディメンションの&#x200B;**Video length**&#x200B;分類にも対応します。 お客様は、その分類を個別に入力および管理する責任があります。 Customer Journey Analyticsは、このディメンションを直接使用します。 必要に応じて、[値のグループ化](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/value-bucketing)を使用できます。

>[!IMPORTANT]
>
>コンテンツの長さが設定されていないか、ゼロより大きくない場合、進行状況マーカーと毎分平均オーディエンスは、そのセッションに対して生成されません。 期間が不明なライブストリームの場合は、`86400`を設定します。

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラル長の値（秒単位）です。
