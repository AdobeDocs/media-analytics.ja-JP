---
title: ストリーミングメディア用 Analyticsの実装を設定する最初の手順
description: メディアストリーミングAdobeの実装方法を説明します。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 29d58b41-9a49-4b71-bdc5-4e2848cd3236
source-git-commit: b57db92ae4ce01e259424e3d71e36311af88ccac
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 11%

---

# Media Edge を使用した Media Analytics のExperience Platform

Adobe Experience Platform Edge を使用すると、複数の製品用のデータを一元的な場所に送信できます。Experience Edge は、適切な情報を目的の製品に転送します。この概念を使用すると、特に複数のデータソリューションにまたがる実装作業を統合できます。

次の図は、Media Analytics の実装で、Experience Platformエッジを使用して、Analysis WorkspaceでAdobe AnalyticsまたはCustomer Journey Analyticsのどちらでデータを使用できるかを示しています。

![CJA ワークフロー](assets/cja-implementation.png)

Experience PlatformEdge を使用しない実装方法を含む、すべての実装オプションの概要については、 [ストリーミングメディアのAdobe AnalyticsまたはCustomer Journey Analyticsへの実装](/help/implementation/overview.md).

>[!IMPORTANT]
>
>ストリーミングメディアは、まだ AEP Web SDK と統合されていません。

Mobile SDK または API のどちらを使用して Experience Edge を使用したストリーミングメディアを実装しているかに関係なく、最初に次の節を完了する必要があります。

## Adobe Experience Platformでのスキーマの設定

Adobe Experience Platform を活用するアプリケーション間で使用するデータ収集を標準化するために、アドビはオープンで公的に文書化された標準である Experience Data Model（XDM）を作成しました。

スキーマを作成して設定するには、次の手順を実行します。

