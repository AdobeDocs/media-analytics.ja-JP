---
audience: end-user
user-guide-title: ストリーミングメディア用 Adobe Analytics
breadcrumb-title: ストリーミングメディア解析ガイド
user-guide-description: ストリーミングメディア用にAdobe Analyticsを実装します。 これには、メディア SDK とメディアコレクション API が含まれます。
product: adobe analytics
sub-product: Media Analytics
translation-type: tm+mt
source-git-commit: 640005cbd90a074a1a441865c4b6abc8f94c1277
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 94%

---


# ストリーミングメディア用 Adobe Analytics {#using}

+ [Adobe Analyticsでのストリーミングメディアの測定](media-overview.md)
+ [サポートされるデバイスとプラットフォーム](measurement-options/supported-devices.md)
+ ストリーミングメディア解析の概要{#intro-to-ava}
   + [前提条件](intro-to-ava/prereqs.md)
   + 実装パス {#implementation-paths}
      + [概要](intro-to-ava/implementation-paths/implementation-paths.md)
      + [クライアントサイド ](intro-to-ava/implementation-paths/client-side-path.md)
      + その他の実装パス {#other-paths}
         + メディアモジュールのマイルストーンの追跡 {#mm-milestone-tracking}
            + [マイルストーンの概要](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [マイルストーンから Media Analytics への移行](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [マイルストーンからカスタムリンクへの移行](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Analytics のカスタムリンク {#cl-in-aa}
            + [カスタムリンク導入ガイド](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [Audience Manager の有効化](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [Media Analytics SDK のサポート終了に関する FAQ](sdk-implement/end-of-support-faqs.md)
   + [SDK のダウンロード](sdk-implement/download-sdks.md)
   + セットアップと設定 {#setup}
      + [概要](sdk-implement/setup/setup-overview.md)
      + [Android のセットアップ](sdk-implement/setup/set-up-android.md)
      + [iOS のセットアップ](sdk-implement/setup/set-up-ios.md)
      + JavaScript のセットアップ {#setup-javascript}
         + [JavaScript 2.x のセットアップ](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [JavaScript 3.x のセットアップ](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [Chromecast のセットアップ ](sdk-implement/setup/set-up-chromecast.md)
      + [Roku のセットアップ ](sdk-implement/setup/set-up-roku.md)
   + ストリーミングメディア再生を追跡{#track-av-playback}
      + [概要](sdk-implement/track-av-playback/track-core-overview.md)
      + コアストリーミングメディア再生の追跡{#track-core}
         + [Android でのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [iOS でのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + JavaScript でのコア再生の追跡 {#track-core-javascript}
            + [JavaScript 2.x でのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [JavaScript 3.x でのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Chromecast でのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Roku でのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + バッファーの追跡 {#track-buffering}
         + [Android でのバッファーの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [iOS でのバッファーの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + JavaScript でのバッファーの追跡 {#track-buffering-js}
            + [JavaScript 2.x でのバッファーの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [JavaScript 3.x でのバッファーの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Chromecast でのバッファーの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Roku でのバッファーの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + シークの追跡 {#track-seeking}
         + [Android でのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [iOS でのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + JavaScript でのシークの追跡 {#track-seeking-js}
            + [JavaScript 2.x でのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [JavaScript 3.x でのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Chromecast でのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Roku でのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + 標準メタデータの実装 {#impl-std-metadata}
         + [Android での標準メタデータの実装](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [iOS での標準メタデータの実装](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS のメタデータキー](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + JavaScript での標準メタデータの実装 {#impl-std-md-js}
            + [JavaScript 2.x での標準メタデータの実装 ](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [JavaScript 3.x での標準メタデータの実装 ](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Chromecast での標準メタデータの実装](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [標準メタデータパラメーター - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Roku での標準メタデータの実装](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [標準メタデータパラメーター - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + 広告の追跡 {#track-ads}
      + [概要](sdk-implement/track-ads/track-ads-overview.md)
      + [Android での広告の追跡](sdk-implement/track-ads/track-ads-android.md)
      + [iOS での広告の追跡](sdk-implement/track-ads/track-ads-ios.md)
      + JavaScript での広告の追跡 {#track-ads-js}
         + [JavaScript 2.x での広告の追跡](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [JavaScript 3.x での広告の追跡](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [Chromecast での広告の追跡](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Roku での広告の追跡](sdk-implement/track-ads/track-ads-roku.md)
      + 標準広告メタデータの実装 {#impl-std-ad-metadata}
         + [Android での標準広告メタデータの実装](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [iOS での標準広告メタデータの実装](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + JavaScript での標準広告メタデータの実装 {#impl-std-ad-md-js}
            + [JavaScript 2.x での標準広告メタデータの実装 ](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [JavaScript 3.x での標準広告メタデータの実装 ](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Roku での標準広告メタデータの実装](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + チャプターおよびセグメントの追跡 {#track-chapters}
      + [概要](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Android でのチャプターおよびセグメントの追跡](sdk-implement/track-chapters/track-chapters-android.md)
      + [iOS でのチャプターおよびセグメントの追跡](sdk-implement/track-chapters/track-chapters-ios.md)
      + JavaScript でのチャプターおよびセグメントの追跡 {#track-chapters-js}
         + [JavaScript 2.x でのチャプターおよびセグメントの追跡](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [JavaScript 3.x でのチャプターおよびセグメントの追跡](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Chromecast でのチャプターおよびセグメントの追跡](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Roku でのチャプターおよびセグメントの追跡](sdk-implement/track-chapters/track-chapters-roku.md)
   + Quality of Experience の追跡 {#track-qos}
      + [概要](sdk-implement/track-qos/track-qos-overview.md)
      + [Android での Quality of Experience の追跡](sdk-implement/track-qos/track-qos-android.md)
      + [iOS での Quality of Experience の追跡](sdk-implement/track-qos/track-qos-ios.md)
      + JavaScript での Quality of Experience の追跡 {#track-qos-js}
         + [JavaScript 2.x での Quality of Experience の追跡](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [JavaScript 3.x での Quality of Experience の追跡](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [Chromecast での Quality of Experience の追跡](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Roku での Quality of Experience の追跡](sdk-implement/track-qos/track-qos-roku.md)
   + エラーの追跡 {#track-errors}
      + [概要](sdk-implement/track-errors/track-errors-overview.md)
      + [Android でのエラーの追跡](sdk-implement/track-errors/track-errors-android.md)
      + [iOS でのエラーの追跡](sdk-implement/track-errors/track-errors-ios.md)
      + JavaScript でのエラーの追跡 {#track-errors-js}
         + [JavaScript 2.x でのエラーの追跡](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [JavaScript 3.x でのエラーの追跡](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [Chromecast でのエラーの追跡](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Roku でのエラーの追跡](sdk-implement/track-errors/track-errors-roku.md)
   + [オプトアウトおよびプライバシー](sdk-implement/opt-out-privacy.md)
   + 追跡シナリオ {#tracking-scenarios}
      + [広告のない VOD 再生](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [プリロール広告のある VOD 再生](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [広告がスキップされた VOD 再生](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [チャプターが 1 つある VOD 再生](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [チャプターがスキップされた VOD 再生](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [メインコンテンツでのシークのある VOD 再生](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [バッファリングがある VOD 再生](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [同時に複数の VOD トラッカー](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [複数のセッションに対する 1 つの VOD トラッカー](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [ライブメインコンテンツ](sdk-implement/tracking-scenarios/live-main-content.md)
      + [順次追跡を含むライブメインコンテンツ](sdk-implement/tracking-scenarios/live-sequential.md)
   + 検証 {#validation}
      + [検証の概要](sdk-implement/validation/validation-overview.md)
      + [テスト 1：標準の再生](sdk-implement/validation/test1-standard-playback.md)
      + [テスト 2：メディアの中断](sdk-implement/validation/test2-media-interrupt.md)
      + [テスト呼び出しの詳細](sdk-implement/validation/test-call-details.md)
      + [ハートビートパラメーターの説明](sdk-implement/validation/heartbeat-params.md)
      + デバッグ {#debugging}
         + [SDK のデバッグ](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Adobe Debug の設定](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [新しいデバッグレポートの作成](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [デバッグのダッシュボードとレポート](sdk-implement/validation/debugging/debug-dash-repts.md)
   + OTT アプリでの Analytics {#analytics-with-ott}
      + [アプリの状態の追跡](sdk-implement/analytics-with-ott/track-app-states.md)
      + [アプリのアクションの追跡](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [ユーザー ID の設定](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT と Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT と Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + クックブック {#cookbook}
      + [SDK クックブック](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [再生中のアプリケーション割り込みの処理](sdk-implement/cookbook/app-interrupts.md)
      + [広告と広告の間に発生する main:play の解決](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [非アクティブなセッションの再開](sdk-implement/cookbook/resuming-inactive.md)
      + [SceneGraph（Roku）でのトラッキング](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Media Analytics 1.x から 2.x への移行 {#va-1x-to-2x}
      + [移行の概要](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [コードの比較：1.x と 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [1.x から 2.x API への変換](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Media Analytics SDK から Launch への移行 {#sdk-to-launch}
      + [SDK から Launch への移行](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + SDK から Launch への移行プラットフォームガイド {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ メディアコレクション API（RESTful） {#media-collection-api}
   + [概要](media-collection-api/mc-api-overview.md)
   + API リファレンス {#mc-api-ref}
      + [Sessions リクエスト](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Events リクエスト](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [リクエストパラメーター](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [イベントタイプと説明](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [JSON 検証スキーマ](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + API の実装 {#mc-api-impl}
      + [クイックスタート](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [プレーヤーでの HTTP リクエストタイプの設定](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [セッション ID の取得](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Events リクエストの実装](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [イベントリクエストの検証](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [ping イベントの送信](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [QoE データの送信](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [カスタムメタデータのサポート](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [タイムアウト条件](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [イベントの順序の制御](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [セッションの応答が遅い場合のイベントのキューへの登録](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + メディアトラッキングタイムライン {#mc-api-timelines}
      + [タイムライン 1 - コンテンツの最後まで視聴](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [タイムライン 2 - ユーザーが中断したセッション](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [タイムライン 3 - チャプター](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ クックブック {#media-analytics-cookbook}
   + [クックブック](media-analytics-cookbook/media-analytics-cookbook.md)
   + [メディアストリームアトリビューション](media-analytics-cookbook/media-dimensions.md)
+ 指標とメタデータ {#metrics-and-metadata}
   + [ストリーミングメディアのパラメータ](metrics-and-metadata/audio-video-parameters.md)
   + [広告パラメーター](metrics-and-metadata/ad-parameters.md)
   + [チャプターパラメーター](metrics-and-metadata/chapter-parameters.md)
   + [プレーヤーステートパラメーター ](metrics-and-metadata/player-state-parameters.md)
   + [品質パラメーター](metrics-and-metadata/quality-parameters.md)
   + [セグメント](metrics-and-metadata/segments.md)
   + [計算指標](metrics-and-metadata/calculated-metrics.md)
+ レポートと分析 {#media-reports}
   + [メディアレポートの有効化](media-reports/media-reports-enable.md)
   + メディアのデフォルトレポート {#media-default-reports}
      + [デフォルトレポートの概要](media-reports/media-default-reports/default-reports-overview.md)
      + [メディアの概要](media-reports/media-default-reports/media-reports-overview.md)
      + [メディアの詳細](media-reports/media-default-reports/media-reports-detail.md)
      + [メディア視聴時間帯レポート](media-reports/media-default-reports/media-reports-daypart.md)
      + [メディア同時ビューアレポート](media-reports/media-default-reports/media-concurrent-viewers.md)
   + メディアワークスペースパネル{#media-workspace-panels}
      + [メディアの同時視聴者パネル](media-reports/media-workspace-panels/media-concurrent-viewers.md)
   + [Media Workspace のテンプレート](media-reports/media-workspace-templates.md)
   + [APIを使用した同時ビューアデータの取得](media-reports/media-default-reports/get-concurrent-json20.md)
+ [ダウンロードされたコンテンツの追跡](media-collection-api/track-downloaded-content.md)
+ プレーヤーステートトラッキング {#player-state-tracking}
   + [概要](sdk-implement/player-state-tracking/player-state-overview.md)
   + [標準ステートとカスタムステート](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [実装とレポート](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [プレーヤーステートトラッキングの例](sdk-implement/player-state-tracking/player-state-examples.md)
+ [Federated Analytics](federated-analytics.md)
<!-- + Player State Tracking {#player-state-tracking}
    + [Overview](sdk-implement/player-state-tracking/player-state-overview.md)
    + [Standard and custom states](sdk-implement/player-state-tracking/standard-and-custom-states.md)
    + [Implementation and reporting](sdk-implement/player-state-tracking/implementation-and-reporting.md)
    + [Player state tracking examples](sdk-implement/player-state-tracking/player-state-examples.md) -->
+ その他のリソース {#additional-resources}
   + [リリースノート](additional-resources/doc-updates.md)
