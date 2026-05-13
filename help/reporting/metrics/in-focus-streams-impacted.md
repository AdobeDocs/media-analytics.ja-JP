---
title: フォーカスの影響を受けるストリーム
description: 少なくとも1回はプレイヤーが注目していたセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 7%

---


# フォーカスの影響を受けるストリーム

>[!BEGINSHADEBOX]

*このページでは、フォーカスの影響を受ける&#x200B;**ストリーム**のレポート指標について説明します。 この変数の収集方法については、[ フォーカス中](/help/implementation/variables/player-state/in-focus.md)を参照してください。*

>[!ENDSHADEBOX]

フォーカスの影響を受ける&#x200B;**ストリーム**&#x200B;指標では、少なくとも1回はプレイヤーがフォーカスを当てていたセッションがカウントされます。 この指標はセッションレベルのブール値で、影響を受ける1つのストリームと同じセッション数の中の複数のフォーカスイベントを指します。 フォーカスイベントの合計数に対して、[ フォーカス数](in-focus-count.md)を使用します。

## この指標の計算方法

メディアバックエンドは、`inFocus` エントリの`mediaReporting.states[]`の`isSet` フラグを`true`に設定し、`statesStart`の`inFocus`を含む`media.statesUpdate` イベントを初めて受信しました。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.infocus.set`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "inFocus"`、フィールド `isSet`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
