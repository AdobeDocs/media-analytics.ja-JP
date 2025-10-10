---
product: adobe analytics
audience: end-user
user-guide-title: ストリーミングメディアサービスガイド
breadcrumb-title: ストリーミングメディアサービスガイド
user-guide-description: ストリーミングメディアサービスを実装します。これには、メディア SDK とメディアコレクション API が含まれます。
sub-product: media analytics
source-git-commit: efe4605d59be2629c931e3f0faca839ccb56c495
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 81%

---


# ストリーミングメディアサービスガイド {#using}

+ [Adobe streaming media services ガイド](media-overview.md)
+ リリースノート {#release-notes}
   + [Streaming Media Services リリースノート](additional-resources/release-notes.md)
+ 基本を学ぶ {#getting-started}
   + [前提条件](getting-started/prereqs.md)
   + [サポートされるデバイス](getting-started/supported-devices.md)
   + [ストリーミングメディアサービスの実装ドキュメント](getting-started/implementation-documentation.md)
   + [SDK、ライブラリおよび拡張機能](getting-started/download-sdks.md)
   + サポートの終了 {#end-of-support}
      + [Media Analytics Mobile SDK のサポート終了](additional-resources/end-of-support-faqs.md)
      + レガシー – スタンドアロンの Media SDKから Launch への移行 {#sdk-to-launch}
         + [概要](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android - Media SDK から Launch へ](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS - Media SDK から Launch へ](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript - Media SDK から Launch へ](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ 実装 {#implementation}
   + [実装の概要](implementation/overview.md)
   + Edgeの実装（推奨） {#edge-recommended}
      + [前提条件](/help/implementation/edge/prerequisites-edge.md)
      + Media Edge SDK/拡張機能 {#media-edge-sdk}
         + [Media Edge SDK／拡張機能の設定](/help/implementation/edge/implementation-edge.md)
         + [Media Edge web SDK](/help/implementation/edge/edge-web-sdk.md)
         + [Media Edge Mobile SDK](/help/implementation/edge/edge-mobile-sdk.md)
      + [Media Edge API](/help/implementation/edge/implementation-edge-api.md)
   + Adobe Analyticsのみの実装 {#analytics-only}
      + [前提条件](/help/implementation/media-sdk/setup/prerequisites-analytics.md)
      + Media SDK/拡張機能 {#media-sdk}
         + [JavaScript Web SDK](implementation/media-sdk/setup/web-implementation.md)
         + [Media Analytics 拡張機能](implementation/media-sdk/setup/web-implementation-tags.md)
         + [モバイル SDK](implementation/media-sdk/setup/mobile-implementation.md)
         + OTT SDK {#ott-setup}
            + [Chromecast SDK のインストール](implementation/media-sdk/setup/set-up-chromecast.md)
            + [Roku SDK のインストール](implementation/media-sdk/setup/set-up-roku.md)
      + Media Collection API – 実装 {#streaming-media-apis}
         + [メディアコレクション](implementation/media-collection-api/mc-api-overview.md)
         + [API クイックスタート](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
         + [Sessions リクエスト](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
         + [Events リクエスト](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
         + [リクエストパラメーター](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
         + [イベントタイプと説明](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
         + API の実装 {#mc-api-impl}
            + [プレーヤーでの HTTP リクエストタイプの設定](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
            + [セッション ID の取得](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
            + [Events リクエストの実装 &#x200B;](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
            + [JSON 検証スキーマ](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
            + [イベントリクエストの検証](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
            + [ping イベントの送信](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
            + [QoE データの送信](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
            + [カスタムメタデータのサポート](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
            + [タイムアウト条件](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
            + [イベントの順序の制御](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
            + [セッションの応答が遅い場合のイベントのキューへの登録](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + 変数 {#variables}
      + [ストリーミングメディアのパラメーター](implementation/variables/audio-video-parameters.md)
      + [広告パラメーター](implementation/variables/ad-parameters.md)
      + [チャプターパラメーター](implementation/variables/chapter-parameters.md)
      + [プレーヤーステートパラメーター &#x200B;](implementation/variables/player-state-parameters.md)
      + [品質パラメーター](implementation/variables/quality-parameters.md)
      + [計算指標 &#x200B;](implementation/variables/calculated-metrics.md)
+ レポート {#media-reports}
   + [メディアレポートの有効化](reporting/media-reports-enable.md)
   + Workspaceのメディアパネル {#media-workspace-panels}
      + [メディア分平均オーディエンスパネル](reporting/workspace/average-minute-audience.md)
      + [メディアの同時視聴者パネル](reporting/workspace/media-concurrent-viewers-overview.md)
      + [メディア再生滞在時間パネル](reporting/workspace/media-playback-time-spent.md)
   + [Workspace のメディアレポート](reporting/workspace/media-workspace-templates.md)
   + [メディアセグメント](reporting/segments.md)
   + デフォルトメディアレポート {#media-default-reports}
      + [デフォルトレポートの概要](reporting/reports-and-analytics/default-reports-overview.md)
      + [メディアの概要](reporting/reports-and-analytics/media-reports-overview.md)
      + [メディアの詳細 &#x200B;](reporting/reports-and-analytics/media-reports-detail.md)
      + [メディア視聴時間帯レポート](reporting/reports-and-analytics/media-reports-daypart.md)
      + [メディア同時ビューアレポート](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + メディア API {#media-api}
      + [同時ビューアデータの取得](reporting/reports-and-analytics/get-concurrent-json20.md)
      + [メディア再生滞在時間のデータの取得](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ ユースケース {#media-use-cases}
   + [Media SDK の使用例](use-cases/cookbook/sdk-cookbook-overview.md)
   + プレーヤーの状態のトラッキング {#player-state-tracking}
      + [概要 &#x200B;](use-cases/player-state-tracking/player-state-overview.md)
      + [標準ステートとカスタムステート](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [実装とレポート](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [複数プレーヤーのステートトラッキング](use-cases/player-state-tracking/multiple-player-states.md)
      + [プレーヤーステートトラッキングの例](use-cases/player-state-tracking/player-state-examples.md)
   + [スケジュールデータの追跡](/help/use-cases/track-schedule-data.md)
   + [ダウンロードされたコンテンツの追跡 &#x200B;](use-cases/track-downloaded-content.md)
   + [Federated Media](use-cases/federated-media.md)
   + [再生中のアプリケーション割り込みの処理](use-cases/cookbook/app-interrupts.md)
   + [メディアストリームのアトリビューション](use-cases/media-analytics-cookbook/media-dimensions.md)
   + Analytics ソースコネクタ用の XDM フィールドの移行 {#xdm-updates}
      + [ソースコネクタの新しい XDM ストリーミングメディアフィールドへの更新](/help/use-cases/xdm-updates/updated-xdm-fields.md)
      + [オーディエンスを移行](/help/use-cases/xdm-updates/migrate-audiences.md)
      + [CJA設定の移行](/help/use-cases/xdm-updates/migrate-cja-setup.md)
      + [データ準備の移行](/help/use-cases/xdm-updates/migrate-dataprep.md)
      + [プロファイルの移行](/help/use-cases/xdm-updates/migrate-profiles.md)
      + [メディアパラメーターのマッピング](/help/use-cases/xdm-updates/parameters-mapping.md)
   + [非アクティブなセッションの再開](use-cases/cookbook/resuming-inactive.md)
   + [SceneGraph での Roku トラッキング](use-cases/cookbook/sdk-track-scenegraph.md)
   + [広告間のギャップの処理](use-cases/cookbook/fix-ad-play-ad.md)
   + タイムライン {#timelines}
      + [チャプターの開始と終了](use-cases/timelines/chapter-start-end.md)
      + [コンテンツの最後まで視聴](use-cases/timelines/view-to-end-of-content.md)
      + [セッションを中断](use-cases/timelines/user-abandons-session.md)
   + OTT アプリでの Analytics の使用 {#analytics-with-ott}
      + [アプリの状態の追跡](use-cases/analytics-with-ott/track-app-states.md)
      + [アプリのアクションの追跡](use-cases/analytics-with-ott/track-app-actions.md)
      + [ユーザー ID の設定](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT と Audience Manager &#x200B;](use-cases/analytics-with-ott/ott-am.md)
      + [OTT と Experience Cloud &#x200B;](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ トラッキング {#tracking}
   + [概要](use-cases/track-av-playback/track-core-overview.md)
   + コアストリーミングメディア再生のトラック {#track-core}
      + [JavaScript 3.x でのコア再生の追跡](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
      + [Chromecast でコア再生を追跡](use-cases/track-av-playback/track-core/track-core-chromecast.md)
      + [Roku でのコア再生の追跡](use-cases/track-av-playback/track-core/track-core-roku.md)
   + バッファーの追跡 {#track-buffering}
      + [JavaScript 3.x でのバッファーの追跡](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
      + [Chromecast でのバッファーの追跡](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
      + [Roku でのバッファーの追跡](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
   + シークの追跡 {#track-seeking}
      + [JavaScript 3.x でのシークの追跡](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
      + [Chromecast でのシークの追跡](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
      + [Roku でのシークの追跡](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
   + 標準メタデータの実装 {#impl-std-metadata}
      + [JavaScript 3.x での標準メタデータの実装 &#x200B;](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
      + [Chromecast での標準メタデータの実装](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
      + [標準メタデータパラメーター - Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
      + [Roku での標準メタデータの実装 &#x200B;](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
      + [標準メタデータパラメーター - Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
   + 広告の追跡 {#track-ads}
      + [概要](use-cases/track-ads/track-ads-overview.md)
      + [JavaScript 3.x での広告の追跡](use-cases/track-ads/track-ads-js/track-ads-js3.md)
      + [Chromecast での広告の追跡](use-cases/track-ads/track-ads-chromecast.md)
      + [Roku での広告の追跡](use-cases/track-ads/track-ads-roku.md)
      + 標準広告メタデータの実装 {#impl-std-ad-metadata}
         + [JavaScript 3.x での標準広告メタデータの実装 &#x200B;](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Roku での標準広告メタデータの実装 &#x200B;](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + チャプターおよびセグメントの追跡 {#track-chapters}
      + [概要](use-cases/track-chapters/track-chapters-overview.md)
      + [JavaScript 3.x でのチャプターおよびセグメントの追跡](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Chromecast でのチャプターとセグメントの追跡](use-cases/track-chapters/track-chapters-chromecast.md)
      + [Roku でのチャプターとセグメントの追跡](use-cases/track-chapters/track-chapters-roku.md)
   + Quality of Experience の追跡 {#track-qos}
      + [概要](use-cases/track-qos/track-qos-overview.md)
      + [JavaScript 3.x での Quality of Experience の追跡](use-cases/track-qos/track-qos-js/track-qos-js3.md)
      + [Chromecast でのエクスペリエンス品質の追跡](use-cases/track-qos/track-qos-chromecast.md)
      + [Roku でのエクスペリエンス品質の追跡](use-cases/track-qos/track-qos-roku.md)
   + エラーの追跡 {#track-errors}
      + [概要](use-cases/track-errors/track-errors-overview.md)
      + [JavaScript 3.x でのエラーの追跡](use-cases/track-errors/track-errors-js/track-errors-js3.md)
      + [Chromecast でのエラーの追跡](use-cases/track-errors/track-errors-chromecast.md)
      + [Roku でのエラーの追跡](use-cases/track-errors/track-errors-roku.md)
+ プライバシーとセキュリティ {#streaming-media-privacy}
   + [オプトアウトおよびプライバシー設定](privacy/opt-out-privacy.md)
   + [セキュリティ](privacy/security.md)
+ レガシー実装 {#legacy-implementations}
   + [レガシー - 概要](legacy/setup/legacy-setup-overview.md)
   + [レガシー - SDK のダウンロード](legacy/legacy-download-sdks.md)
   + レガシー – Media SDK {#legacy-media-sdks}
      + [レガシー - Media SDK の概要](legacy/media-sdk/setup/setup-overview.md)
      + [Android のセットアップ](legacy/media-sdk/setup/set-up-android.md)
      + [iOS のセットアップ](legacy/media-sdk/setup/set-up-ios.md)
      + JavaScript のセットアップ {#setup-javascript}
         + [JavaScript 2.x のセットアップ](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [ハートビート測定について](legacy/heartbeat-measurement.md)
   + [Adobe Primetime](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Adobe Audience Management のイネーブルメント](legacy/intro-to-ava/am-enablement.md)
   + [カスタムリンクの実装](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + レガシーマイルストーンのトラッキング {#legacy-milestone-tracking}
      + [レガシーマイルストーンのトラッキング](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [マイルストーンから VA への移行](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [マイルストーンから CL への移行](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + 検証 {#validation}
      + [検証の概要](legacy/validation/validation-overview.md)
      + [テスト 1：標準の再生](legacy/validation/test1-standard-playback.md)
      + [テスト 2：メディアの中断](legacy/validation/test2-media-interrupt.md)
      + [テスト呼び出しの詳細](legacy/validation/test-call-details.md)
      + [ハートビートパラメーターの説明](legacy/validation/heartbeat-params.md)
      + デバッグ {#debugging}
         + [SDK のデバッグ](legacy/validation/debugging/sdk-debugging.md)
   + [レガシー移行：VHL 1.x から VHL 2.x へ](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [v1.x と v2.x のコードの比較](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [API 1x から 2x へのトラッキング](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [レガシー - AVA の概要](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [クライアントサイドパス](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + レガシートラッキング {#track-av-playback}
      + [Android でのコア再生の追跡](use-cases/track-av-playback/track-core/track-core-android.md)
      + [iOS でのコア再生の追跡](use-cases/track-av-playback/track-core/track-core-ios.md)
      + JavaScriptでのコア再生の追跡 {#track-core-javascript}
         + [JavaScript 2.x でのコア再生の追跡](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [Android でのバッファーの追跡](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
         + [iOS でのバッファーの追跡](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
         + JavaScriptでのバッファーの追跡 {#track-buffering-js}
            + [JavaScript 2.x でのバッファーの追跡](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [Android でのシークの追跡](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
         + [iOS でのシークの追跡](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
         + JavaScriptでのシークの追跡 {#track-seeking-js}
            + [JavaScript 2.x でのシークの追跡](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [Android での標準メタデータの実装](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [iOS での標準メタデータの実装](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS のメタデータキー](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + JavaScriptでの標準メタデータの実装 {#impl-std-md-js}
            + [JavaScript 2.x での標準メタデータの実装 &#x200B;](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + 広告の追跡 {#track-ads}
         + [Android での広告の追跡](use-cases/track-ads/track-ads-android.md)
         + [iOS での広告の追跡](use-cases/track-ads/track-ads-ios.md)
         + JavaScriptでの広告の追跡 {#track-ads-js}
            + [JavaScript 2.x での広告の追跡](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [Android での標準広告メタデータの実装 &#x200B;](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [iOS での標準広告メタデータの実装 &#x200B;](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + JavaScriptでの標準広告メタデータの実装 {#impl-std-ad-md-js}
               + [JavaScript 2.x での標準広告メタデータの実装 &#x200B;](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + チャプターおよびセグメントの追跡 {#track-chapters}
         + [Android でのチャプターとセグメントの追跡](use-cases/track-chapters/track-chapters-android.md)
         + [iOS でのチャプターおよびセグメントの追跡](use-cases/track-chapters/track-chapters-ios.md)
         + JavaScriptでのチャプターおよびセグメントの追跡 {#track-chapters-js}
            + [JavaScript 2.x でのチャプターおよびセグメントの追跡](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Android でのエクスペリエンス品質の追跡](use-cases/track-qos/track-qos-android.md)
         + [iOS でのエクスペリエンス品質の追跡](use-cases/track-qos/track-qos-ios.md)
         + JavaScriptでの Quality of Experience の追跡 {#track-qos-js}
            + [JavaScript 2.x での Quality of Experience の追跡](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + エラーの追跡 {#track-errors}
         + [Android でのエラーの追跡](use-cases/track-errors/track-errors-android.md)
         + [iOS でのエラーの追跡 &#x200B;](use-cases/track-errors/track-errors-ios.md)
         + JavaScriptでのエラーの追跡 {#track-errors-js}
            + [JavaScript 2.x でのエラーの追跡](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + 追跡シナリオ {#tracking-scenarios}
         + [広告のない VOD 再生](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [プリロール広告のある VOD 再生](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [広告がスキップされた VOD 再生](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [チャプターが 1 つある VOD 再生](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [チャプターがスキップされた VOD 再生](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [メインコンテンツでシークのある VOD 再生](use-cases/tracking-scenarios/vod-seeking.md)
         + [バッファリングがある VOD 再生](use-cases/tracking-scenarios/vod-buffering.md)
         + [同時に動作する複数の VOD トラッカー](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [複数のセッションに対応する 1 つの VOD トラッカー](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [ライブメインコンテンツ &#x200B;](use-cases/tracking-scenarios/live-main-content.md)
         + [順次トラッキングを含むライブメインコンテンツ](use-cases/tracking-scenarios/live-sequential.md)
