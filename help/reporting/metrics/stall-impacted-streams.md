---
title: 影響を受けるストリームを停止する
description: 再生中に少なくとも1回のストールが発生したセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%

---


# 影響を受けるストリームを停止する

**失速の影響を受けるストリーム**&#x200B;指標は、再生中に少なくとも1回の失速が発生したセッションをカウントします。 この指標はセッションレベルのブール値で、同じセッション内の複数のストールが、影響を受ける1つのストリームと同じようにカウントされます。 合計失速ボリュームには、[失速イベント &#x200B;](stall-events.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中に少なくとも3つの連続したイベントについて、メインコンテンツに再生ヘッドの動きが記録されていない場合に、このフラグを設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.qoe.stall`をカスタムイベントにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （処理ルールが`a.media.qoe.stall`にマッピングするカスタムイベント。[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)の参照を参照） |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