1. Adobe Experience Platformで、 [UI でのスキーマの作成と編集](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

   スキーマを作成する場合は、「 [!UICONTROL **XDM ExperienceEvent**] から [!UICONTROL **スキーマを作成**] ドロップダウンメニュー。

1. 内 [!UICONTROL **構成**] 領域、 [!UICONTROL **フィールドグループ**] セクション、選択 [!UICONTROL **追加**]&#x200B;を検索し、次の新しいフィールドグループをスキーマに追加します。
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   フィールドグループを追加した後、「 [!UICONTROL **フィールドグループ**] セクションの説明を次に示します。

   ![追加されたフィールドグループ](assets/schema-field-groups-added.png)


この節の次の手順はオプションです。Media Edge API へのリクエストは、AEP スキーマ UI で指定されたフィールドを非表示にしなくても機能します。
ただし、非表示のフィールドは Media Edge API で使用されないので、フィールドを非表示にすると、スキーマが読みやすく理解しやすくなります。
次の手順は、 `MediaAnalytics Interaction Details` fieldgroup.

1. 内 [!UICONTROL **構造**] 領域で、 `Media Collection Details` フィールド、選択 [!UICONTROL **関連するフィールドの管理**]&#x200B;次の手順に従ってスキーマを更新します。

   ![manage-related-fields](assets/manage-related-fields.png)

   * 内 `Media Collection Details` フィールド、非表示 `List Of States` フィールドに入力します。

     ![メディアコレクションの状態を非表示にする](assets/schema-hide-media-collection-states.png)

   * 内 `Media Collection Details` > `Advertising Details` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Ad Completed`, `Ad Started`、および `Ad Time Played`.

   * 内 `Media Collection Details` > `Advertising Pod Details` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Ad Break ID`

   * 内 `Media Collection Details` > `Chapter Details` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Chapter ID`, `Chapter Completed`, `Chapter Started`、および `Chapter Time Played`.

   * 内 `Media Collection Details` > `Qoe Data Details` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`、および `Total Stalling Duration`.

   * 内 `Media Collection Details` > `Session Details` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`、および `Pccr`.

   * 内 `Media Collection Details` > `List Of States End` および `Media Collection Details` > `List Of States Start` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Player State Count`, `Player State Set`、および `Player State Time`.

     ![非表示にするフィールド](assets/schema-hide-listofstates.png)

1. 選択 [!UICONTROL **確認**] 変更を保存します。

1. 内 [!UICONTROL **構造**] 領域で、 `List Of Media Collection Downloaded Content Events` フィールド、選択 [!UICONTROL **関連するフィールドの管理**]&#x200B;次の手順に従ってスキーマを更新します。

   * 内 `List Of Media Collection Downloaded Content Events` > `Media Details` フィールド、非表示 `List Of States` フィールドに入力します。

   * 内 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Ad Completed`, `Ad Started`、および `Ad Time Played`.

   * 内 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Ad Break ID`

   * 内 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Chapter ID`, `Chapter Completed`, `Chapter Started`、および `Chapter Time Played`.

   * 内 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`、および `Total Stalling Duration`.

   * 内 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`、および `Pccr`.

   * 内 `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` および `Media Collection Details` > `List Of States Start` 「 」フィールドで、次のレポートフィールドを非表示にします。 `Player State Count`, `Player State Set`、および `Player State Time`.

   * 内 `List Of Media Collection Downloaded Content Events` > `Media Details`  フィールド、非表示 `Media Session ID` フィールドに入力します。

1. 選択 [!UICONTROL **確認**] 変更を保存します。

1. 内 [!UICONTROL **構造**] 領域で、 `Media Reporting Details` フィールド、選択 [!UICONTROL **関連するフィールドの管理**]&#x200B;次の手順に従ってスキーマを更新します。

   * 内 `Media Reporting Details` 次のフィールドを非表示にします。 `Error Details`, `List Of States End`, `List of States Start`、および `Media Session ID`.

1. 選択 [!UICONTROL **確認**] > [!UICONTROL **保存**]  変更を保存します。

1. 続行 [Adobe Experience Platformでのデータセットの作成](#create-a-dataset-in-adobe-experience-platform).

## Adobe Experience Platformでのデータセットの作成

1. スキーマが [Adobe Experience Platformでのスキーマの設定](#set-up-the-schema-in-adobe-experience-platform).

1. Adobe Experience Platformで、 [データセット UI ガイド](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=ja#create).

   データセットのスキーマを選択する際に、以前に作成したスキーマを選択します。詳しくは、 [Adobe Experience Platformでのスキーマの設定](#set-up-the-schema-in-adobe-experience-platform).

1. 続行 [データストリームのCustomer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

## Adobe Experience Platformでのデータストリームの設定

1. データセットを作成したことを確認します ( [Adobe Experience Platformでのデータセットの作成](#create-a-dataset-in-adobe-experience-platform).

1. 新しいデータストリームの作成 ( [データストリームの設定](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=ja).

   データストリームを作成する場合は、次の設定を選択します。

   * 内 [!UICONTROL **イベントスキーマ**] フィールドでデータストリームを作成する場合、 [Adobe Experience Platformでのスキーマの設定](#set-up-the-schema-in-adobe-experience-platform). 「[!UICONTROL **保存**]」を選択します。

     >[!IMPORTANT]
     >
         > 選択しない [!UICONTROL **マッピングの保存と追加**] そうすると、「タイムスタンプ」フィールドでマッピングエラーが発生します。
     
     ![データストリームの作成とスキーマの選択](assets/datastream-create-schema.png)

   * Adobe AnalyticsとCustomer Journey Analyticsのどちらを使用しているかに応じて、次のいずれかのサービスをデータストリームに追加します。

      * [!UICONTROL **Adobe Analytics**] (Adobe Analyticsを使用する場合 )

        Adobe Analyticsを使用している場合は、「 [レポートスイートの定義](#define-a-report-suite) 」を参照してください。

      * [!UICONTROL **Adobe Experience Platform**] (Customer Journey Analyticsを使用する場合 )

     データストリームにサービスを追加する方法について詳しくは、 [データストリームの設定](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

     ![Adobe Analyticsサービスの追加](assets/datastream-add-service.png)

   * 展開 [!UICONTROL **詳細オプション**]、次にを有効にします。 [!UICONTROL **Media Analytics**] オプション。

     ![Media Analytics オプション](assets/datastream-media-check.png)

1. 続行 [Customer Journey Analyticsでの接続の作成](#create-a-connection-in-customer-journey-analytics).

## Customer Journey Analytics で接続を作成する

>[!NOTE]
>
>次の手順は、Customer Journey Analyticsを使用する場合にのみ必要です。


1. データストリームを作成したことを確認します ( [データストリームのCustomer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

1. Customer Journey Analyticsで、 [接続の作成](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=ja).

   接続を作成する場合、ストリーミングメディアを実装するには、次の設定が必要です。

   1. 以前に作成したデータセットを選択します。詳しくは、 [Adobe Experience Platformでのデータセットの作成](#create-a-dataset-in-adobe-experience-platform).

   1. 次を確認します。 [!UICONTROL **すべての新しいデータをインポート**] の設定が有効になっています。

1. 続行 [Customer Journey Analyticsでのデータビューの作成](#create-a-new-data-view-in-customer-journey-analytics).

## Customer Journey Analyticsでのデータビューの作成

>[!NOTE]
>
>次の手順は、Customer Journey Analyticsを使用する場合にのみ必要です。

1. 接続がCustomer Journey Analyticsで作成されていることを確認します ( [Customer Journey Analyticsでの接続の作成](#create-a-connection-in-customer-journey-analytics).

1. 顧客ジャーニー分析で、 [データビューの作成または編集](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=ja).

   データビューを作成する場合、ストリーミングメディアの実装には、次の設定が必要です。

   1. 内 [!UICONTROL **接続**] 「 」フィールドで、以前に作成した接続を選択します。 [Customer Journey Analyticsでの接続の作成](#create-a-connection-in-customer-journey-analytics).

      作成した接続が選択できるようになるまでに、最大 15 分かかる場合があります。

   1. の [!UICONTROL **コンポーネント**] タブ、 [!UICONTROL **スキーマフィールド**] 「 」セクションで、以下の表に示す各コンポーネントを検索し、 [!UICONTROL **指標**] パネル。 同じ名前のフィールドが複数存在する場合は、XDM パスを使用して、そのフィールドが正しいことを確認します。

      **メインコンテンツ — コンテンツ指標**

      | コンポーネント名 | XDM パス |
      |----------|---------|
      | メディア開始 | mediaReporting.sessionDetails.isViewed |
      | メディアセグメント表示 | mediaReporting.sessionDetails.hasSegmentView |
      | コンテンツ開始 | mediaReporting.sessionDetails.isPlayed |
      | コンテンツ完了 | mediaReporting.sessionDetails.isCompleted |
      | コンテンツ視聴時間 | mediaReporting.sessionDetails.timePlayed |
      | メディア視聴時間 | mediaReporting.sessionDetails.totalTimePlayed |
      | ユニーク再生時間 | mediaReporting.sessionDetails.uniqueTimePlayed |
      | 10％プログレスマーカー | mediaReporting.sessionDetails.hasProgress10 |
      | 分平均オーディエンス | mediaReporting.sessionDetails.averageMinuteAudience |


      **チャプターおよび広告 — チャプターおよび広告の指標**

      | コンポーネント名 | XDM パス |
      |----------|---------|
      | チャプター開始済み | mediaReporting.chapterDetails.isStarted |
      | チャプター完了 | mediaReporting.chapterDetails.isCompleted |
      | チャプター再生時間 | mediaReporting.chapterDetails.timePlayed |
      | 広告開始済み | mediaReporting.advertisingDetails.isStarted |
      | 広告完了 | mediaReporting.advertisingDetails.isCompleted |
      | 広告の再生時間 | mediaReporting.advertisingDetails.timePlayed |


      **QoE - QoE 指標**

      | コンポーネント名 | XDM パス |
      |----------|---------|
      | 開始時間 | mediaReporting.qoeDataDetails.timeToStart |
      | 開始前にドロップ | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | バッファーの影響を受けたストリーム | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | ビットレート変更の影響を受けたストリーム | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | ビットレート変更 | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | 平均ビットレート | mediaReporting.qoeDataDetails.bitrateAverage |
      | ドロップフレーム | mediaReporting.qoeDataDetails.droppedFrames |
      | エラー | mediaReporting.qoeDataDetails.errorCount |
      | エラーの影響を受けたストリーム | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | ドロップフレームの影響を受けたストリーム | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |


      **プレーヤーステート — プレーヤーステート指標**

      | コンポーネント名 | XDM パス |
      |----------|---------|
      | プレーヤーステートセット | mediaReporting.states.isSet |
      | プレーヤーステートカウント | mediaReporting.states.count |
      | プレーヤーステートタイム | mediaReporting.states.time |


   1. ラベルを更新します ( [!UICONTROL **コンテキストラベル**] ドロップダウンメニュー ) を次の表に示します。 指標パネルにまだ表示されていないコンポーネントを検索して、パネルにドラッグします。

      | コンポーネント名 | コンテキストラベル |
      |---------|----------|
      | メディアセッションサーバーのタイムアウト | メディア：前回の呼び出しからの経過時間（秒） |
      | メディア視聴時間 | メディア：メディア視聴時間 |
      | 合計バッファー時間 | メディア：合計バッファー時間 |
      | 開始時間 | メディア：開始時間 |
      | 一時停止時間合計 | メディア：一時停止時間合計 |

   1. 分類をCustomer Journey Analyticsプロジェクトに追加するには、次のディメンションを [!UICONTROL **Dimension**] パネル：

      | XDM パス | コンポーネント名 |
      |---------|----------|
      | mediaReporting.states.name | プレーヤーステート名 |
      | mediaReporting.sessionDetails.ID | メディアセッション ID |

      このテーブルのディメンションに加えて、Customer Journey Analyticsプロジェクトでデータをフィルタリングするために使用可能にする他のディメンションも追加できます。

1. 選択 [!UICONTROL **保存して続行**] > [!UICONTROL **保存して終了**] 変更を保存します。

1. 続行 [プロジェクトの作成とCustomer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## プロジェクトの作成とCustomer Journey Analytics

1. データビューがCustomer Journey Analyticsで作成されていることを確認します。詳しくは、 [Customer Journey Analyticsでのデータビューの作成](#create-a-new-data-view-in-customer-journey-analytics).

1. Customer Journey Analytics内、 [!UICONTROL **Workspace**] タブ、 [!UICONTROL **プロジェクト**] 領域、選択 [!UICONTROL **プロジェクトを作成**].

1. 選択 [!UICONTROL **空のプロジェクト**] > [!UICONTROL **作成**].

1. 新しいプロジェクトで、以前に作成したデータビューを選択します。

   プロジェクトでパネルを作成する際には、データビューに追加した任意のコンポーネントを使用できます。詳しくは、 [Customer Journey Analyticsでのデータビューの作成](#create-a-new-data-view-in-customer-journey-analytics).

   次の 4 つのパネルは、作成可能なパネルの例です。

   ![メインコンテンツパネル](assets/main-content-panel.png)

   ![チャプターと広告のパネル](assets/chapter-and-ads-panel.png)

   ![QoE パネル](assets/qoe-panel.png)

   ![プレーターステートパネル](assets/player-state-panel.png)

1. を選択します。 **パネル** アイコンをクリックし、 [!UICONTROL **メディア同時閲覧者数**] パネルと [!UICONTROL **メディア再生に費やした時間**] パネル。

   2 つのパネルは次のようになります。

   ![メディア同時閲覧者パネル](assets/media-concurrent-viewers-panels.png)

   ![メディア再生に費やした時間パネル](assets/media-playback-time-spent-panels.png)

1. プロジェクトを共有します。詳しくは、 [プロジェクトの共有](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=ja).

   >[!NOTE]
   >
   >   共有したいユーザーが使用できない場合は、そのユーザーがAdobe Admin ConsoleのCustomer Journey Analyticsに対するユーザーおよび管理者アクセス権を持っていることを確認してください。

1. 続行 [データをExperience PlatformEdge に送信](#send-data-to-experience-platform-edge).

## AEP Mobile SDK を使用したExperience PlatformEdge へのデータ送信

Adobe Experience Platform mobile SDK を使用して、モバイルデータを Experience Platform Edge に送信できます。

次のドキュメントリソースを使用して、iOSと Android の両方の実装を完了します。

* [はじめに](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [API リファレンス](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [Edge Network 拡張機能のAdobeストリーミングメディアへの移行](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

または、以下のリソースを使用して Edge API のカスタム実装を使用できます。

* [メディアエッジ API の概要](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [Media Edge API の概要](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [メディア Edge API トラブルシューティングガイド](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [Media Edge API 用の Open API 仕様ファイルの使用](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/swagger.html)
