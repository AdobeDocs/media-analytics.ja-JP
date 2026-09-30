---
title: 開始時間（ディメンション）
description: 最初のフレームがレンダリングされるまでの経過時間をレポートします。
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
source-wordcount: '190'
ht-degree: 7%
---

# 開始時間（ディメンション）

>[!BEGINSHADEBOX]

*このページでは、**開始までの時間**&#x200B;ディメンションについて説明します。 Adobe Analyticsは、同じ`a.media.qoe.timeToStart`個のコンテキストデータ変数から、ペアの[開始時間（指標） &#x200B;](/help/reporting/metrics/time-to-start.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.timeToStart` フィールドを公開します。 この変数の収集方法については、[開始時間](/help/implementation/variables/quality/time-to-start.md)を参照してください。*

>[!ENDSHADEBOX]

**開始時間** ディメンションは、セッションの開始から最初のフレームレンダリングまでの経過時間をレポートします。 ディメンションを使用して、起動時バケットごとのエンゲージメントを分割します。 Adobeは、値を秒単位で保存し、取り込み時にプレーヤーがレポートするミリ秒単位からコンバージョンします。

## このディメンションの入力方法

セッションが開始される前に、プレーヤーはQoE オブジェクトに`timeToStart`を設定します。 バックエンドは、クローズコールの値をレポートします。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.timeToStart`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## ディメンション項目

各項目は、クローズ呼び出しでレポートされるリテラル起動時値です。
