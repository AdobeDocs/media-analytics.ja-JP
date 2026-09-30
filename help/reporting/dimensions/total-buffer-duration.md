---
title: 合計バッファー期間（ディメンション）
description: セッションあたりのバッファリングに費やした累積秒数をレポートします。
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
source-wordcount: '194'
ht-degree: 7%
---

# 合計バッファー期間（ディメンション）

>[!BEGINSHADEBOX]

*このページでは、**合計バッファー期間**ディメンションについて説明します。 Adobe Analyticsは、同じ`a.media.qoe.bufferTime`個のコンテキストデータ変数から、ペアの[合計バッファー時間（指標） ](/help/reporting/metrics/total-buffer-duration.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`xdm.mediaReporting.qoeDataDetails.bufferTime` フィールドを公開します。*

>[!ENDSHADEBOX]

**合計バッファー時間** ディメンションは、プレーヤーがセッション中にバッファー状態で費やした累積時間を秒単位でレポートします。 ディメンションを使用して、バッファー期間の正確な値ごとにエンゲージメントを分割します。

## このディメンションの入力方法

メディアバックエンドは、各バッファー間隔のデュレーションを合計します（[ バッファー開始](/help/implementation/events/playback/buffer-start.md)から次の状態変更まで）。 値はクローズ呼び出しで報告されます。 Analysis Workspaceは値を`HH:MM:SS`として表示します。データフィード、Data Warehouse、レポート APIは秒単位で値を表示します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bufferTime`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoebuffertimeevar`, `post_videoqoebuffertimeevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |

## ディメンション項目

各項目は、クローズ呼び出しで報告されるリテラル期間の値（秒単位）です。
