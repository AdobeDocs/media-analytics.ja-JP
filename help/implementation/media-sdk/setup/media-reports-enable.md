---
title: メディアレポートの有効化
description: メディア指標を収集するメディアレポートスイートについて説明します。  メディアデータを送信する前に、次の手順に従ってメディアレポートを設定します。
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
  - id: e38cbddc-1633-4cd5-bed5-9f289f2a6029
  - id: ef60b66e-5984-4336-ba72-6d978b1b6f87
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
  - id: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 503
ht-degree: 20%

---

# メディアレポートの有効化

メディア指標を収集する各レポートスイートは、メディアデータの送信前に設定しておく必要があります。

1. [Adobe Analytics](https://experience.adobe.com/analytics)で、**[!UICONTROL 管理者]** → **[!UICONTROL レポートスイート]**&#x200B;に移動します。
1. メディアデータを収集するレポートスイートを選択します。 **[!UICONTROL 設定を編集]** → **[!UICONTROL メディア管理]** → **[!UICONTROL メディアレポート]**&#x200B;を選択します。

   ![&#x200B; レポートスイートマネージャーメニューのスクリーンショット &#x200B;](assets/media-reporting.png)

1. **[!UICONTROL Media Reporting]** ページで、目的のストリーミングメディアコンポーネントを有効にします（以下を参照）。

1. **[!UICONTROL 保存].**&#x200B;を選択

   このレポートスイートが既にメディアデータを収集するように設定されている場合は、「**[!UICONTROL 保存]**」をクリックした後に、追加の設定ページが表示されます。 **[!UICONTROL メディアコア指標]**&#x200B;ページが表示されたら、次のステップへと進みます。

## 利用可能なストリーミングメディアモジュール

メディア測定には、以下のモジュールが含まれます。

* **[!UICONTROL Media Core]**：すべてのストリーミングメディアトラッキングに必要です。 コンテンツ再生とセッションデータ用のソリューション変数を予約します。
   * **ディメンション：**
      * [[!UICONTROL コンテンツ]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL &#x200B; コンテンツチャネル &#x200B;]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL &#x200B; コンテンツの長さ（変数） &#x200B;]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL &#x200B; コンテンツ名（変数） &#x200B;]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL &#x200B; コンテンツプレーヤー名]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL &#x200B; コンテンツセグメント &#x200B;]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL &#x200B; コンテンツの種類]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL &#x200B; メディアパス &#x200B;]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL &#x200B; メディアセッション ID]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL &#x200B; ストリームタイプ &#x200B;]](/help/reporting/dimensions/stream-type.md)
   * **指標：**
      * [[!UICONTROL 分平均オーディエンス]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL &#x200B; コンテンツ完了]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL &#x200B; コンテンツが再開]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL &#x200B; コンテンツセグメントビュー]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL &#x200B; コンテンツ開始]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL &#x200B; コンテンツに費やした時間]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL &#x200B; メディア開始]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL &#x200B; イベントを一時停止]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL 影響を受けるストリームを一時停止]](/help/reporting/metrics/paused-impacted-streams.md)
      * [[!UICONTROL 進行状況マーカー]](/help/reporting/metrics/progress-markers.md)
      * [[!UICONTROL 合計一時停止期間]](/help/reporting/metrics/total-pause-duration.md)
      * [[!UICONTROL &#x200B; ユニーク再生時間]](/help/reporting/metrics/unique-time-played.md)
* **[!UICONTROL メディア広告]**: メディアコンテンツ内の広告の追跡を有効にします。
   * **ディメンション：**
      * [[!UICONTROL Ad]](/help/reporting/dimensions/ad.md)
      * [[!UICONTROL &#x200B; ポッド位置の広告]](/help/reporting/dimensions/ad-in-pod-position.md)
      * [[!UICONTROL 広告の長さ（変数） &#x200B;]](/help/reporting/dimensions/ad-length.md)
      * [[!UICONTROL 広告名（変数） &#x200B;]](/help/reporting/dimensions/ad-name.md)
      * [[!UICONTROL &#x200B; プレイヤー名]](/help/reporting/dimensions/ad-player-name.md)
      * [[!UICONTROL 広告ポッド &#x200B;]](/help/reporting/dimensions/ad-pod.md)
      * [[!UICONTROL 広告主]](/help/reporting/dimensions/advertiser.md)
      * [[!UICONTROL キャンペーン ID]](/help/reporting/dimensions/campaign-id.md)
   * **分類ディメンション：**
      * [[!UICONTROL &#x200B; アセット ID]](/help/reporting/dimensions/asset-id.md)
      * [[!UICONTROL &#x200B; コンテンツの評価]](/help/reporting/dimensions/content-rating.md)
      * [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md)
      * [[!UICONTROL 最初のエア日]](/help/reporting/dimensions/first-air-date.md)
      * [[!UICONTROL 最初のデジタル日付]](/help/reporting/dimensions/first-digital-date.md)
      * [[!UICONTROL &#x200B; ポッド名]](/help/reporting/dimensions/pod-name.md)
      * [[!UICONTROL &#x200B; ポッドの位置]](/help/reporting/dimensions/pod-position.md)
   * **指標：**
      * [[!UICONTROL 広告が完了しました]](/help/reporting/metrics/ad-completes.md)
      * [[!UICONTROL 広告開始]](/help/reporting/metrics/ad-starts.md)
      * [[!UICONTROL 広告に費やした時間]](/help/reporting/metrics/ad-time-spent.md)
      * [[!UICONTROL &#x200B; メディア滞在時間]](/help/reporting/metrics/media-time-spent.md)
* **[!UICONTROL メディアチャプター]**: メディアコンテンツ内のチャプターの追跡を有効にします。
   * **Dimension:**
      * [[!UICONTROL 章]](/help/reporting/dimensions/chapter.md)
   * **分類ディメンション：**
      * [[!UICONTROL 章の長さ]](/help/reporting/dimensions/chapter-length.md)
      * [[!UICONTROL 章名]](/help/reporting/dimensions/chapter-name.md)
      * [[!UICONTROL 章のオフセット &#x200B;]](/help/reporting/dimensions/chapter-offset.md)
      * [[!UICONTROL 章の位置]](/help/reporting/dimensions/chapter-position.md)
      * [[!UICONTROL 発信元]](/help/reporting/dimensions/originator.md)
   * **指標：**
      * [[!UICONTROL 章完了]](/help/reporting/metrics/chapter-completes.md)
      * [[!UICONTROL 章開始]](/help/reporting/metrics/chapter-starts.md)
      * [[!UICONTROL 章の滞在時間]](/help/reporting/metrics/chapter-time-spent.md)
* **[!UICONTROL メディア品質]**: バッファリング、ビットレート、エラーイベントを含む再生品質データの追跡を有効にします。
   * **ディメンション：**
      * [[!UICONTROL 平均ビットレート &#x200B;]](/help/reporting/dimensions/average-bitrate.md)
      * [[!UICONTROL &#x200B; ビットレートの変更]](/help/reporting/dimensions/bitrate-changes.md)
      * [[!UICONTROL &#x200B; バッファーイベント &#x200B;]](/help/reporting/dimensions/buffer-events.md)
      * [[!UICONTROL &#x200B; フレームをドロップ &#x200B;]](/help/reporting/dimensions/dropped-frames.md)
      * [[!UICONTROL エラー]](/help/reporting/dimensions/errors.md)
      * [[!UICONTROL 外部エラーID]](/help/reporting/dimensions/external-error-ids.md)
      * [[!UICONTROL Player SDK エラーID]](/help/reporting/dimensions/player-sdk-error-ids.md)
      * [[!UICONTROL 開始までの時間]](/help/reporting/dimensions/time-to-start.md)
      * [[!UICONTROL 合計バッファー時間]](/help/reporting/dimensions/total-buffer-duration.md)
   * **指標：**
      * [[!UICONTROL 平均ビットレート &#x200B;]](/help/reporting/metrics/average-bitrate.md)
      * [[!UICONTROL &#x200B; ビットレートの変更が影響を受けるストリーム &#x200B;]](/help/reporting/metrics/bitrate-change-impacted-streams.md)
      * [[!UICONTROL &#x200B; ビットレートの変更]](/help/reporting/metrics/bitrate-changes.md)
      * [[!UICONTROL &#x200B; バッファーイベント &#x200B;]](/help/reporting/metrics/buffer-events.md)
      * [[!UICONTROL 影響を受けるストリームのバッファー]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL &#x200B; ドロップされたフレームの影響を受けるストリーム &#x200B;]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL &#x200B; フレームをドロップ &#x200B;]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL 開始する前にドロップします]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL &#x200B; エラーイベント &#x200B;]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL 影響を受けるストリームのエラー]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL 開始までの時間]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL 合計バッファー時間]](/help/reporting/metrics/total-buffer-duration.md)
* **[!UICONTROL ビデオメタデータ]**：番組、季節、ジャンルなどの標準ビデオコンテンツ属性の追跡を有効にします。
   * **ディメンション：**
      * [!UICONTROL 広告が読み込まれます]
      * [[!UICONTROL 日パート &#x200B;]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL &#x200B; エピソード &#x200B;]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL &#x200B; ジャンル &#x200B;]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL &#x200B; メディアフィードの種類]](/help/reporting/dimensions/media-feed-type.md)
      * [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL ネットワーク]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL &#x200B; シーズン &#x200B;]](/help/reporting/dimensions/season.md)
      * [[!UICONTROL 表示]](/help/reporting/dimensions/show.md)
      * [[!UICONTROL &#x200B; タイプを表示]](/help/reporting/dimensions/show-type.md)
   * **指標：**
      * [[!UICONTROL 認証済み]](/help/reporting/metrics/authorized.md)
* **[!UICONTROL オーディオメタデータ]**: アーティスト、アルバム、ステーションなどの標準オーディオコンテンツ属性のトラッキングを有効にします。
   * **ディメンション：**
      * [[!UICONTROL &#x200B; アルバム &#x200B;]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL &#x200B; アーティスト &#x200B;]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL 作成者]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL ラベル]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL 発行者]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL 駅]](/help/reporting/dimensions/station.md)
* **[!UICONTROL プレイヤーの状態トラッキング]**：フルスクリーン、クローズドキャプション、ピクチャインピクチャなどの標準的なプレイヤーUIの状態の測定を有効にします。
   * **指標：**
      * [[!UICONTROL &#x200B; クローズドキャプション数]](/help/reporting/metrics/closed-captioning-count.md)
      * [[!UICONTROL &#x200B; クローズドキャプションの合計期間]](/help/reporting/metrics/closed-captioning-total-duration.md)
      * [[!UICONTROL 全画面数]](/help/reporting/metrics/full-screen-count.md)
      * [[!UICONTROL 全画面表示の合計期間]](/help/reporting/metrics/full-screen-total-duration.md)
      * [[!UICONTROL &#x200B; フォーカス数]](/help/reporting/metrics/in-focus-count.md)
      * [[!UICONTROL &#x200B; フォーカス合計期間]](/help/reporting/metrics/in-focus-total-duration.md)
      * [[!UICONTROL 分数]](/help/reporting/metrics/mute-count.md)
      * [[!UICONTROL 合計期間]分](/help/reporting/metrics/mute-total-duration.md)
      * [[!UICONTROL &#x200B; ピクチャインピクチャ数]](/help/reporting/metrics/picture-in-picture-count.md)
      * [[!UICONTROL &#x200B; ピクチャの合計期間]](/help/reporting/metrics/picture-in-picture-total-duration.md)
      * [クローズドキャプションの影響を受ける[!UICONTROL &#x200B; ストリーム &#x200B;]](/help/reporting/metrics/closed-captioning-streams-impacted.md)
      * [フルスクリーンの影響を受ける[!UICONTROL &#x200B; ストリーム &#x200B;]](/help/reporting/metrics/full-screen-streams-impacted.md)
      * [フォーカスの影響を受ける[!UICONTROL &#x200B; ストリーム &#x200B;]](/help/reporting/metrics/in-focus-streams-impacted.md)
      * [ミュート ]の影響を受ける[[!UICONTROL &#x200B; ストリーム]](/help/reporting/metrics/mute-streams-impacted.md)
      * [[!UICONTROL &#x200B; ピクチャインピクチャの影響を受けるストリーム &#x200B;]](/help/reporting/metrics/picture-in-picture-streams-impacted.md)
