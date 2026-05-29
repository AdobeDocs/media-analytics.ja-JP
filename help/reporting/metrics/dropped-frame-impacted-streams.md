---
title: ドロップしたフレームの影響を受けるストリーム
description: 少なくとも1つのフレームがドロップされたセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 11%

---


# ドロップしたフレームの影響を受けるストリーム

**ドロップされたフレームの影響を受けるストリーム**&#x200B;指標は、少なくとも1つのフレームがドロップされたセッションをカウントします。 この指標はセッションレベルのブール値で、影響を受ける1つのストリームと同じセッション数の中の複数のドロップを指します。 合計ドロップボリュームには、[ ドロップされたフレーム ](dropped-frames.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッションのクローズ時にQoE オブジェクトの`droppedFrames`値が0より大きい場合に、このフラグを設定します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.qoe.droppedFrames`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
