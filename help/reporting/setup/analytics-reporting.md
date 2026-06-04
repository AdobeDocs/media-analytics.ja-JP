---
title: Analyticsのみの実装用のレポートの設定
description: Adobe Analyticsのメディアレポートスイートモジュールを有効にして、ストリーミングメディアデータを収集およびレポートできるようにします。
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 9%

---

# Analyticsのみの実装用のレポートの設定

Analyticsのみの実装でストリーミングメディアデータを収集する前に、そのデータを受信する各レポートスイートを設定して、適切なメディアモジュールを有効にする必要があります。 このページでは、これらのモジュールを有効にする方法と、結果のレポートを検索する場所について説明します。

* **前提条件**: Adobe Analyticsの実装。 [Analyticsのみの実装の概要](/help/implementation/analytics-only/overview.md)と、選択した実装方法を参照してください。

## レポートスイートでメディアレポートを有効にする

メディア指標を収集する各レポートスイートは、メディアデータの送信前に設定しておく必要があります。

1. [Adobe Analytics](https://experience.adobe.com/analytics)で、**[!UICONTROL 管理者]** → **[!UICONTROL レポートスイート]**&#x200B;に移動します。
1. メディアデータを収集するレポートスイートを選択します。 **[!UICONTROL 設定を編集]** → **[!UICONTROL メディア管理]** → **[!UICONTROL メディアレポート]**&#x200B;を選択します。

   ![ レポートスイートマネージャーメニューのスクリーンショット ](assets/media-reporting.png)

1. **[!UICONTROL Media Reporting]** ページで、目的のストリーミングメディアモジュールを有効にします（以下を参照）。

1. **[!UICONTROL 保存].**&#x200B;を選択

   このレポートスイートが既にメディアデータを収集するように設定されている場合、**[!UICONTROL 保存]**&#x200B;を選択すると、追加の設定ページが表示されます。 **[!UICONTROL メディアコア指標]**&#x200B;ページが表示されたら、次のステップへと進みます。

## 利用可能なストリーミングメディアモジュール

メディア測定には、以下のモジュールが含まれます。

* **[!UICONTROL Media Core]**：すべてのストリーミングメディアトラッキングに必要です。 コンテンツ再生とセッションデータ用のソリューション変数を予約します。
   * **ディメンション：**
      * [[!UICONTROL コンテンツ]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL  コンテンツチャネル ]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL  コンテンツの長さ（変数） ]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL  コンテンツ名（変数） ]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL  コンテンツプレーヤー名]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL  コンテンツセグメント ]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL  コンテンツの種類]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL  メディアパス ]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL  メディアセッション ID]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL  ストリームタイプ ]](/help/reporting/dimensions/stream-type.md)
   * **指標：**
      * [[!UICONTROL 分平均オーディエンス]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL  コンテンツ完了]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL  コンテンツが再開]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL  コンテンツセグメントビュー]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL  コンテンツ開始]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL  コンテンツに費やした時間]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL  メディア開始]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL  イベントを一時停止]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL 影響を受けるストリームを一時停止]](/help/reporting/metrics/paused-impacted-streams.md)
      * [[!UICONTROL 進行状況マーカー]](/help/reporting/metrics/progress-markers.md)
      * [[!UICONTROL 合計一時停止期間]](/help/reporting/metrics/total-pause-duration.md)
      * [[!UICONTROL  ユニーク再生時間]](/help/reporting/metrics/unique-time-played.md)
