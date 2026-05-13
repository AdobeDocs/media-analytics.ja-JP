---
title: 広告数
description: セッション中に開始された広告の数をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# 広告数

**広告数**&#x200B;指標は、セッション中に開始された広告の数を報告します。 このツールを使用して、コンテンツ、チャネル、ストリームタイプごとの広告ロードを把握します。 広告ディメンション（広告主、キャンペーン、クリエイティブ）によってピボット化された広告開始数の場合は、広告変数カテゴリが有効になっている場合に使用できる広告開始指標を使用します。

## この指標の計算方法

メディア バックエンドは、セッション中に受信した`media.adStart` イベントごとに`mediaReporting.sessionDetails.adCount`を増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.adCount`をカスタムイベントにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （処理ルールが`a.media.adCount`にマッピングするカスタムイベント。[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)の参照を参照） |
