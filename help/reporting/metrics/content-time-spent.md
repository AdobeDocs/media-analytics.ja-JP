---
title: コンテンツ滞在時間
description: セッションごとのアクティブなメインコンテンツ再生の合計秒数を報告します。
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 6%

---


# コンテンツ滞在時間

**コンテンツ滞在時間**&#x200B;指標は、広告、一時停止、バッファリング、ストールを除いた、セッションごとのアクティブなメインコンテンツの再生合計秒数を報告します。 コンテンツ表示のエンゲージメント指標として使用します。広告を含む滞在時間については、[&#x200B; メディア滞在時間](media-time-spent.md)を参照してください。

## この指標の計算方法

メディアバックエンドは、プレーヤーがメインコンテンツの`play`状態にある間に、イベント間の経過時間を合計します。 広告、一時停止、バッファーイベント、ストール中の時間は除外されます。 アクティブな再生時間のみがカウントされるため、視聴者が逆方向にシークしてセグメントを再視聴すると、指標は[&#x200B; コンテンツの長さ](/help/reporting/dimensions/content-length.md)を超える可能性があります。 特定のセグメントを通過するたびに追加の再生時間が蓄積され、ユーザーがセッションでコンテンツを消費して巻き戻す限り、発生する可能性があります。 この指標は、クローズ呼び出しで報告されます。 値は、Analysis Workspaceでは`HH:MM:SS`として表示され、データフィード、Data Warehouse、レポート APIでは秒単位で表示されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.timePlayed`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.timePlayed` |
