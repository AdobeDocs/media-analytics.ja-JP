---
title: 計算指標
description: Adobe AnalyticsおよびCustomer Journey Analyticsのストリーミングメディアレポート用のカスタム計算指標。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---

# 計算指標

Adobeのストリーミングメディアサービスの計算指標は、標準的なストリーミングメディア指標から構築されたカスタム指標です。これにより、実装を変更することなく、平均広告滞在時間やメディア完了率などの比率を導き出すことができます。

Analysis Workspaceでこれらの計算指標を作成するには、[Adobe Analytics](https://experienceleague.adobe.com/ja/docs/analytics/components/calculated-metrics/cm-overview)または[Customer Journey Analytics](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)でそれぞれの計算指標の概要を参照してください。

| 計算指標 | 説明 | 数式 |
| --- | --- | --- |
| 平均 メディアストリームあたりの広告 | [[!UICONTROL 広告開始]](/help/reporting/metrics/ad-starts.md)/[[!UICONTROL &#x200B; メディア開始]](/help/reporting/metrics/media-starts.md) | `[Ad starts] / [Media starts]` |
| 平均 メディアストリームごとのチャプター | [[!UICONTROL 章開始]](/help/reporting/metrics/chapter-starts.md)/[[!UICONTROL &#x200B; メディア開始]](/help/reporting/metrics/media-starts.md) | `[Chapter starts] / [Media starts]` |
| 平均 メディア滞在時間 | [&#128279;](/help/reporting/metrics/media-time-spent.md)&#x200B; メディアが[[!UICONTROL &#x200B; メディア開始]](/help/reporting/metrics/media-starts.md) （`HH:MM:SS`）ごとに費やした時間 | `[Media time spent] / [Media starts]` |
| 平均 コンテンツ滞在時間 | [&#128279;](/help/reporting/metrics/content-time-spent.md)&#x200B; コンテンツが[[!UICONTROL 個のコンテンツを開始]](/help/reporting/metrics/content-starts.md) （`HH:MM:SS`）ごとに費やした時間 | `[Content time spent] / [Content starts]` |
| 平均 広告滞在時間 | [&#128279;](/help/reporting/metrics/ad-time-spent.md)広告が[[!UICONTROL 広告開始]](/help/reporting/metrics/ad-starts.md) （`HH:MM:SS`）ごとに回費やした時間 | `[Ad time spent] / [Ad starts]` |
| 平均 章の滞在時間 | [&#128279;](/help/reporting/metrics/chapter-starts.md)章が[[!UICONTROL 章ごとに]](/help/reporting/metrics/chapter-time-spent.md)回費やした時間 （`HH:MM:SS`） | `[Chapter time spent] / [Chapter starts]` |
| メディア完了率 | [[!UICONTROL &#x200B; コンテンツ完了率]](/help/reporting/metrics/content-completes.md) vs. [[!UICONTROL &#x200B; メディア開始]](/help/reporting/metrics/media-starts.md) | `[Content completes] / [Media starts]` |
| コンテンツ完了率 | [[!UICONTROL &#x200B; コンテンツ完了率]](/help/reporting/metrics/content-completes.md) vs. [[!UICONTROL &#x200B; コンテンツ開始]](/help/reporting/metrics/content-starts.md) | `[Content completes] / [Content starts]` |
| 広告完了率 | [[!UICONTROL 広告完了率]](/help/reporting/metrics/ad-completes.md) vs. [[!UICONTROL 広告開始]](/help/reporting/metrics/ad-starts.md) | `[Ad completes] / [Ad starts]` |
| 章完了率 | [[!UICONTROL 章完了率]](/help/reporting/metrics/chapter-completes.md) vs. [[!UICONTROL 章開始]](/help/reporting/metrics/chapter-starts.md) | `[Chapter completes] / [Chapter starts]` |
| 開始率より前にドロップ | [[!UICONTROL 開始]](/help/reporting/metrics/drops-before-start.md)前のドロップ率と[[!UICONTROL &#x200B; メディア開始]](/help/reporting/metrics/media-starts.md) | `[Drops before start] / [Media starts]` |
| コンテンツ中断期間の割合 | [[!UICONTROL 合計一時停止の期間]](/help/reporting/metrics/total-pause-duration.md)と[[!UICONTROL &#x200B; コンテンツの滞在時間]](/help/reporting/metrics/content-time-spent.md)の割合 | `[Total pause duration] / [Content time spent]` |
| コンテンツバッファー期間レート | 合計バッファー時間[&#128279;](/help/reporting/metrics/total-buffer-duration.md)と[[!UICONTROL  コンテンツ滞在時間]](/help/reporting/metrics/content-time-spent.md)の割合 | `[Total buffer duration] / [Content time spent]` |
| コンテンツの開始時間 | [[!UICONTROL 開始までの時間]](/help/reporting/metrics/time-to-start.md)と[[!UICONTROL &#x200B; コンテンツ滞在時間]](/help/reporting/metrics/content-time-spent.md)の割合 | `[Time to start] / [Content time spent]` |
| 広告滞在時間率 | [[!UICONTROL 広告費]](/help/reporting/metrics/ad-time-spent.md)と[[!UICONTROL &#x200B; コンテンツ費やす時間]](/help/reporting/metrics/content-time-spent.md)の割合 | `[Ad time spent] / [Content time spent]` |

