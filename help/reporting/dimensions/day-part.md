---
title: 日パート
description: コンテンツがブロードキャストまたは再生された時間帯バケット（午前、午後、時間、深夜）を報告します。
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
source-wordcount: '151'
ht-degree: 9%
---

# 日パート

>[!BEGINSHADEBOX]

*このページでは、**日パート**のレポートディメンションについて説明します。 この変数の収集方法については、[日パート ](/help/implementation/variables/standard-metadata/day-part.md)を参照してください。*

>[!ENDSHADEBOX]

**日パート** ディメンションは、コンテンツがブロードキャストまたは再生された日時バケットをレポートします。 共通の値は`"Morning"`、`"Afternoon"`、`"Primetime"`、`"Late Night"`です。 視聴者のローカルタイムゾーンに関係なく、時間帯区分ごとのエンゲージメントを比較するために使用します。

## このディメンションの入力方法

日付部分は、セッション開始時にプレイヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  ビデオメタデータ ]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.dayPart`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## ディメンション項目

各項目は、セッション開始時にレポートされるリテラルのdaypart ラベルです。 行項目の一貫性を保つために、実装全体で固定された値のセットを使用します。
