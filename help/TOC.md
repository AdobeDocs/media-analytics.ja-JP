---
product: Media Analytics
audience: end-user
user-guide-title: オーディオおよびビデオ用Adobe Analytics
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Adobe Analytics for Audio and Video {#using}

+ [Adobe Analyticsでのオーディオおよびビデオの測定](media-overview.md)
+ Measurement Options {#measurement-options}
   + Media Module Milestone Tracking {#mm-milestone-tracking}
      + [マイルストーンの概要](measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Media Analyticsへのマイルストーンの移行](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [マイルストーンからカスタムリンクへの移行](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Analytics のカスタムリンク {#cl-in-aa}
      + [カスタムリンク導入ガイド](measurement-options/cl-in-aa/cl-impl-guide.md)
+ オーディオおよびビデオ分析の概要 {#intro-to-ava}
   + [前提条件](intro-to-ava/prereqs.md)
   + 実装パス {#implementation-paths}
      + [概要](intro-to-ava/implementation-paths/implementation-paths.md)
      + [クライアント側](intro-to-ava/implementation-paths/client-side-path.md)
      + [Adobe Experience Platform Launch](intro-to-ava/implementation-paths/launch-path.md)
      + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
   + [Audience Manager の有効化](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [SDK のダウンロード](sdk-implement/download-sdks.md)
   + セットアップと設定 {#setup}
      + [概要](sdk-implement/setup/setup-overview.md)
      + [Android のセットアップ](sdk-implement/setup/set-up-android.md)
      + [iOS のセットアップ](sdk-implement/setup/set-up-ios.md)
      + [JavaScript のセットアップ](sdk-implement/setup/set-up-js.md)
      + [Chromecast のセットアップ](sdk-implement/setup/set-up-chromecast.md)
      + [Roku のセットアップ](sdk-implement/setup/set-up-roku.md)
   + オーディオとビデオの再生の追跡 {#track-av-playback}
      + [概要](sdk-implement/track-av-playback/track-core-overview.md)
      + Track Core Audio and Video Playback {#track-core}
         + [Androidでのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [iOSでのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + [JavaScriptでのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-js.md)
         + [Chromecastでのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Rokuでのコア再生の追跡](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Track Buffering {#track-buffering}
         + [Androidでのバッファリングの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [iOSでのバッファリングの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + [JavaScriptでのバッファリングの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-js.md)
         + [Chromecastでのバッファリングの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Rokuでのバッファリングの追跡](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Track Seeking {#track-seeking}
         + [Androidでのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [iOSでのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + [JavaScriptでのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-js.md)
         + [Chromecastでのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Rokuでのシークの追跡](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + 標準メタデータの実装 {#impl-std-metadata}
         + [Android での標準メタデータの実装](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [iOS での標準メタデータの実装](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOSメタデータキー](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + [JavaScript での標準メタデータの実装](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)
         + [Chromecast での標準メタデータの実装](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [標準メタデータパラメーター- Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Roku での標準メタデータの実装](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [標準メタデータパラメーター- Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + 広告の追跡 {#track-ads}
      + [概要](sdk-implement/track-ads/track-ads-overview.md)
      + [Androidでの広告の追跡](sdk-implement/track-ads/track-ads-android.md)
      + [iOSでの広告の追跡](sdk-implement/track-ads/track-ads-ios.md)
      + [JavaScriptでの広告の追跡](sdk-implement/track-ads/track-ads-js.md)
      + [Chromecastでの広告の追跡](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Rokuの広告の追跡](sdk-implement/track-ads/track-ads-roku.md)
      + 標準広告メタデータの実装 {#impl-std-ad-metadata}
         + [Android での標準広告メタデータの実装](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [iOS での標準広告メタデータの実装](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + [JavaScript での標準広告メタデータの実装](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
         + [Roku での標準広告メタデータの実装](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + チャプターおよびセグメントの追跡 {#track-chapters}
      + [概要](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Android上のチャプターとセグメントの追跡](sdk-implement/track-chapters/track-chapters-android.md)
      + [iOS上のチャプターとセグメントの追跡](sdk-implement/track-chapters/track-chapters-ios.md)
      + [JavaScript上のチャプターとセグメントの追跡](sdk-implement/track-chapters/track-chapters-js.md)
      + [Chromecastのチャプターとセグメントの追跡](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Rokuのチャプターとセグメントの追跡](sdk-implement/track-chapters/track-chapters-roku.md)
   + Quality of Experience の追跡 {#track-qos}
      + [概要](sdk-implement/track-qos/track-qos-overview.md)
      + [Androidでのエクスペリエンスの追跡の品質](sdk-implement/track-qos/track-qos-android.md)
      + [iOSでのエクスペリエンスの追跡の品質](sdk-implement/track-qos/track-qos-ios.md)
      + [JavaScriptでのエクスペリエンスの追跡の品質](sdk-implement/track-qos/track-qos-js.md)
      + [Chromecastでのエクスペリエンスの追跡の品質](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Rokuでのエクスペリエンスのトラック品質](sdk-implement/track-qos/track-qos-roku.md)
   + Track Errors {#track-errors}
      + [概要](sdk-implement/track-errors/track-errors-overview.md)
      + [Androidでのエラーの追跡](sdk-implement/track-errors/track-errors-android.md)
      + [iOSでのエラーの追跡](sdk-implement/track-errors/track-errors-ios.md)
      + [JavaScriptでのエラーの追跡](sdk-implement/track-errors/track-errors-js.md)
      + [Chromecastでのエラーの追跡](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Rokuでのエラーの追跡](sdk-implement/track-errors/track-errors-roku.md)
   + [オプトアウトとプライバシー](sdk-implement/opt-out-privacy.md)
   + Tracking Scenarios {#tracking-scenarios}
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
      + [テスト2:メディア中断](sdk-implement/validation/test2-media-interrupt.md)
      + [テストコールの詳細](sdk-implement/validation/test-call-details.md)
      + [ハートビートパラメーターの説明](sdk-implement/validation/heartbeat-params.md)
      + デバッグ {#debugging}
         + [SDKデバッグ](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Adobe Debug の設定](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [新しいデバッグレポートの作成](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [デバッグのダッシュボードとレポート](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analytics in OTT Apps {#analytics-with-ott}
      + [アプリの状態の追跡](sdk-implement/analytics-with-ott/track-app-states.md)
      + [アプリのアクションの追跡](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [ユーザーIDの設定](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT と Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT と Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + クックブック {#cookbook}
      + [再生中のアプリケーション割り込みの処理](sdk-implement/cookbook/app-interrupts.md)
      + [広告と広告の間に発生する main:play の解決](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [非アクティブセッションの再開](sdk-implement/cookbook/resuming-inactive.md)
      + [SceneGraph（Roku）でのトラッキング](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Media Analytics 1.x to 2.x Migration {#va-1x-to-2x}
      + [移行の概要](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [コードの比較：1.x と 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [1.x から 2.x API への変換](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
+ メディア収集API（RESTful） {#media-collection-api}
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
      + [セッションの応答が遅いときのイベントのキューへの登録](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Media Tracking Timelines {#mc-api-timelines}
      + [タイムライン 1 - コンテンツの最後まで視聴](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [タイムライン 2 - ユーザーが中断したセッション](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [タイムライン 3 - チャプター](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
   + [ダウンロードしたコンテンツの追跡](media-collection-api/track-downloaded-content.md)
+ 指標とメタデータ {#metrics-and-metadata}
   + [オーディオおよびビデオのパラメーター](metrics-and-metadata/audio-video-parameters.md)
   + [広告パラメーター](metrics-and-metadata/ad-parameters.md)
   + [チャプターパラメーター](metrics-and-metadata/chapter-parameters.md)
   + [品質パラメーター](metrics-and-metadata/quality-parameters.md)
   + [セグメント](metrics-and-metadata/segments.md)
   + [計算指標](metrics-and-metadata/calculated-metrics.md)
+ Reporting and Analysis {#media-reports}
   + [メディアレポートの有効化](media-reports/media-reports-enable.md)
   + Media Default Reports {#media-default-reports}
      + [デフォルトのレポートの概要](media-reports/media-default-reports/default-reports-overview.md)
      + [メディアの概要](media-reports/media-default-reports/media-reports-overview.md)
      + [メディアの詳細](media-reports/media-default-reports/media-reports-detail.md)
      + [メディア視聴時間帯](media-reports/media-default-reports/media-reports-daypart.md)
      + [メディア同時ビューア](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [同時ビューア JSON レポートデータの取得](media-reports/media-default-reports/get-concurrent-json.md)
   + [メディアワークスペーステンプレート](media-reports/media-workspace-templates.md)
+ [Federated Analytics](federated-analytics.md)
+ その他のリソース {#additional-resources}
   + [ドキュメントのアップデート](additional-resources/doc-updates.md)