* **[!UICONTROL メディア広告]**: メディアコンテンツ内の広告の追跡を有効にします。
   * **ディメンション：**
      * [[!UICONTROL Ad]](/help/reporting/dimensions/ad.md)
      * [[!UICONTROL  ポッド位置の広告]](/help/reporting/dimensions/ad-in-pod-position.md)
      * [[!UICONTROL 広告の長さ（変数） ]](/help/reporting/dimensions/ad-length.md)
      * [[!UICONTROL 広告名（変数） ]](/help/reporting/dimensions/ad-name.md)
      * [[!UICONTROL  プレイヤー名]](/help/reporting/dimensions/ad-player-name.md)
      * [[!UICONTROL 広告ポッド ]](/help/reporting/dimensions/ad-pod.md)
      * [[!UICONTROL 広告主]](/help/reporting/dimensions/advertiser.md)
      * [[!UICONTROL キャンペーン ID]](/help/reporting/dimensions/campaign-id.md)
   * **分類ディメンション：**
      * [[!UICONTROL  アセット ID]](/help/reporting/dimensions/asset-id.md)
      * [[!UICONTROL  コンテンツの評価]](/help/reporting/dimensions/content-rating.md)
      * [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md)
      * [[!UICONTROL 最初のエア日]](/help/reporting/dimensions/first-air-date.md)
      * [[!UICONTROL 最初のデジタル日付]](/help/reporting/dimensions/first-digital-date.md)
      * [[!UICONTROL  ポッド名]](/help/reporting/dimensions/pod-name.md)
      * [[!UICONTROL  ポッドの位置]](/help/reporting/dimensions/pod-position.md)
   * **指標：**
      * [[!UICONTROL 広告が完了しました]](/help/reporting/metrics/ad-completes.md)
      * [[!UICONTROL 広告開始]](/help/reporting/metrics/ad-starts.md)
      * [[!UICONTROL 広告に費やした時間]](/help/reporting/metrics/ad-time-spent.md)
      * [[!UICONTROL  メディア滞在時間]](/help/reporting/metrics/media-time-spent.md)
* **[!UICONTROL メディアチャプター]**: メディアコンテンツ内のチャプターの追跡を有効にします。
   * **Dimension:**
      * [[!UICONTROL 章]](/help/reporting/dimensions/chapter.md)
   * **分類ディメンション：**
      * [[!UICONTROL 章の長さ]](/help/reporting/dimensions/chapter-length.md)
      * [[!UICONTROL 章名]](/help/reporting/dimensions/chapter-name.md)
      * [[!UICONTROL 章のオフセット ]](/help/reporting/dimensions/chapter-offset.md)
      * [[!UICONTROL 章の位置]](/help/reporting/dimensions/chapter-position.md)
      * [[!UICONTROL 発信元]](/help/reporting/dimensions/originator.md)
   * **指標：**
      * [[!UICONTROL 章完了]](/help/reporting/metrics/chapter-completes.md)
      * [[!UICONTROL 章開始]](/help/reporting/metrics/chapter-starts.md)
      * [[!UICONTROL 章の滞在時間]](/help/reporting/metrics/chapter-time-spent.md)
* **[!UICONTROL メディア品質]**: バッファリング、ビットレート、エラーイベントを含む再生品質データの追跡を有効にします。
   * **ディメンション：**
      * [[!UICONTROL 平均ビットレート ]](/help/reporting/dimensions/average-bitrate.md)
      * [[!UICONTROL  ビットレートの変更]](/help/reporting/dimensions/bitrate-changes.md)
      * [[!UICONTROL  バッファーイベント ]](/help/reporting/dimensions/buffer-events.md)
      * [[!UICONTROL  フレームをドロップ ]](/help/reporting/dimensions/dropped-frames.md)
      * [[!UICONTROL エラー]](/help/reporting/dimensions/errors.md)
      * [[!UICONTROL 外部エラーID]](/help/reporting/dimensions/external-error-ids.md)
      * [[!UICONTROL Player SDK エラーID]](/help/reporting/dimensions/player-sdk-error-ids.md)
      * [[!UICONTROL 開始までの時間]](/help/reporting/dimensions/time-to-start.md)
      * [[!UICONTROL 合計バッファー時間]](/help/reporting/dimensions/total-buffer-duration.md)
   * **指標：**
      * [[!UICONTROL 平均ビットレート ]](/help/reporting/metrics/average-bitrate.md)
      * [[!UICONTROL  ビットレートの変更が影響を受けるストリーム ]](/help/reporting/metrics/bitrate-change-impacted-streams.md)
      * [[!UICONTROL  ビットレートの変更]](/help/reporting/metrics/bitrate-changes.md)
      * [[!UICONTROL  バッファーイベント ]](/help/reporting/metrics/buffer-events.md)
      * [[!UICONTROL 影響を受けるストリームのバッファー]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL  ドロップされたフレームの影響を受けるストリーム ]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL  フレームをドロップ ]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL 開始する前にドロップします]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL  エラーイベント ]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL 影響を受けるストリームのエラー]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL 開始までの時間]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL 合計バッファー時間]](/help/reporting/metrics/total-buffer-duration.md)
