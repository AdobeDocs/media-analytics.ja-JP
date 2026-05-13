---
title: ビットレートの変更（ディメンション）
description: セッションごとのビットレート変更イベントの数をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 5%

---


# ビットレートの変更（ディメンション）

>[!BEGINSHADEBOX]

*このページでは、**ビットレートの変更**ディメンションについて説明します。 Adobe Analyticsは、同じ`a.media.qoe.bitrateChangeCount`個のコンテキストデータ変数から、ペアの[ ビットレート変更（指標） ](/help/reporting/metrics/bitrate-changes.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`mediaReporting.qoeDataDetails.bitrateChangeCount` フィールドを公開します。 ビットレート変更イベントを実行する方法については、[ ビットレート変更](/help/implementation/variables/quality/bitrate-change.md)を参照してください。*

>[!ENDSHADEBOX]

**ビットレート変更** ディメンションは、セッション中に発生したビットレート変更イベントの数をレポートします。 ディメンションを使用して、正確な変更回数の値でエンゲージメントと品質を分割します（例えば、「3 ビットレートの変更を含むセッションと0」を含むセッション）。

## このディメンションの入力方法

メディアバックエンドは、セッション中に受信した`media.bitrateChange` イベントごとにカウントを増分します。 値はクローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bitrateChangeCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoebitratechangecountevar, post_videoqoebitratechangecountevar` |

## ディメンション項目

各項目は、クローズ呼び出しで報告されたリテラル変更回数の値です。 セッションレベルのブール値レポートの場合（セッションでビットレートの変更が発生したかどうかにかかわらず）、[ ビットレートの変更が影響を受けるストリーム ](/help/reporting/metrics/bitrate-change-impacted-streams.md)を使用します。
