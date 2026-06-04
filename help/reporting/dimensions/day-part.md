---
title: 日パート
description: コンテンツがブロードキャストまたは再生された時間帯バケット（午前、午後、時間、深夜）を報告します。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 8%

---


# 日パート

>[!BEGINSHADEBOX]

*このページでは、**日パート**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[日パート &#x200B;](/help/implementation/variables/standard-metadata/day-part.md)を参照してください。*

>[!ENDSHADEBOX]

**日パート** ディメンションは、コンテンツがブロードキャストまたは再生された日時バケットをレポートします。 共通の値は`"Morning"`、`"Afternoon"`、`"Primetime"`、`"Late Night"`です。 視聴者のローカルタイムゾーンに関係なく、時間帯区分ごとのエンゲージメントを比較するために使用します。

## このディメンションの入力方法

日付部分は、セッション開始時にプレイヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; ビデオメタデータ &#x200B;]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.dayPart`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## ディメンション項目

各項目は、セッション開始時にレポートされるリテラルのdaypart ラベルです。 行項目の一貫性を保つために、実装全体で固定された値のセットを使用します。
