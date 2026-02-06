---
title: Chromecast でシークをトラッキングする方法
description: Chromecast で Media SDK を使用してシーク開始イベントとシーク完了イベントをトラッキングする方法を説明します。
uuid: 8018e6c4-fed9-4de7-9eae-c720da55ad8c
exl-id: 03be8ed3-ae3a-4e9a-b667-0d9280a844a1
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 100%

---

# Chromecast でのシークの追跡{#track-seeking-on-chromecast}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

## シーク追跡の定数

| 定数名 | 説明     |
|---|---|
| `SeekStart` | 追跡する Seek Start イベントの定数。 |
| `SeekComplete` | 追跡する Seek Complete イベントの定数。 |

## シークの実装

1. メディアプレーヤーの再生シークイベントをリッスンし、シーク開始イベント通知時に、`SeekStart` イベントを使用してシークを追跡します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekStart);
   ```

1. メディアプレーヤーからのシーク完了通知時に、`SeekComplete` イベントを使用してシークの終わりを追跡します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekComplete);
   ```

詳しくは、追跡シナリオの[メインコンテンツでのシークのある VOD 再生](/help/use-cases/tracking-scenarios/vod-seeking.md)を参照してください。
