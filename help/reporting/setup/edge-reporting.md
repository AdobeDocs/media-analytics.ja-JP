---
title: Edge実装用のレポートの設定
description: Edge Networkを通じて収集されたストリーミングメディアデータをレポートするようにCustomer Journey Analyticsを設定します。
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 18%

---

# Edge実装用のレポートの設定

Edge Networkを使用してStreaming Media Collectionを実装したら、収集したデータをレポートするようにCustomer Journey Analyticsを設定します。 このページでは、ストリーミングメディア用の接続、データビューおよびプロジェクトの作成方法について説明します。

>[!NOTE]
>
>このページでは、Edge実装の推奨される宛先であるCustomer Journey Analyticsでのレポートについて説明します。 データストリームがストリーミングメディアデータをAdobe Analyticsに送信する場合は、[Analyticsのみの実装に対するレポートの設定](analytics-reporting.md)を参照してください。

* **前提条件**: Edgeの実装を完了し、データを収集します。 [Edgeの実装の概要](/help/implementation/edge/overview.md)と、選択した実装方法を参照してください。

## Customer Journey Analytics で接続を作成する

1. Customer Journey Analyticsで、[Create a connection](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=ja)の説明に従って接続を作成します。

   接続を作成する場合、ストリーミングメディアには次の選択が必要です。

   1. 実装中に作成したデータセットを選択します。

   1. **[!UICONTROL すべての新しいデータの読み込み]**&#x200B;設定が有効になっていることを確認してください。

