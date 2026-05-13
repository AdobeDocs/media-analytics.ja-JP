---
title: 合計バッファー期間（ディメンション）
description: セッションあたりのバッファリングに費やした累積秒数をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 5%

---


# 合計バッファー期間（ディメンション）

>[!BEGINSHADEBOX]

*このページでは、**合計バッファー期間**&#x200B;ディメンションについて説明します。 Adobe Analyticsは、同じ`a.media.qoe.bufferTime`個のコンテキストデータ変数から、ペアの[合計バッファー時間（指標） &#x200B;](/help/reporting/metrics/total-buffer-duration.md)を自動入力します。 Customer Journey Analyticsは、ディメンションまたは指標として使用できる1つの`mediaReporting.qoeDataDetails.bufferTime` フィールドを公開します。*

>[!ENDSHADEBOX]

**合計バッファー時間** ディメンションは、プレーヤーがセッション中にバッファー状態で費やした累積時間を秒単位でレポートします。 ディメンションを使用して、バッファー期間の正確な値ごとにエンゲージメントを分割します。

## このディメンションの入力方法

メディアバックエンドは、各バッファー間隔（`media.bufferStart`から次の状態変更まで）の期間を合計します。 値はクローズ呼び出しで報告されます。 Analysis Workspaceは値を`HH:MM:SS`として表示します。データフィード、Data Warehouse、レポート APIは秒単位で値を表示します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.bufferTime`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `videoqoebuffertimeevar, post_videoqoebuffertimeevar` |

## ディメンション項目

各項目は、クローズ呼び出しで報告されるリテラル期間の値（秒単位）です。
