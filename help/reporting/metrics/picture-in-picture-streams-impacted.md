---
title: ピクチャインピクチャの影響を受けるストリーム
description: ビューアが少なくとも1回はピクチャインピクチャに入ったセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 7%

---


# ピクチャインピクチャの影響を受けるストリーム

>[!BEGINSHADEBOX]

*このページでは、ピクチャインピクチャの影響を受ける&#x200B;**ストリーム**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[図](/help/implementation/variables/player-state/picture-in-picture.md)を参照してください。*

>[!ENDSHADEBOX]

ピクチャインピクチャの影響を受ける&#x200B;**ストリーム**&#x200B;指標では、ビューアが少なくとも1回ピクチャインピクチャ再生を開始したセッションがカウントされます。 この指標は、セッションレベルのブール値です。影響を受ける1つのストリームと同じセッションカウント内の複数のピクチャインピクチャエントリです。 ピクチャーインピクチャーの合計配信数には、[&#x200B; ピクチャーインピクチャー数](picture-in-picture-count.md)を使用します。

## この指標の計算方法

メディアバックエンドは、`pictureInPicture` エントリの`mediaReporting.states[]`の`isSet` フラグを`true`に設定し、`statesStart`の`pictureInPicture`を含む`media.statesUpdate` イベントを初めて受信しました。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.states.pictureinpicture.set`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "pictureInPicture"`、フィールド `isSet`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.set` |
