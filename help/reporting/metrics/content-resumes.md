---
title: コンテンツの再開
description: 以前に中断された再生を再開したセッションをカウントします。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 7%

---


# コンテンツの再開

>[!BEGINSHADEBOX]

*このページでは、**コンテンツ再開**レポート指標について説明します。 この変数の収集方法については、[ コンテンツの再開](/help/implementation/variables/core/content-resumes.md)を参照してください。*

>[!ENDSHADEBOX]

**Content resumes**&#x200B;指標は、以前に中断された再生を再開したセッションをカウントします。 プレーヤーがセッションを`sessionStart`の再開としてフラグ付けすると、増分されます（たとえば、バッファー、一時停止、失速が30分を超えた後など）。 同じビューアとアセットの継続セッションから本物の新しいセッションを分離するために使用します。

## この指標の計算方法

`mediaCollection.sessionDetails.hasResume`が`media.sessionStart` イベントの`true`の場合、メディアバックエンドは`mediaReporting.sessionDetails.hasResume = true`を設定します。 プレーヤーは、セッションに履歴書として明示的にフラグを付ける必要があります。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.resume`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
