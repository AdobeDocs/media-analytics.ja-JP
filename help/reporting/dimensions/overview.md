---
title: ストリーミングメディアディメンションの概要
description: Adobe AnalyticsとCustomer Journey Analytics全体でストリーミングメディアディメンションが入力され、整理される方法について説明します。
feature: Dimensions
role: User, Admin
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---


# ストリーミングメディアディメンションの概要

ストリーミングメディア分析のディメンションでは、コンテンツ名、ストリームタイプ、広告名などの数十の属性によって指標をスライスし、フィルタリングできます。 ほとんどの設定は、セッション開始時にプレーヤーによって行われ、セッション終了まで続行されます。

## ディメンションの入力方法

ストリーミングメディアのディメンションは、主に3つの母集団パターンに従います。

* **メディアプレーヤーから提供された**：ほとんどのディメンションのソース。 プレーヤーは[&#x200B; セッション開始](/help/implementation/events/session/session-start.md)呼び出しでこれらの値を送信し、メディアバックエンドはセッション内の後続のすべてのイベントにそれらを添付します。 セッション開始時にプレイヤーが送信するのは、レポートに表示されるものです。 例としては、[[!UICONTROL &#x200B; ストリームタイプ &#x200B;]](/help/reporting/dimensions/stream-type.md)、[[!UICONTROL &#x200B; コンテンツ名]](/help/reporting/dimensions/content-name.md)、[[!UICONTROL &#x200B; コンテンツ長]](/help/reporting/dimensions/content-length.md)などがあります。

* **派生値**: メディアバックエンドが、プレーヤーが指定した値を読み取るのではなく、蓄積された再生状態から計算するディメンション。 [[!UICONTROL &#x200B; コンテンツセグメント &#x200B;]](/help/reporting/dimensions/content-segment.md)は、再生中に再生ヘッドの位置から計算されます。 [[!UICONTROL &#x200B; メディアパス &#x200B;]](/help/reporting/dimensions/media-path.md)は、セッション全体のコンテンツと広告ステート間のトランジションを追跡します。 これらのディメンションは、プレーヤーが上書きすることはできません。

* **分類**: オプション。 個別のディメンションを入力する代わりに、[分類セット &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/components/classifications/sets/overview) （Adobe Analytics）または[&#x200B; ルックアップデータセット &#x200B;](https://experienceleague.adobe.com/en/docs/analytics-platform/using/compare-aa-cja/upgrade-to-cja/create-datasets/cja-upgrade-dataset-lookup) （Customer Journey Analytics）を使用して分類データを管理できます。

## レポートシステム別の可用性

| レポートシステム | ディメンションの到達方法 |
| --- | --- |
| Adobe Analytics | [&#x200B; コンテキストデータ変数](https://experienceleague.adobe.com/ja/docs/analytics/implementation/vars/page-vars/contextdata)を使用して入力されました。 これらのコンテキストデータ変数を使用してディメンションに自動的に入力されるディメンションもあれば、[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を使用して入力されるディメンションもあります。 値を自動入力するディメンションでは、最初にそれぞれの[&#x200B; ストリーミングメディアレポートスイート設定](../../implementation/media-sdk/setup/media-reports-enable.md)を有効にする必要があります。 |
| Customer Journey Analytics | 通常、`xdm.mediaReporting.sessionDetails`のXDM フィールドは、ストリーミングメディアデータを含む任意のデータセットから取得されます。 [&#x200B; データビューコンポーネント設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)内で、必要な設定を持つ各ディメンションを作成する必要があります。 |
| データフィード | ディメンションには、自動的に入力された独自のデータフィード列名（`videostreamtype`、`videoname`、または`videolength`など）があります。 処理ルールを必要とするディメンションでは、`evar`列の名前が使用されます。 |
| Audience Manager | Adobe Analyticsから転送されるコンテキストデータ。 AnalyticsからAudience Managerへのサーバーサイド転送が設定されている場合にのみ使用できます。 |

>[!MORELIKETHIS]
>
>* [指標の概要](../metrics/overview.md): ストリーミングメディア指標の参照
>* [&#x200B; パラメーターマッピング &#x200B;](/help/implementation/parameters-mapping.md)：変数から列からXDMへの参照を完了します
>* [&#x200B; メディアセグメント &#x200B;](/help/reporting/segments.md): ストリーミングメディアディメンションを使用する組み込みセグメント
