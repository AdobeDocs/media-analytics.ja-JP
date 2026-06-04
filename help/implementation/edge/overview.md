---
title: Edgeの導入の概要
description: Edge Networkを通じてストリーミングメディアデータを収集するために必要なAdobe Experience Platform スキーマ、データセット、データストリームを設定します。
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 6%

---

# Edgeの導入の概要

Adobe Experience Platform Edge Networkでは、複数の製品向けのデータを1つのエンドポイントに送信し、各製品に適切な情報を転送できます。 これにより、複数のデータソリューションの実装作業が統合され、Adobe AnalyticsとCustomer Journey Analyticsの両方にStreaming Media Collectionを導入することをお勧めします。

Web SDK、モバイルSDK（iOSまたはAndroid）、Roku SDK、Media Edge APIなど、使用するコードベースに関係なく、最初にこのページで説明されているプラットフォーム設定を完了する必要があります。

## 前提条件

1. **一般的な前提条件を完了します。** [一般的な前提条件](/help/getting-started/prereqs.md)を参照してください。

1. **互換性のあるAdobe ソリューションを確認します。** Customer Journey Analytics、Adobe Analytics、Adobe Journey Optimizer、またはReal-Time Customer Data Platformの実装が正常に動作している必要があります。
   * [Customer Journey Analytics ガイド](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=ja)
   * [Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)
   * [Adobe Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
   * [Real-Time Customer Data Platform ドキュメント](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=ja)

## Adobe Experience Platformでのスキーマの設定

Adobe Adobe Experience Platformを使用するアプリケーションをまたいでデータ収集を標準化するために、Adobeは、一般に公開されているオープンなExperience Data Model （XDM）標準を開発しました。

1. Adobe Experience Platformで、[UIでのスキーマの作成と編集](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)の説明に従って、スキーマの作成を開始します。

1. スキーマの詳細ページで、スキーマのベースクラスとして&#x200B;**[!UICONTROL Experience Event]**&#x200B;を選択します。

   ![ フィールドグループを追加](assets/schema-experience-event.png)

1. 「**[!UICONTROL 次へ]**」を選択します。

1. スキーマの表示名と説明を指定し、**[!UICONTROL 終了]**&#x200B;を選択します。

1. **[!UICONTROL 構成]**&#x200B;領域の&#x200B;**[!UICONTROL フィールドグループ]** セクションで、**[!UICONTROL 追加]**&#x200B;を選択し、次のフィールドグループを検索してスキーマに追加します。
   * `End User ID Details`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   フィールドグループを追加すると、**[!UICONTROL フィールドグループ]** セクションに表示されます。

   ![ フィールドグループを追加](assets/schema-field-groups-added.png)

1. **[!UICONTROL 保存]**&#x200B;を選択して、変更を保存します。

1. （オプション） Media Edge APIで使用されていない特定のフィールドを非表示にできます。 これらのフィールドを非表示にすると、スキーマは読みやすくなりますが、必須ではありません。 これらのフィールドは、`MediaAnalytics Interaction Details` フィールドグループ内のフィールドのみを参照します。

   +++ 展開すると、非表示にできるフィールドに関する手順が表示されます。

   1. **[!UICONTROL 構造]**&#x200B;領域で、`Media Collection Details` フィールドを選択し、**[!UICONTROL 関連フィールドの管理]**&#x200B;を選択します。

      ![関連フィールドの管理](assets/manage-related-fields.png)

   1. 「**[!UICONTROL フィールドの表示名を表示する]**」オプションを有効にし、次のようにスキーマを更新します。

      * `Media Collection Details` > `Advertising Details` フィールドで、次のレポートフィールドを非表示にします：`Ad Completed`、`Ad Started`、および`Ad Time Played`。

      * `Media Collection Details` > `Advertising Pod Details` フィールドで、次のレポートフィールドを非表示にします：`Ad Break ID`

      * `Media Collection Details` > `Chapter Details` フィールドで、次のレポートフィールドを非表示にします：`Chapter Completed`、`Chapter ID`、`Chapter Started`、および`Chapter Time Played`。

      * `Media Collection Details` フィールドで、`List Of States` フィールドを非表示にします。

        ![ メディア コレクションの状態を非表示](assets/schema-hide-media-collection-states.png)

      * `Media Collection Details` > `List Of States End`および`Media Collection Details` > `List Of States Start` フィールドで、次のレポートフィールドを非表示にします：`Player State Count`、`Player State Set`、および`Player State Time`。

        非表示にする![ フィールド ](assets/schema-hide-listofstates.png)

      * `Media Collection Details` > `Qoe Data Details` フィールドで、次のレポートフィールドを非表示にします：`Average Bitrate`、`Average Bitrate Bucket`、`Bitrate Change Impacted Streams`、`Bitrate Changes`、`Buffer Impacted Streams`、`Buffer Events`、`Dropped Frame Impacted Streams`、`Drops Before Starts`、`Errors`、`External Error IDs`、`Error Impacted Streams`、`Media SDK Error IDs`、`Player SDK Error IDs`、`Stalling Impacted Streams`、`Stalling Events`、`Total Buffer Duration`、および`Total Stalling Duration`。

      * `Media Collection Details` > `Session Details` フィールドで、次のレポートフィールドを非表示にします：`10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID`, `Media Session Server Timeout`, `Pause Events`, `Pause Impacted Streams`, `Pccr`, `Total Pause Duration`, `Unique Time Played`および`Video Segment`。`Media Time Spent``Pev3`

   1. **[!UICONTROL 確認]**&#x200B;を選択して変更を保存します。

   1. **[!UICONTROL 構造]**&#x200B;領域で、**[!UICONTROL フィールドの表示名を表示]**&#x200B;するオプションを有効にし、`List Of Media Collection Downloaded Content Events` フィールドを選択します。

   1. 「**[!UICONTROL 関連フィールドを管理]**」を選択し、次のようにスキーマを更新します。

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` フィールドで、次のレポートフィールドを非表示にします：`Ad Completed`、`Ad Started`、および`Ad Time Played`。

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` フィールドで、次のレポートフィールドを非表示にします：`Ad Break ID`

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` フィールドで、次のレポートフィールドを非表示にします：`Chapter Completed`、`Chapter ID`、`Chapter Started`、および`Chapter Time Played`。

      * `List Of Media Collection Downloaded Content Events` > `Media Details` フィールドで、`List Of States` フィールドを非表示にします。

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End`および`Media Collection Details` > `List Of States Start` フィールドで、次のレポートフィールドを非表示にします：`Player State Count`、`Player State Set`、および`Player State Time`。

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` フィールドで、次のレポートフィールドを非表示にします：`Average Bitrate`、`Average Bitrate Bucket`、`Bitrate Change Impacted Streams`、`Bitrate Changes`、`Buffer Events`、`Buffer Impacted Streams`、`Drops Before Starts`、`Dropped Frame Impacted Streams`、`Error Impacted Streams`、`Errors`、`External Error IDs`、`Media SDK Error IDs`、`Player SDK Error IDs`、`Stalling Events`、`Stalling Impacted Streams`、`Total Buffer Duration`および`Total Stalling Duration`。

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` フィールドで、次のレポートフィールドを非表示にします：`10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID`, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pccr`, `Pev3`, `Total Pause Duration`、`Unique Time Played`、`Video Segment`。`Media Starts``Pause Impacted Streams`

      * `List Of Media Collection Downloaded Content Events` > `Media Details` フィールドで、`Media Session ID` フィールドを非表示にします。

   1. **[!UICONTROL 確認]**&#x200B;を選択して変更を保存します。

   1. **[!UICONTROL 構造]**&#x200B;領域で、`Media Reporting Details` フィールドを選択し、**[!UICONTROL 関連フィールドの管理]**&#x200B;を選択します。

   1. 「**[!UICONTROL フィールドの表示名を表示する]**」オプションを有効にし、次のようにスキーマを更新します。

      * `Media Reporting Details` フィールドで、次のフィールドを非表示にします：`Error Details`、`List Of States End`、`List of States Start`、および`Media Session ID`。

   1. **[!UICONTROL 確認]** > **[!UICONTROL 保存]**&#x200B;を選択して、変更を保存します。

   +++

1. （オプション）カスタムメタデータをスキーマに追加できます。 これにより、特定のニーズやコンテキストに応じて、ユーザー定義のメタデータを追加で含めることができます。 Media Edge APIを使用したカスタムメタデータについて詳しくは、[ カスタムメタデータのサポート ](custom-metadata.md)を参照してください。

   +++ 展開して、スキーマにカスタムメタデータを追加する手順を表示します。

   1. **[!UICONTROL アカウント情報]** > **[!UICONTROL 割り当てられた組織]** > [!UICONTROL _**組織名**_] > **[!UICONTROL テナント]**&#x200B;を選択して、組織のテナント名を探します。

      カスタムフィールドは、このパスを通じて受信されます。 （例えば、テナント名：_dcbl → myCustomField パス：_dcbl.myCustomField）。

   1. 定義したメディアスキーマにカスタムフィールドグループを追加します。

      ![add-custom-metadata](assets/add-custom-metadata-fieldgroup.png)

   1. 追跡するカスタムフィールドをフィールドグループに追加します。

      ![add-custom-metadata](assets/add-custom-fields.png)

   1. [ リクエストペイロードのカスタムフィールドに生成されたパス ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/fields/overview#type-specific-properties)を使用します。

      ![add-custom-metadata](assets/custom-fields-path.png)

   +++

1. [Adobe Experience Platformでデータセットを作成](#create-a-dataset-in-adobe-experience-platform)します。

## Adobe Experience Platform でデータセットを作成

1. [Adobe Experience Platformでのスキーマの設定](#set-up-the-schema-in-adobe-experience-platform)の説明に従って、スキーマを設定していることを確認してください。

1. Adobe Experience Platformで、[ データセット UI ガイド ](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=ja#create)の説明に従って、データセットの作成を開始します。

   データセットのスキーマを選択する際には、以前に作成したスキーマを選択します。

1. [Adobe Experience Platformでデータストリームを設定](#configure-a-datastream-in-adobe-experience-platform)します。

## Adobe Experience Platformでのデータストリームの設定

1. 「[Adobe Experience Platformでデータセットを作成する](#create-a-dataset-in-adobe-experience-platform)」の説明に従ってデータセットを作成していることを確認してください。

1. 「[ データストリームの設定](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=ja)」の説明に従って、新しいデータストリームを作成します。

   データストリームを作成する際に、次の選択を行います。

   * 「**[!UICONTROL イベントスキーマ]**」フィールドで、[で作成したスキーマを選択し、Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform)でスキーマを設定します。 「**[!UICONTROL 保存]**」を選択します。

     >[!IMPORTANT]
     >
     >「**[!UICONTROL マッピングを保存して追加]**」を選択しないでください。選択すると、タイムスタンプフィールドのマッピングエラーが発生します。

     ![ データストリームを作成してスキーマを選択](assets/datastream-create-schema.png)

   * Adobe AnalyticsとCustomer Journey Analyticsのどちらを使用しているかに応じて、次のいずれかのサービスをデータストリームに追加します。

      * **[!UICONTROL Adobe Analytics]** （Adobe Analyticsを使用している場合）

        Adobe Analyticsを使用している場合は、[ レポートスイートの作成](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite)の説明に従ってレポートスイートを定義します。

      * **[!UICONTROL Adobe Experience Platform]** （Customer Journey Analyticsを使用している場合）

     データストリームへのサービスの追加について詳しくは、[ データストリームの設定](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details)の「データストリームへのサービスの追加」を参照してください。

     ![Adobe Analytics サービスを追加](assets/datastream-add-service.png)

   * **[!UICONTROL 詳細オプション]**&#x200B;を展開し、**[!UICONTROL Media Analytics]** オプションを有効にします。

     ![ メディア分析オプション ](assets/datastream-media-check.png)

## 実装方法の選択

スキーマ、データセットおよびデータストリームを配置した状態で、次のいずれかのコードベースを実装して、Edge Networkへのストリーミングメディアデータの送信を開始します。 各ページは、ストリーミングメディア固有の設定をカバーしています。イベントごとのコードと変数ごとのコードは、[ イベント ](/help/implementation/events/overview.md)と[変数](/help/implementation/variables/overview.md)にあります。

| Codebase | インコード | タグ経由 |
|---|---|---|
| Web | [Web SDK](web-sdk.md) | [Web SDK タグ拡張機能](web-sdk-tags.md) |
| iOS | [iOS](ios.md) | [iOS （Tags） ](ios-tags.md) |
| Android | [Android](android.md) | [Android （Tags） ](android-tags.md) |
| Roku | [Roku](roku.md) | — |
| API | [Media Edge API](media-edge-api.md) | — |

## 次の手順

データの収集を開始したら、レポートを設定できます。

* [Edge実装のレポートの設定](/help/reporting/setup/edge-reporting.md) （Customer Journey Analytics）
* [Analyticsのみの実装に対するレポートの設定](/help/reporting/setup/analytics-reporting.md) （データストリームがAdobe Analyticsにフィードしている場合）

>[!MORELIKETHIS]
>
>* [ カスタムメタデータのサポート ](custom-metadata.md)
>* [XDM レポートスキーマ ](reporting-schema.md)
>* [ イベントの概要](/help/implementation/events/overview.md)
