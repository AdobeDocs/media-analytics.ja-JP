---
source-git-commit: c06ecd16f417c9584fb87181074d1c2bee487e0b
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---
﻿---
title: 計算指標
description: Adobe AnalyticsおよびCustomer Journey Analyticsのストリーミングメディアレポート用のカスタム計算指標。
feature: Metrics
role: User, Admin
---

# 計算指標

Adobeのストリーミングメディアサービスの計算指標は、標準的なストリーミングメディア指標から構築されたカスタム指標です。これにより、実装を変更することなく、平均広告滞在時間やメディア完了率などの比率を導き出すことができます。

Analysis Workspaceでこれらの計算指標を作成するには、[Adobe Analytics](https://experienceleague.adobe.com/ja/docs/analytics/components/calculated-metrics/cm-overview)または[Customer Journey Analytics](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)でそれぞれの計算指標の概要を参照してください。

| 計算指標 | 説明 | 数式 |
| --- | --- | --- |
| 平均 メディアストリームあたりの広告 | 広告開始/メディア開始 | [`Ad Starts`](/help/reporting/metrics/ad-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 平均 メディアストリームごとのチャプター | チャプター開始/メディア開始 | [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 平均 メディア滞在時間 | メディア開始あたりの合計滞在時間（`HH:MM:SS`） | [`Media Time Spent`](/help/reporting/metrics/media-time-spent.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 平均 コンテンツ滞在時間 | コンテンツ開始あたりのコンテンツ滞在時間（`HH:MM:SS`） | [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| 平均 広告滞在時間 | 広告開始あたりの広告滞在時間（`HH:MM:SS`） | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| 平均 章の滞在時間 | 章開始あたりの章滞在時間（`HH:MM:SS`） | [`Chapter Time Spent`](/help/reporting/metrics/chapter-time-spent.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| メディア完了率 | 完了したコンテンツと開始されたメディアの割合 | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| コンテンツ完了率 | 完了したコンテンツと開始したコンテンツの割合 | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| 広告完了率 | 広告完了率と広告開始の比較 | [`Ad Completes`](/help/reporting/metrics/ad-completes.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| 章完了率 | 章の完了率と章の開始率 | [`Chapter Completes`](/help/reporting/metrics/chapter-completes.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| 開始率より前にドロップ | 開始前の低下の割合とメディアの開始前の低下の割合 | [`Drops Before Start`](/help/reporting/metrics/drops-before-start.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| コンテンツ中断期間の割合 | 合計中断時間とコンテンツ滞在時間の比較 | [`Total Pause Duration`](/help/reporting/metrics/total-pause-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| コンテンツバッファー期間レート | 総バッファ時間とコンテンツに費やした時間の割合 | [`Total Buffer Duration`](/help/reporting/metrics/total-buffer-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| コンテンツの開始時間 | 開始までの時間とコンテンツに費やした時間の比較 | [`Time to Start`](/help/reporting/metrics/time-to-start.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| 広告滞在時間率 | 広告滞在時間とコンテンツ滞在時間の比較 | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
