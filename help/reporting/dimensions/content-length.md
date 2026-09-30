---
title: コンテンツの長さ
description: セッション開始時に設定された各メディアセッションの合計時間を秒単位でレポートします。
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
source-wordcount: '231'
ht-degree: 7%
---

# コンテンツの長さ

>[!BEGINSHADEBOX]

*このページでは、**コンテンツの長さ**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; コンテンツの長さ](/help/implementation/variables/core/content-length.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツ長** ディメンションは、セッション開始時に設定された各メディアセッションの合計期間を秒単位でレポートします。 [進行状況マーカー](/help/reporting/metrics/progress-markers.md)および[毎分平均オーディエンス &#x200B;](/help/reporting/metrics/average-minute-audience.md)を含むバックエンド指標を強化します。

## このディメンションの入力方法

コンテンツの長さは、セッション開始時にプレーヤーによって設定されます。 報告される値は、アセットの経過時間ではなく、秒単位の全期間です。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.length`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.length`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videolength`, `post_videolength` |
| Audience Manager | `c_contextdata.a.media.length` |

>[!NOTE]
>
>Adobe Analyticsでは、この値は[Content](content.md) ディメンションの&#x200B;**Video length**&#x200B;分類にも対応します。 お客様は、その分類を個別に入力および管理する責任があります。 Customer Journey Analyticsは、このディメンションを直接使用します。 必要に応じて、[値のグループ化](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/value-bucketing)を使用できます。

>[!IMPORTANT]
>
>コンテンツの長さが設定されていないか、ゼロより大きくない場合、進行状況マーカーと毎分平均オーディエンスは、そのセッションに対して生成されません。 期間が不明なライブストリームの場合は、`86400`を設定します。

## ディメンション項目

各アイテムは、セッション開始時にレポートされるリテラル長の値（秒単位）です。
