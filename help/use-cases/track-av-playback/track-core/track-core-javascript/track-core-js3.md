---
title: JavaScript v3.x を使用してコア再生をトラッキングする方法
description: JavaScript 3.x アプリを使用するブラウザーで Media SDK を使用してコアトラッキングを実装する方法を説明します。
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/bIOfr94Q7wJLH9LfRg9VLIEJuS6JPvcgSWS62YCVguc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 759
ht-degree: 85%

---

# JavaScript 3.x を使用したコア再生の追跡{#track-core-playback-on-javascript}

このドキュメントでは、バージョン 3.x の SDK でのトラッキングについて説明しています。

>[!IMPORTANT]
>
>以前バージョンの SDK を実装する場合は、開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

1. **トラッキングの初期設定**

   いつユーザーが再生の意図をトリガーする（ユーザーが再生をクリックする、または自動再生がオンになる）かを識別し、`MediaObject` インスタンスを作成します。

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | 変数名 | タイプ | 説明 |
   | --- | --- | --- |
   | `name` | string | メディア名を示す、空白以外の文字列。 |
   | `id` | string | 一意のメディア識別子を示す、空白以外の文字列。 |
   | `length` | number | メディアの長さを秒単位で示す正の数。 長さが不明な場合は 0 を使用します。 |
   | `streamType` | string |   |
   | `mediaType` | | メディアのタイプ（オーディオまたはビデオ）。 |

   **`StreamType`定数：**

   | 定数名 | 説明   |
   |---|---|
   | `VOD` | ビデオオンデマンドのストリームタイプ。 |
   | `AOD` | オーディオオンデマンドのストリームタイプ。 |

   **`MediaType`定数：**

   | 定数名 | 説明 |
   |---|---|
   | `Audio` | オーディオストリームのメディアタイプ。 |
   | `Video` | ビデオストリームのメディアタイプ。 |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **メタデータのアタッチ**

   オプションで、コンテキストデータ変数を使用して標準またはカスタムメタデータをトラッキングセッションにアタッチします。

   * **標準メタデータ**

     >[!NOTE]
     >
     >標準メタデータのアタッチは任意です。

      * メディアメタデータキー API リファレンス - [標準メタデータキー - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

   * **カスタムメタデータ**

     カスタム変数の変数オブジェクトを作成し、このメディアのデータを設定します。 次に例を示します。

     ```js
     /* Set context data */
      var contextData = {};
     
      //Standard metadata
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
     
      //Custom metadata
      contextData["isUserLoggedIn"] = "false";
      contextData["tvStation"] = "Sample TV Station";
     ```

1. **意図を追跡して再生を開始**

   メディアセッションの追跡を開始するには、メディアハートビートインスタンスの `trackSessionStart` を呼び出します。

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` では、再生の開始ではなく、ユーザーの再生の意図を追跡します。 この API は、データ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >contextData を使用しない場合は、`data` の `trackSessionStart` 引数に空のオブジェクトを送信します。

1. **実際の再生開始を追跡**

   再生開始（メディアの最初のフレームが画面に表示）に関するイベントをメディアプレーヤーから識別し、`trackPlay` を呼び出します。

   ```js
   tracker.trackPlay();
   ```

1. **再生ヘッド値を更新**

   メディア再生ヘッドが変更された場合は、`mediaUpdatePlayhead` APIを呼び出してSDKに通知します。<br /> ビデオオンデマンド（VOD）の場合、値はメディア項目の先頭から秒単位で指定されます。<br /> ライブストリーミングの場合、プレーヤーがコンテンツ時間に関する情報を提供しない場合、その日の午前0時UTCからの秒数として値を指定できます。

   ```
   tracker.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >`tracker.updatePlayhead` APIを呼び出す際には、次の点を考慮してください。
   >* 進捗マーカーを使用する場合、コンテンツの継続時間が必要です。再生ヘッドは、メディア項目の先頭から0から始まる秒数で更新する必要があります。
   >* Media SDKを使用する場合は、少なくとも1秒に1回は`tracker.updatePlayhead` APIを呼び出す必要があります。

1. **再生の完了を追跡**

   再生完了（ユーザーがコンテンツを最後まで視聴）に関するイベントをメディアプレーヤーから識別し、`trackComplete` を呼び出します。

   ```js
   tracker.trackComplete();
   ```

1. **セッションの終了を追跡**

   再生のアンロード／終了（ユーザーがメディアを閉じる、またはメディアが完了してアンロードされる）に関するイベントをメディアプレーヤーから識別し、`trackSessionEnd` を呼び出します。

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` は、トラッキングセッションの終わりをマークします。 セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。 `trackSessionEnd` の後は、他のすべての `track*` API 呼び出しは無視されます（新しいトラッキングセッション用の `trackSessionStart` を除く）。

1. **考えられるすべての一時停止シナリオを追跡**

   一時停止に関するイベントをメディアプレーヤーから識別し、`trackPause` を呼び出します。

   ```js
   tracker.trackPause();
   ```

   **一時停止のシナリオ**

   メディアプレーヤーが一時停止するあらゆるシナリオを識別して、`trackPause` が適切に呼び出されるようにします。 以下のシナリオでは、アプリで `trackPause()` () を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリケーション*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリケーションのセッションを開いたままにしておきたい。
   * （*モバイルアプリケーション*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。 例：ユーザーに電話がかかってきた場合や、別のアプリケーションのポップアップが表示された場合でも、アプリケーションのセッションを終了せず、ユーザーが中断した場所からメディアを再開できるようにしたい。

1. 一時停止からの再生および再開に関するイベントをプレーヤーから識別し、`trackPlay` を呼び出します。

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >これは、手順 4 で使用したのと同じイベントソースである可能性があります。 再生が再開される際に、各 `trackPause()` API 呼び出しが後続の `trackPlay()` API 呼び出しと対になっていることを確認します。

* トラッキングのシナリオ：[広告のない VOD 再生](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* JavaScript SDK に含まれている、追跡の完全な例を示すサンプルプレーヤー。
