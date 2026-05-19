---
title: フルスクリーンの影響を受けるストリーム
description: ビューアがフルスクリーンで少なくとも1回入力したセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# フルスクリーンの影響を受けるストリーム

>[!BEGINSHADEBOX]

*このページでは、フルスクリーンの影響を受ける&#x200B;**ストリーム**のレポート指標について説明します。 この変数の収集方法については、[全画面](/help/implementation/variables/player-state/full-screen.md)を参照してください。*

>[!ENDSHADEBOX]

フルスクリーンの影響を受ける&#x200B;**ストリーム**&#x200B;指標では、ビューアがフルスクリーンに少なくとも1回参加したセッションがカウントされます。 この指標は、セッションレベルのブール値です。影響を受ける1つのストリームと同じセッション数の中で、複数のフルスクリーンエントリが表示されます。 全画面表示の合計配信数には、[全画面数](full-screen-count.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中にフルスクリーンの状態開始イベントを初めて受信したときに、このフラグを設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.fullscreen.set`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "fullscreen"`、フィールド `isSet`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.set` |
