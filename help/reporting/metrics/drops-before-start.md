---
title: 開始前にドロップ
description: メインコンテンツがレンダリングされる前にビューアが終了したセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 7%

---


# 開始前にドロップ

**開始前にドロップ**&#x200B;指標は、ビューアがメインコンテンツをレンダリングする前に終了したセッションをカウントします。 この指標は、広告の行動に関係なく、コンテンツが放棄された前にフラグを立てるため、純粋なコンテンツ前の脱落を測定するのに最適な手段です。 [&#x200B; メディア開始](/help/reporting/metrics/media-starts.md)および[&#x200B; コンテンツ開始](/help/reporting/metrics/content-starts.md)と組み合わせて、コンテンツフレームを生成しなかったセッションのシェアを計算します。

## この指標の計算方法

メディアバックエンドは、メインコンテンツで[play](/help/implementation/events/playback/play.md) イベントを生成することなく閉じるセッションにこのフラグを設定します。 この指標は、クローズ呼び出しで報告されます。 一般的なシナリオには、プレロール広告中にビューアが終了する、最初のバッファーフェーズでプレーヤーが無期限に停止する、最初のメインコンテンツ再生イベントの前にエラーが発生するなどがあります。 これらすべての場合、セッションは[&#x200B; メディア開始](/help/reporting/metrics/media-starts.md)を記録しますが、[&#x200B; コンテンツ開始](/help/reporting/metrics/content-starts.md)と[進行状況マーカー](/help/reporting/metrics/progress-markers.md)は記録されません。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.dropBeforeStart`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.dropBeforeStart` |
