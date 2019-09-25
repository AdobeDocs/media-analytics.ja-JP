---
seo-title: Roku でのシークの追跡
title: Roku でのシークの追跡
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Roku でのシークの追跡{#track-seeking-on-roku}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## シークトラッキング定数

| 定数名 | 説明     |
|---|---|
| `SeekStart` | 追跡する Seek Start イベントの定数。 |
| `SeekComplete` | 追跡する Seek Complete イベントの定数。 |

## シークの実装

1. メディアプレーヤーの再生シークイベントをリッスンし、シーク開始イベント通知時に、`SeekStart` イベントを使用してシークを追跡します。

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. メディアプレーヤーからのシーク完了通知時に、`SeekComplete` イベントを使用してシークの終わりを追跡します。

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

詳しくは、追跡シナリオの[メインコンテンツでのシークのある VOD 再生](/help/sdk-implement/tracking-scenarios/vod-seeking.md)を参照してください。
