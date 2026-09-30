---
title: ビットレートの変更（ディメンション）
description: セッションごとのビットレート変更イベントの数をレポートします。
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
source-wordcount: '205'
ht-degree: 6%
---

# ビットレートの変更（ディメンション）

>[!BEGINSHADEBOX]

*このページでは、**ビットレートの変更**&#x200B;ディメンションについて説明します。 Adobe Analyticsは、同じ`a.media.qoe.bitrateChangeCount`個のコンテキストデータ変数から、ペアの[&#x200B; ビットレート変更（指標） &#x200B;](/help/reporting/metrics/bitrate-changes.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` フィールドを公開します。 ビットレート変更イベントを実行する方法については、[&#x200B; ビットレート変更](/help/implementation/variables/quality/bitrate-change.md)を参照してください。*

>[!ENDSHADEBOX]

**ビットレート変更** ディメンションは、セッション中に発生したビットレート変更イベントの数をレポートします。 ディメンションを使用して、正確な変更回数の値でエンゲージメントと品質を分割します（例えば、「3 ビットレートの変更を含むセッションと0」を含むセッション）。

## このディメンションの入力方法

メディアバックエンドは、セッション中に受信した[&#x200B; ビットレート変更](/help/implementation/events/playback/bitrate-change.md) イベントごとにカウントを増分します。 値はクローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bitrateChangeCount`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoebitratechangecountevar`, `post_videoqoebitratechangecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

## ディメンション項目

各項目は、クローズ呼び出しで報告されたリテラル変更回数の値です。 セッションレベルのブール値レポートの場合（セッションでビットレートの変更が発生したかどうかにかかわらず）、[&#x200B; ビットレートの変更が影響を受けるストリーム &#x200B;](/help/reporting/metrics/bitrate-change-impacted-streams.md)を使用します。
