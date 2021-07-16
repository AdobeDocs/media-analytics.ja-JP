---
title: JavaScript 2.xを使用したコア再生の追跡方法を説明します。
description: JavaScript 2.xアプリを使用して、ブラウザーのメディアSDKを使用したコア追跡を実装する方法について説明します。
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
exl-id: d8af37a0-9048-4e6b-8cba-809386cbed5f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 94%

---

# JavaScript 2.x を使用したコア再生の追跡{#track-core-playback-on-javascript}

以下の手順は、2.x SDKをまたいだ実装のガイダンスです。

>[!IMPORTANT]
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

1. **トラッキングの初期設定**

   いつユーザーが再生の意図をトリガーする（ユーザーが再生をクリックする、または自動再生がオンになる）かを識別し、`MediaObject` インスタンスを作成します。

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | メディア名 | ○ |
   | `mediaid` | メディアの一意の ID | ○ |
   | `length` | メディアの長さ | ○ |
   | `streamType` | ストリームタイプ（後述の _StreamType 定数_ を参照） | ○ |
   | `mediaType` | メディアタイプ（後述の&#x200B;_MediaType 定数_ を参照） | ○ |

   **`StreamType`定数：**

   | 定数名 | 説明   |
   |---|---|
   | `VOD` | ビデオオンデマンドのストリームタイプ。 |
   | `LIVE` | LIVE コンテンツのストリームタイプ。 |
   | `LINEAR` | LINEAR コンテンツのストリームタイプ。 |
   | `AOD` | オーディオオンデマンドのストリームタイプ。 |
   | `AUDIOBOOK` | オーディオブックのストリームタイプ。 |
   | `PODCAST` | ポッドキャストのストリームタイプ。 |

   **`MediaType`定数：**

   | 定数名 | 説明 |
   |---|---|
   | `Audio` | オーディオストリームのメディアタイプ。 |
   | `Video` | ビデオストリームのメディアタイプ。 |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **メタデータのアタッチ**

   オプションで、コンテキストデータ変数を使用して標準またはカスタムメタデータオブジェクトをトラッキングセッションにアタッチします。

   * **標準メタデータ**

      [JavaScript での標準メタデータの実装](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >メディアオブジェクトへの標準メタデータオブジェクトのアタッチはオプションです。

      * メディアメタデータキー API リファレンス - [標準メタデータキー - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         利用可能なメタデータの包括的なセットについては、[オーディオおよびビデオパラメーター](/help/metrics-and-metadata/audio-video-parameters.md)を参照してください。
   * **カスタムメタデータ**

      カスタム変数の変数オブジェクトを作成し、このメディアのデータを設定します。例：

      ```js
      /* Set custom context data */
      var customVideoMetadata = {
          isUserLoggedIn: "false",
          tvStation: "Sample TV station",
          programmer: "Sample programmer"
      };
      ```


1. **意図を追跡して再生を開始**

   メディアセッションの追跡を開始するには、メディアハートビートインスタンスの `trackSessionStart` を呼び出します。

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >2 つ目の値は、手順 2 で作成した、カスタムのメディアメタデータオブジェクトの名前です。

   >[!IMPORTANT]
   >
   >`trackSessionStart` では、再生の開始ではなく、ユーザーの再生の意図を追跡します。この API は、データ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >カスタムメタデータを使用しない場合は、前述の iOS の例でコメントアウトされている行に示されているように、`trackSessionStart` の `data` 引数に空のオブジェクトを送信します。

1. **実際の再生開始を追跡**

   再生開始（メディアの最初のフレームが画面に表示）に関するイベントをメディアプレーヤーから識別し、`trackPlay` を呼び出します。

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **再生の完了を追跡**

   再生完了（ユーザーがコンテンツを最後まで視聴）に関するイベントをメディアプレーヤーから識別し、`trackComplete` を呼び出します。

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **セッションの終了を追跡**

   再生のアンロード／終了（ユーザーがメディアを閉じる、またはメディアが完了してアンロードされる）に関するイベントをメディアプレーヤーから識別し、`trackSessionEnd` を呼び出します。

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` は、トラッキングセッションの終わりをマークします。セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。`trackSessionEnd` の後は、他のすべての `track*` API 呼び出しは無視されます（新しいトラッキングセッション用の `trackSessionStart` を除く）。

1. **考えられるすべての一時停止シナリオを追跡**

   一時停止に関するイベントをメディアプレーヤーから識別し、`trackPause` を呼び出します。

   ```js
   mediaHeartbeat.trackPause();
   ```

   **一時停止のシナリオ**

   メディアプレーヤーが一時停止するあらゆるシナリオを識別して、`trackPause` が適切に呼び出されるようにします。以下のシナリオでは、アプリケーションで `trackPause()` を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリケーション*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリケーションのセッションを開いたままにしておきたい。
   * （*モバイルアプリケーション*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。例：ユーザーに電話がかかってきた場合や、別のアプリケーションのポップアップが表示された場合でも、アプリケーションのセッションを終了せず、ユーザーが中断した場所からメディアを再開できるようにしたい。

1. 一時停止からの再生および再開に関するイベントをプレーヤーから識別し、`trackPlay` を呼び出します。

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >これは、手順 4 で使用したのと同じイベントソースである可能性があります。再生が再開される際に、各 `trackPause()` API 呼び出しが後続の `trackPlay()` API 呼び出しと対になっていることを確認します。

* トラッキングのシナリオ：[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* JavaScript SDK に含まれている、追跡の完全な例を示すサンプルプレーヤー。
