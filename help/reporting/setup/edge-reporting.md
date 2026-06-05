---
title: Edge実装用のレポートの設定
description: Edge Networkを通じて収集されたストリーミングメディアデータをレポートするようにCustomer Journey Analyticsを設定します。
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 8%

---

# Edge実装用のレポートの設定

Edge Networkを使用してStreaming Media Collectionを実装したら、収集したデータをレポートするようにCustomer Journey Analyticsを設定します。

>[!NOTE]
>
>このページでは、Edge実装の推奨される宛先であるCustomer Journey Analyticsでのレポートについて説明します。 データストリームがストリーミングメディアデータをAdobe Analyticsに送信する場合は、[Analyticsのみの実装に対するレポートの設定](analytics-reporting.md)を参照してください。

* **前提条件**: Edgeの実装を完了し、データを収集します。 [Edgeの実装の概要](/help/implementation/edge/overview.md)と、選択した実装方法を参照してください。

## Customer Journey Analytics で接続を作成する

1. Customer Journey Analyticsで、[Create a connection](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/create-connection)の説明に従って接続を作成します。 接続を作成する際に、「**[!UICONTROL すべての新しいデータを読み込む]**」チェックボックスが有効になっていることを確認します。

## Customer Journey Analytics でデータビューを作成

1. Customer Journey Analyticsで、[&#x200B; データビューの作成または編集](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/create-dataview)の説明に従ってデータビューを作成します。

   1. 「**[!UICONTROL 接続]**」フィールドで、以前に作成した接続を選択します。 新しい接続が表示されるまでに最大15分かかる場合があります。

   1. 「**[!UICONTROL コンポーネント]**」タブの「**[!UICONTROL スキーマフィールド]**」セクションで、下のテーブルの各コンポーネントを検索し、適切な&#x200B;**[!UICONTROL ディメンション]**&#x200B;または&#x200B;**[!UICONTROL 指標]** パネルにドラッグします。 同じ名前のフィールドが複数ある場合は、XDM パスを使用して正しいフィールドを確認します。 コンポーネント設定の「**[!UICONTROL コンテキストラベル]**」ドロップダウンに表示されているコンテキストラベルを適用します。

      | コンポーネント | タイプ | XDM パス | コンテキストラベル |
      |---|---|---|---|
      | [コンテンツ](/help/reporting/dimensions/content.md) | ディメンション | `mediaReporting.sessionDetails.name` | Media: Content ID |
      | [&#x200B; コンテンツ名](/help/reporting/dimensions/content-name.md) | ディメンション | `mediaReporting.sessionDetails.friendlyName` | メディア：ビデオ名 |
      | [&#x200B; コンテンツの長さ](/help/reporting/dimensions/content-length.md) | ディメンション | `mediaReporting.sessionDetails.length` | メディア：ビデオの長さ |
      | [表示](/help/reporting/dimensions/show.md) | ディメンション | `mediaReporting.sessionDetails.show` | メディア：表示 |
      | [&#x200B; シーズン &#x200B;](/help/reporting/dimensions/season.md) | ディメンション | `mediaReporting.sessionDetails.season` | メディア：季節 |
      | [&#x200B; エピソード &#x200B;](/help/reporting/dimensions/episode.md) | ディメンション | `mediaReporting.sessionDetails.episode` | メディア：エピソード |
      | イベントタイプ | ディメンション | `eventType` | メディア：イベントタイプ |
      | [&#x200B; コンテンツに費やした時間](/help/reporting/metrics/content-time-spent.md) | 指標 | `mediaReporting.sessionDetails.timePlayed` | メディア：コンテンツ滞在時間 |
      | [&#x200B; メディア滞在時間](/help/reporting/metrics/media-time-spent.md) | 指標 | `mediaReporting.sessionDetails.totalTimePlayed` | メディア：メディア滞在時間 |
      | [合計一時停止期間](/help/reporting/metrics/total-pause-duration.md) | 指標 | `mediaReporting.sessionDetails.pauseTime` | メディア：合計一時停止の期間 |
      | [開始までの時間](/help/reporting/metrics/time-to-start.md) | 指標 | `mediaReporting.qoeDataDetails.timeToStart` | メディア：開始までの時間 |
      | [合計バッファー時間](/help/reporting/metrics/total-buffer-duration.md) | 指標 | `mediaReporting.qoeDataDetails.bufferTime` | メディア：合計バッファー時間 |
      | メディア セッション サーバーのタイムアウト | 指標 | `mediaReporting.sessionDetails.secondsSinceLastCall` | メディア：最後の呼び出しからの秒数 |

      >[!IMPORTANT]
      >
      >この表のコンテキストラベルは、ストリーミングメディアパネルが機能するために必要です。 Customer Journey Analyticsでは、それらを使用して、**同時視聴者数**&#x200B;および&#x200B;**再生時間**&#x200B;派生指標（[&#x200B; メディア同時視聴者数](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)および[&#x200B; メディア再生時間](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent) パネルで使用）を自動計算し、[&#x200B; メディア平均分視聴者数](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel) パネルにレポートオプションを入力します。

      この時点で、他の[&#x200B; ディメンション &#x200B;](/help/reporting/dimensions/overview.md)または[指標](/help/reporting/metrics/overview.md)をデータビューに追加できます。 各ページには、そのコンポーネントのXDM パスが一覧表示されます。

1. **[!UICONTROL 保存して続行]** → **[!UICONTROL 保存して終了]**&#x200B;を選択し、変更を保存します。

## Customer Journey Analyticsでのプロジェクトの作成と設定

1. Customer Journey Analyticsの「**[!UICONTROL Workspace]**」タブの「**[!UICONTROL プロジェクト]**」領域で、「**[!UICONTROL プロジェクトを作成]**」を選択します。

1. **[!UICONTROL 空のプロジェクト]** → **[!UICONTROL 作成]**&#x200B;を選択します。

1. 新しいプロジェクトで、以前に作成したデータビューを選択します。

   プロジェクトでパネルを作成する場合は、データビューに追加した任意のコンポーネントを使用できます。

1. 左側のパネルで「**パネル**」アイコンを選択し、**[!UICONTROL メディア平均分視聴者]**、**[!UICONTROL メディア同時視聴者数]**、**[!UICONTROL メディア再生時間]** パネルにドラッグします。

1. （条件付き）スキーマにカスタムメタデータを追加した場合は、Customer Journey Analytics ガイドの[永続性コンポーネント設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)で説明されているように、カスタムフィールドの永続性を設定します。

1. 「[&#x200B; プロジェクトを共有](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en)」の説明に従って、プロジェクトを共有します。

   >[!NOTE]
   >
   >共有するユーザーが利用できない場合は、Adobe Admin ConsoleのCustomer Journey Analyticsへのユーザーおよび管理者アクセス権を持っていることを確認します。

## Customer Journey Analyticsで使用可能なメディアパネル

Customer Journey AnalyticsのAnalysis Workspaceには、Streaming Media Collection アドオンを使用するお客様向けの3つの専用メディアパネルが含まれています。 これらのパネルには、最も一般的なストリーミングメディアのレポート作成のニーズに対応する、事前定義済みのビジュアライゼーションが用意されています。

* **[メディアの平均分視聴者数](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)**：任意の長さまたはジャンルのプログラムの平均コンテンツ消費量を比較します。 特定のコンテンツ（期間ベース）とカスタム期間モードの両方をサポートし、事後期間の分類を更新できます。
* **[メディア同時視聴者数](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)**：同時視聴者数を経時的に分析して、同時視聴者数と離脱ポイントのピークを特定します。 セグメント、ディメンション、日付範囲ごとに設定可能な粒度とシリーズ分類をサポートしています。
* **[メディア再生時間](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)**：再生時間を時間の経過に沿って分析し、ピーク期間とトラフ期間の詳細を確認します。 設定可能な粒度と出力形式（時間または分）をサポートします。

>[!MORELIKETHIS]
>
>* [&#x200B; ディメンションの概要](/help/reporting/dimensions/overview.md)
>* [指標の概要](/help/reporting/metrics/overview.md)
