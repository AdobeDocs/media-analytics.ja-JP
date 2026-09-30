---
title: フォーカスの影響を受けるストリーム
description: 少なくとも1回はプレイヤーが注目していたセッションをカウントします。
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
source-wordcount: '177'
ht-degree: 8%
---

# フォーカスの影響を受けるストリーム

>[!BEGINSHADEBOX]

*このページでは、フォーカスの影響を受ける&#x200B;**ストリーム**のレポート指標について説明します。 この変数の収集方法については、[ フォーカス中](/help/implementation/variables/player-state/in-focus.md)を参照してください。*

>[!ENDSHADEBOX]

フォーカスの影響を受ける&#x200B;**ストリーム**&#x200B;指標では、少なくとも1回はプレイヤーがフォーカスを当てていたセッションがカウントされます。 この指標はセッションレベルのブール値です。同じセッション内の複数のフォーカスイベントは、影響を受ける1つのストリームとしてカウントされます。 フォーカスイベントの合計数に対して、[ フォーカス数](in-focus-count.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中に初めてフォーカス状態の開始イベントを受信したときに、このフラグを設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.states.infocus.set`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "inFocus"`、フィールド `isSet`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.infocus.set` |
