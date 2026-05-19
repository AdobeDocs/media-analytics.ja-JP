---
title: バッファーの影響を受けるストリーム
description: プレイヤーが少なくとも1回バッファー状態に入ったセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 10%

---


# バッファーの影響を受けるストリーム

**バッファーの影響を受けたストリーム**&#x200B;指標では、少なくとも1回はバッファー状態に入ったセッションがカウントされます。 この指標は、セッションレベルのブール値です。影響を受ける1つのストリームと同じセッション数の中の複数のバッファーイベントです。 合計バッファーボリュームに対して、[&#x200B; バッファーイベント &#x200B;](buffer-events.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中に[&#x200B; バッファー開始](/help/implementation/events/playback/buffer-start.md) イベントを初めて受信したときに、このフラグを設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.buffer`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.buffer` |
