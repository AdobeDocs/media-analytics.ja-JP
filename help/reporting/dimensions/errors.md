---
title: エラー数
description: セッションごとのエラーイベントの数を報告します。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---


# エラー数

>[!BEGINSHADEBOX]

*このページでは、**エラー**ディメンションについて説明します。 Adobe Analyticsは、同じ`a.media.qoe.errorCount`個のコンテキストデータ変数から、ペアの[ エラーイベント指標](/help/reporting/metrics/error-events.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.errorCount` フィールドを公開します。*

>[!ENDSHADEBOX]

**エラー** ディメンションは、セッション中に受信したエラーイベントの数を報告します。 ディメンションを使用して、正確なエラー数ごとにエンゲージメントを分割します。

## このディメンションの入力方法

メディアバックエンドは、プレーヤーによって報告されるすべてのエラーのカウントを増分します。 値はクローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.errorCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoeerrorcountevar`, `post_videoqoeerrorcountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

## ディメンション項目

各項目は、クローズ呼び出しで報告されるリテラルのエラー数の値です。 セッションレベルのブール値レポートの場合（エラーが発生したかどうかにかかわらず）、[ エラーが影響を受けるストリーム ](/help/reporting/metrics/error-impacted-streams.md)を使用します。 一意のエラーIDの場合、[外部エラーID](external-error-ids.md)と[Player SDK エラーID](player-sdk-error-ids.md)を使用します。

>[!NOTE]
>
>従来のハートビート SDK（Media SDK 1.5.x-2.x）を使用する場合、SDKによって内部的に生成されたエラーIDは、コンテキストデータキー`a.media.qoe.mediaSdkErrors`で自動的に収集され、カスタム処理ルールを介してAdobe Analyticsでアクセスできます。 Audience Manager特性は`c_contextdata.a.media.qoe.mediaSdkErrors`です。 このフィールドは、Media Collection APIまたはMedia Edge APIの実装には適用されません。
