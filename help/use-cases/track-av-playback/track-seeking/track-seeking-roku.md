---
title: Roku でシークをトラッキングする方法
description: Roku で Media SDK を使用してシーク開始イベントとシーク完了イベントをトラッキングする方法について説明します。
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
exl-id: cb0581f7-3ced-4d46-ac6a-a309a179c21e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LiR3Z-tC5yV2XcOwKTcIlcOsxx7UpBTMbn3LPXndxB4
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 133
ht-degree: 100%

---

# Roku でのシークの追跡{#track-seeking-on-roku}

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

詳しくは、追跡シナリオの[メインコンテンツでのシークのある VOD 再生](/help/use-cases/tracking-scenarios/vod-seeking.md)を参照してください。
