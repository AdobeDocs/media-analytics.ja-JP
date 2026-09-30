---
title: ドロップしたフレームの影響を受けるストリーム
description: 少なくとも1つのフレームがドロップされたセッションをカウントします。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 11%
---

# ドロップしたフレームの影響を受けるストリーム

**ドロップされたフレームの影響を受けるストリーム**&#x200B;指標は、少なくとも1つのフレームがドロップされたセッションをカウントします。 この指標はセッションレベルのブール値です。同じセッション内の複数のドロップは、影響を受ける1つのストリームとしてカウントされます。 合計ドロップボリュームには、[ ドロップされたフレーム ](dropped-frames.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッションのクローズ時にQoE オブジェクトの`droppedFrames`値が0より大きい場合に、このフラグを設定します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア品質]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.qoe.droppedFrames`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
