---
title: フルスクリーンの影響を受けるストリーム
description: ビューアがフルスクリーンで少なくとも1回入力したセッションをカウントします。
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
source-wordcount: '180'
ht-degree: 8%
---

# フルスクリーンの影響を受けるストリーム

>[!BEGINSHADEBOX]

*このページでは、フルスクリーンの影響を受ける&#x200B;**ストリーム**&#x200B;のレポート指標について説明します。 この変数の収集方法については、[全画面](/help/implementation/variables/player-state/full-screen.md)を参照してください。*

>[!ENDSHADEBOX]

フルスクリーンの影響を受ける&#x200B;**ストリーム**&#x200B;指標では、ビューアがフルスクリーンに少なくとも1回参加したセッションがカウントされます。 この指標はセッションレベルのブール値です。同じセッション内の複数のフルスクリーンエントリが、影響を受ける1つのストリームとしてカウントされます。 全画面表示の合計配信数には、[全画面数](full-screen-count.md)を使用します。

## この指標の計算方法

メディアバックエンドは、セッション中にフルスクリーンの状態開始イベントを初めて受信したときに、このフラグを設定します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.states.fullscreen.set`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/media-reporting-details) エントリ （`name = "fullscreen"`、フィールド `isSet`） |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/ja/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.set` |
