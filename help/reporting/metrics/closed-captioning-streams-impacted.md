---
title: クローズドキャプションの影響を受けるストリーム
description: ビューアが少なくとも1回キャプションを有効にしたセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 7%

---


# クローズドキャプションの影響を受けるストリーム

>[!BEGINSHADEBOX]

*このページでは、クローズドキャプション&#x200B;**レポート指標の影響を受ける**ストリームについて説明します。 この変数の収集方法については、[ クローズドキャプション ](/help/implementation/variables/player-state/closed-captioning.md)を参照してください。*

>[!ENDSHADEBOX]

クローズドキャプションの影響を受ける&#x200B;**ストリーム**&#x200B;指標では、ビューアが少なくとも1回はキャプションを有効にしたセッションがカウントされます。 この指標はセッションレベルのブール値です。影響を受ける1つのストリームと同じセッション数内の複数のキャプショントグルです。 キャプションを有効にする合計ボリュームには、[ クローズドキャプション数](closed-captioning-count.md)を使用します。

## この指標の計算方法

メディアバックエンドは、`closedCaptioning` エントリの`mediaReporting.states[]`の`isSet` フラグを`true`に設定し、`statesStart`の`closedCaptioning`を含む`media.statesUpdate` イベントを初めて受信しました。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.closedcaptioning.set`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "closedCaptioning"`、フィールド `isSet`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
