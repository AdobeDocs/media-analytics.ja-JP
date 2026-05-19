---
title: ピクチャインピクチャ数
description: セッション中にビューアがピクチャインピクチャに入った回数をレポートします。
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---


# ピクチャインピクチャ数

>[!BEGINSHADEBOX]

*このページでは、**ピクチャインピクチャ数**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[図](/help/implementation/variables/player-state/picture-in-picture.md)を参照してください。*

>[!ENDSHADEBOX]

**ピクチャインピクチャ数**&#x200B;指標は、視聴者がセッション中にピクチャインピクチャ再生に入った回数を報告します。 各ピクチャインピクチャの状態開始イベントは、カウントを増やします。 セッションレベルのブール値ロールアップのピクチャーによって影響を受ける[&#128279;](picture-in-picture-streams-impacted.md)&#x200B; ストリームと、状態の合計時間の[&#x200B; ピクチャーの合計期間](picture-in-picture-total-duration.md)を組み合わせます。

## この指標の計算方法

メディアバックエンドでは、ピクチャインピクチャのステート開始イベントごとに、このカウントを増やします。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.pictureinpicture.count`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "pictureInPicture"`、フィールド `count`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.count` |
