---
seo-title: 1.x から 2.x API への変換
title: 1.x から 2.x API への変換
uuid: 6e619288-c082-4cb4-8685-e90823dadf4a
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# API 1.xから2.xへの変換 {#one-x-to-two-x-conv}

## Media SDK 2.x APIリファレンス

* [Android API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [iOS API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [JS API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [Chromecast API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## 必要なTrack* API:

|  VHL 1.x | VHL 2.x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | 該当なし |
| `videoPlayerPlugin.trackSessionStart()` | [mediaHeartbeat.trackSessionStart(mediaObject, mediaCustomMetadata)](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [mediaHeartbeat.trackPlay()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [mediaHeartbeat.trackPause()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [mediaHeartbeat.trackComplete()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [mediaHeartbeat.trackSessionEnd()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | 該当なし |
| `videoPlayerPlugin.trackVideoPlayerError()` | [mediaHeartbeat.trackError()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

広告、チャプター、ビットレート変更、シーク、バッファーなどのオプションの追跡 API は、すべて `trackEvent` API に含まれています。[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent) API は、追跡対象のイベントのタイプを表す定数パラメーターを受け取ります。

## オプションの trackEvent API は次のとおりです。

| VHL 1.x | VHL 2.x |
|---|---|
| Return a valid `AdBreakInfo` in `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakStart)` |
| Return null in `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakComplete)` |
| `playerPlugin.trackAdStart()` | `trackEvent(Event.AdStart, adObject, adCustomMetadata)` |
| `playerPlugin.trackAdComplete()` | `trackEvent(Event.AdComplete)` |
| Return null in `VideoPlayerPlugin.getAdInfo()` | `trackEvent(Event.AdSkip)` |
| `playerPlugin.trackChapterStart()` | `trackEvent(Event.ChapterStart, chapterObject, chapterCustomMetadata)` |
| `playerPlugin.trackChapterComplete()` | `trackEvent(Event.ChapterComplete)` |
| Return null in `VideoPlayerPlugin.getChapterInfo()` | `trackEvent(Event.ChapterSkip)` |
| `playerPlugin.trackSeekStart()` | `trackEvent(Event.SeekStart)` |
| `playerPlugin.trackSeekComplete()` | `trackEvent(Event.SeekComplete)` |
| `playerPlugin.trackBufferStart()` | `trackEvent(Event.BufferStart)` |
| `playerPlugin.trackBufferComplete()` | `trackEvent(Event.BufferComplete)` |
| `playerPlugin.trackBitrateChange()` | `trackEvent(Event.BitrateChange)` |
| `playerPlugin.trackTimedMetadata()` | `trackEvent(Event.TimedMetadataUpdate)` |

