---
title: 開始時間（ディメンション）
description: 最初のフレームがレンダリングされるまでの経過時間をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

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
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.timeToStart`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## ディメンション項目

各項目は、クローズ呼び出しでレポートされるリテラル起動時値です。