1. [Customer Journey Analyticsでデータビューを作成します](#create-a-data-view-in-customer-journey-analytics)。

## Customer Journey Analytics でデータビューを作成

1. Customer Journey Analyticsで、[&#x200B; データビューの作成または編集](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=ja)の説明に従ってデータビューを作成します。

   1. 「**[!UICONTROL 接続]**」フィールドで、以前に作成した接続を選択します。

      新しい接続を選択できるようになるまでに最大15分かかる場合があります。

   1. 「**[!UICONTROL コンポーネント]**」タブの「**[!UICONTROL スキーマフィールド]**」セクションで、下のテーブルで各コンポーネントを検索し、**[!UICONTROL 指標]** パネルにドラッグします。 同じ名前のフィールドが複数ある場合は、XDM パスを使用して正しいフィールドを確認します。

      **メインコンテンツ – コンテンツ指標**

      | コンポーネント名 | XDM パス |
      |----------|---------|
      | メディア開始 | mediaReporting.sessionDetails.isViewed |
      | メディアセグメント表示 | mediaReporting.sessionDetails.hasSegmentView |
      | コンテンツ開始 | mediaReporting.sessionDetails.isPlayed |
      | コンテンツ完了 | mediaReporting.sessionDetails.isCompleted |
      | コンテンツ視聴時間 | mediaReporting.sessionDetails.timePlayed |
      | メディア視聴時間 | mediaReporting.sessionDetails.totalTimePlayed |
      | ユニーク再生時間 | mediaReporting.sessionDetails.uniqueTimePlayed |
      | 10%進捗状況マーカー | mediaReporting.sessionDetails.hasProgress10 |
      | 分平均オーディエンス | mediaReporting.sessionDetails.averageMinuteAudience |

      **章と広告 – 章と広告の指標**

      | コンポーネント名 | XDM パス |
      |----------|---------|
      | 章の始め | mediaReporting.chapterDetails.isStarted |
      | 章が完了しました | mediaReporting.chapterDetails.isCompleted |
      | 章再生時間 | mediaReporting.chapterDetails.timePlayed |
      | 広告が開始されました | mediaReporting.advertisingDetails.isStarted |
      | Ad Completed | mediaReporting.advertisingDetails.isCompleted |
      | 広告再生時間 | mediaReporting.advertisingDetails.timePlayed |

      **QoE - QoE指標**

      | コンポーネント名 | XDM パス |
      |----------|---------|
      | 開始時間 | mediaReporting.qoeDataDetails.timeToStart |
      | 起動前にドロップ | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | バッファーの影響を受けたストリーム | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | ビットレート変更の影響を受けたストリーム | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | ビットレート変更 | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | 平均ビットレート | mediaReporting.qoeDataDetails.bitrateAverage |
      | ドロップフレーム | mediaReporting.qoeDataDetails.droppedFrames |
      | エラー数 | mediaReporting.qoeDataDetails.errorCount |
      | エラーの影響を受けたストリーム | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | ドロップフレームの影響を受けたストリーム | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |

      **プレイヤーの状態 – プレイヤーの状態の指標**

      | コンポーネント名 | XDM パス |
      |----------|---------|
      | Player State Set | mediaReporting.states.isSet |
      | プレーヤーの状態カウント | mediaReporting.states.count |
      | プレーヤーの状態時間 | mediaReporting.states.time |

   1. 次の表のコンポーネントのラベル（**[!UICONTROL コンテキストラベル]** ドロップダウンメニュー）を更新します。 指標パネルにまだ含まれていないコンポーネントを検索してパネルにドラッグします。

      | コンポーネント名 | コンテキストラベル |
      |---------|----------|
      | メディアセッションサーバーのタイムアウト | メディア：最後の呼び出しからの秒数 |
      | メディア視聴時間 | メディア：メディア滞在時間 |
      | 合計バッファー時間 | メディア：合計バッファー時間 |
      | 開始時間 | メディア：開始までの時間 |
      | 一時停止時間合計 | メディア：合計一時停止の期間 |

   1. プロジェクトに分類を追加するには、**[!UICONTROL ディメンション]** パネルに次のディメンションを追加します。

      | XDM パス | コンポーネント名 |
      |---------|----------|
      | mediaReporting.states.name | プレーヤーの状態名 |
      | mediaReporting.sessionDetails.ID | メディアセッション ID |

      この表のディメンションに加えて、プロジェクトでデータをフィルタリングする他のディメンションを追加できます。

1. **[!UICONTROL 保存して続行]** > **[!UICONTROL 保存して終了]**&#x200B;を選択し、変更を保存します。

1. [Customer Journey Analyticsでプロジェクトを作成して設定します](#create-and-configure-a-project-in-customer-journey-analytics)。

## Customer Journey Analyticsでのプロジェクトの作成と設定

1. Customer Journey Analyticsの「**[!UICONTROL Workspace]**」タブの「**[!UICONTROL プロジェクト]**」領域で、「**[!UICONTROL プロジェクトを作成]**」を選択します。

1. **[!UICONTROL 空のプロジェクト]** > **[!UICONTROL 作成]**&#x200B;を選択します。

1. 新しいプロジェクトで、以前に作成したデータビューを選択します。

   プロジェクトでパネルを作成する場合は、データビューに追加した任意のコンポーネントを使用できます。

1. 左側のパネルで&#x200B;**パネル** アイコンを選択し、**[!UICONTROL メディア同時視聴者数]** パネルと&#x200B;**[!UICONTROL メディア再生時間]** パネルをドラッグします。

1. （条件付き）スキーマにカスタムメタデータを追加した場合は、Customer Journey Analytics ガイドの[永続性コンポーネント設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)で説明されているように、カスタムフィールドの永続性を設定します。

1. 「[&#x200B; プロジェクトを共有](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en)」の説明に従って、プロジェクトを共有します。

   >[!NOTE]
   >
   >共有するユーザーが利用できない場合は、Adobe Admin ConsoleのCustomer Journey Analyticsへのユーザーおよび管理者アクセス権を持っていることを確認します。

>[!MORELIKETHIS]
>
>* Workspaceの[&#x200B; メディアパネル &#x200B;](/help/reporting/workspace/media-concurrent-viewers-overview.md)
>* [&#x200B; ディメンションの概要](/help/reporting/dimensions/overview.md)
>* [指標の概要](/help/reporting/metrics/overview.md)
