---
title: コンテンツ完了
description: 再生ヘッドがコンテンツの最後に達したセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 9%

---


# コンテンツ完了

**コンテンツが完了しました**&#x200B;指標は、再生ヘッドがコンテンツの最後に達したセッションをカウントします。 [ コンテンツ開始](content-starts.md)と組み合わせて完了率を計算し、[ メディア開始](media-starts.md)と組み合わせてエンドツーエンドの表示率を計算します。

## この指標の計算方法

メディア バックエンドは、`media.sessionComplete` イベントを受信したときに`mediaReporting.sessionDetails.isCompleted = true`を設定します。 この指標は、クローズ呼び出しで報告されます。 明示的な`sessionComplete`なしでタイムアウトしたセッションは、完了としてカウントされません。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.complete`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
