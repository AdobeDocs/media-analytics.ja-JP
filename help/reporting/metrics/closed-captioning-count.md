---
title: クローズドキャプション数
description: セッション中にビューアがキャプションを有効にした回数をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%

---


# クローズドキャプション数

>[!BEGINSHADEBOX]

*このページでは、**クローズドキャプション数**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[&#x200B; クローズドキャプション &#x200B;](/help/implementation/variables/player-state/closed-captioning.md)を参照してください。*

>[!ENDSHADEBOX]

**クローズドキャプション数**&#x200B;指標は、セッション中にビューアがキャプションを有効にした回数を報告します。 各caption-enable state-start イベントは、カウントを増分します。 セッションレベルのブール値ロールアップのクローズドキャプション [&#128279;](closed-captioning-streams-impacted.md)の影響を受ける ストリームと、ステートでの合計時間の[&#x200B; クローズドキャプション合計時間](closed-captioning-total-duration.md)を組み合わせます。

## この指標の計算方法

メディアバックエンドでは、キャプションを有効にして状態を開始するイベントごとに、このカウントを増分します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.closedcaptioning.count`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "closedCaptioning"`、フィールド `count`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.count` |
