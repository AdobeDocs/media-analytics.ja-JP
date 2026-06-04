---
title: ストリーミングメディア指標の概要
description: Adobe AnalyticsとCustomer Journey Analyticsをまたいで、ストリーミングメディア指標を計算および整理する方法を説明します。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---


# ストリーミングメディア指標の概要

Streaming Media Analyticsの指標は、メディアバックエンドによって計算されるイベント駆動型のカウントと期間です。 メディアプレーヤーは、セッション開始、再生、ping、広告の開始などのイベントを送信します。メディアバックエンドは、これらのイベントを処理し、セッションのクローズコールで指標値を確定します。

## 指標の計算方法

ストリーミングメディア指標は、主に4つの計算パターンに従います。

* **イベントトリガーフラグ**：適格なイベントがセッションに初めて到達する時刻を設定します。 メインコンテンツの[`play`](/help/implementation/events/playback/play.md) イベントは[[!UICONTROL &#x200B; コンテンツ開始]](content-starts.md) フラグを設定し、[`adStart`](/help/implementation/events/ads/ad-start.md) イベントは[[!UICONTROL 広告が開始]](ad-starts.md)を設定します。 フラグは、イベントごとではなく、クローズコールのセッションごとに1回報告されます。

* **累積期間**：特定の再生状態がアクティブになっている間のping イベント間の間隔を合計します。 [[!UICONTROL &#x200B; メインコンテンツの再生中に費やされたコンテンツ時間]](content-time-spent.md)が累積されます。広告の再生中に[[!UICONTROL 広告時間]](ad-time-spent.md)が累積されます。 Adobeで推奨されるping間隔は、メインコンテンツの場合は10秒、広告中の場合は1秒です。そのため、使用時間の指標は、実装のping間隔と同じくらい詳細にすることができます。

* **イベント数**: セッション内の合計発生回数を追跡します。 [[!UICONTROL &#x200B; バッファーイベント &#x200B;]](buffer-events.md)、[[!UICONTROL &#x200B; ビットレートの変更]](bitrate-changes.md)、[[!UICONTROL &#x200B; エラーイベント &#x200B;]](error-events.md)、[[!UICONTROL 一時停止イベント &#x200B;]](pause-events.md)などの品質指標は、最初のイベントだけでなく、すべての発生をカウントします。

* **影響を受けるストリーム**：セッション中に対応するイベントが発生した場合、セッション レベルのフラグが1に設定されます（回数に関係なく）。 これらの指標を使用してリーチを測定し、イベント数指標を使用して重大度を測定します。 例えば、[[!UICONTROL &#x200B; バッファーの影響を受けたストリーム &#x200B;]](buffer-impacted-streams.md)を使用して、すべての再生セッションでバッファリングの影響を受けたセッションの割合を判断できます。

## レポートシステム別の可用性

| レポートシステム | 指標の到達方法 |
| --- | --- |
| Adobe Analytics | [&#x200B; コンテキストデータ変数](https://experienceleague.adobe.com/ja/docs/analytics/implementation/vars/page-vars/contextdata)を使用して入力されました。 一部の指標は、これらのコンテキストデータ変数を使用してソリューションイベントに自動的に入力されます。その他の指標は、[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を使用してカスタムイベントにマッピングする必要があります。 値を自動入力する指標では、最初にそれぞれの[&#x200B; ストリーミングメディアレポートスイート設定](../setup/analytics-reporting.md)を有効にする必要があります。 |
| Customer Journey Analytics | `xdm.mediaReporting.sessionDetails`および関連ノードのXDM フィールド。ストリーミングメディアデータを含む任意のデータセットから取得します。 [&#x200B; データビューコンポーネント設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/overview)内で、必要な設定を持つ各指標を作成する必要があります。 |
| データフィード | 指標は、`event_list`列と`post_event_list`列にイベント IDとして表示されます。 各フィードファイルには、ストリーミングメディア指標を含むすべての指標のルックアップを含む`events.csv` ファイルが含まれています。 |

>[!MORELIKETHIS]
>
>* [&#x200B; イベントの概要](/help/implementation/events/overview.md)：指標に入力するプレイヤーイベント
>* [変数の概要](/help/implementation/variables/overview.md): Adobeに取り込まれるデータ
>* [&#x200B; ディメンションの概要](/help/reporting/dimensions/overview.md)：変数が入力するレポートディメンション