* **[!UICONTROL ビデオメタデータ]**：番組、季節、ジャンルなどの標準ビデオコンテンツ属性の追跡を有効にします。
   * **ディメンション：**
      * [[!UICONTROL 広告が読み込まれます]](/help/reporting/dimensions/ad-load-type.md)
      * [[!UICONTROL 日パート ]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL  エピソード ]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL  ジャンル ]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL  メディアフィードの種類]](/help/reporting/dimensions/media-feed-type.md)
      * [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL ネットワーク]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL  シーズン ]](/help/reporting/dimensions/season.md)
      * [[!UICONTROL 表示]](/help/reporting/dimensions/show.md)
      * [[!UICONTROL  タイプを表示]](/help/reporting/dimensions/show-type.md)
   * **指標：**
      * [[!UICONTROL 認証済み]](/help/reporting/metrics/authorized.md)
* **[!UICONTROL オーディオメタデータ]**: アーティスト、アルバム、ステーションなどの標準オーディオコンテンツ属性のトラッキングを有効にします。
   * **ディメンション：**
      * [[!UICONTROL  アルバム ]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL  アーティスト ]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL 作成者]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL ラベル]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL 発行者]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL 駅]](/help/reporting/dimensions/station.md)
* **[!UICONTROL プレイヤーの状態トラッキング]**：フルスクリーン、クローズドキャプション、ピクチャインピクチャなどの標準的なプレイヤーUIの状態の測定を有効にします。
   * **指標：**
      * [[!UICONTROL  クローズドキャプション数]](/help/reporting/metrics/closed-captioning-count.md)
      * [[!UICONTROL  クローズドキャプションの合計期間]](/help/reporting/metrics/closed-captioning-total-duration.md)
      * [[!UICONTROL 全画面数]](/help/reporting/metrics/full-screen-count.md)
      * [[!UICONTROL 全画面表示の合計期間]](/help/reporting/metrics/full-screen-total-duration.md)
      * [[!UICONTROL  フォーカス数]](/help/reporting/metrics/in-focus-count.md)
      * [[!UICONTROL  フォーカス合計期間]](/help/reporting/metrics/in-focus-total-duration.md)
      * [[!UICONTROL 分数]](/help/reporting/metrics/mute-count.md)
      * [[!UICONTROL 合計期間]分](/help/reporting/metrics/mute-total-duration.md)
      * [[!UICONTROL  ピクチャインピクチャ数]](/help/reporting/metrics/picture-in-picture-count.md)
      * [[!UICONTROL  ピクチャの合計期間]](/help/reporting/metrics/picture-in-picture-total-duration.md)
      * [クローズドキャプションの影響を受ける[!UICONTROL  ストリーム ]](/help/reporting/metrics/closed-captioning-streams-impacted.md)
      * [フルスクリーンの影響を受ける[!UICONTROL  ストリーム ]](/help/reporting/metrics/full-screen-streams-impacted.md)
      * [フォーカスの影響を受ける[!UICONTROL  ストリーム ]](/help/reporting/metrics/in-focus-streams-impacted.md)
      * [ミュート ]の影響を受ける[!UICONTROL  ストリーム](/help/reporting/metrics/mute-streams-impacted.md)
      * [[!UICONTROL  ピクチャインピクチャの影響を受けるストリーム ]](/help/reporting/metrics/picture-in-picture-streams-impacted.md)

>[!MORELIKETHIS]
>
>* [Workspaceのメディア レポート ](/help/reporting/workspace/media-workspace-templates.md)
>* [ ディメンションの概要](/help/reporting/dimensions/overview.md)
>* [指標の概要](/help/reporting/metrics/overview.md)
