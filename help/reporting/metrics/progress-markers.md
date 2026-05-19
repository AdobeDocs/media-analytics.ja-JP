---
title: 進捗マーカー
description: 再生ヘッドが5つの固定しきい値（10%、25%、50%、75%、95%）をそれぞれ超えたセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 9%

---


# 進捗マーカー

**プログレスマーカー**&#x200B;は、5つの固定しきい値（コンテンツの長さの10%、25%、50%、75%、95%）をそれぞれ超える再生ヘッドを持つセッションをカウントする5つの個別の指標です。 これらを使用して、コンテンツ ランタイム全体のドロップオフをグラフ化します。[ コンテンツ開始](content-starts.md)と組み合わせて、各マイルストーンに達した開始セッションの共有を計算します。

各マーカーはセッションごとに1回起動し、シーク バック時にリトリガーされません。 転送を求める際にスキップされたマーカーはカウントされません（例えば、5%から60%にジャンプしたビューアは、10%、25%、50%のマーカーを一度にトリガーします）。

## 各マーカーの計算方法

メディアバックエンドは、各イベントの後にレポートされた再生ヘッドを[ コンテンツの長さ](../dimensions/content-length.md)と比較します。 再生ヘッドが最初にしきい値を超えると、対応するフラグがセッションの残りの部分に設定されます。 5つのマーカーはすべて、クローズコールで報告されます。 メインコンテンツで再生イベントを生成しないセッション（[開始する前にドロップ ](/help/reporting/metrics/drops-before-start.md)など）では、再生ヘッドがしきい値を超えることはないため、マーカーは設定されません。

>[!IMPORTANT]
>
>進捗マーカーには、ゼロ以外の[ コンテンツ長](/help/reporting/dimensions/content-length.md)と正確な再生ヘッドのレポートが必要です。 コンテンツの長さが設定されていないか、ゼロであるか、間違っている場合、マーカーは間違ったタイミングで起動するか、まったく起動しない可能性があります。

### 10%進捗マーカー {#progress-10}

再生ヘッドが最初にコンテンツの長さの10%に達したときに起動します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.progress10`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress10`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.progress10` |

### 25%進捗マーカー {#progress-25}

再生ヘッドが最初にコンテンツの長さの25%に達したときに起動します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.progress25`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress25`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.progress25` |

### 50%進捗マーカー {#progress-50}

再生ヘッドが最初にコンテンツの長さの50%に達したときに起動します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.progress50`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress50`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.progress50` |

### 75%進捗マーカー {#progress-75}

再生ヘッドが最初にコンテンツの長さの75%に達したときに起動します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.progress75`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress75`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.progress75` |

### 95%進捗マーカー {#progress-95}

再生ヘッドが最初にコンテンツの長さの95%に達したときに起動します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.progress95`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress95`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.progress95` |
