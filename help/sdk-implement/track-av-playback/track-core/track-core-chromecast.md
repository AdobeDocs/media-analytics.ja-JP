---
title: Chromecastでのコア再生の追跡方法を説明します。
description: ChromecastでのメディアSDKを使用したコア追跡の実装方法を説明します。
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
exl-id: 9812d06d-9efd-460c-a626-6a15f61a4c35
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 96%

---

# Chromecast でのコア再生の追跡{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>このドキュメントでは、バージョン 2.x の SDK でのトラッキングについて説明しています。1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

1. **トラッキングの初期設定**

   いつユーザーが再生の意図をトリガーする（ユーザーが再生をクリックする、または自動再生がオンになる）かを識別し、`MediaObject` インスタンスを作成します。

   **`MediaObject`API リファレンス:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`定数：**

   [ADBMobile メディア](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`定数：**

   [ADBMobile メディア](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **ビデオメタデータのアタッチ**

   オプションで、コンテキストデータ変数を使用して標準またはカスタムのビデオメタデータオブジェクトをビデオトラッキングセッションにアタッチします。

   * **標準のビデオメタデータ**

      [Chromecast での標準メタデータの実装](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >メディアオブジェクトへの標準のビデオメタデータオブジェクトのアタッチはオプションです。

   * **カスタムメタデータ**

      カスタム変数の変数オブジェクトを作成し、このビデオのデータを設定します。例：

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **意図を追跡して再生を開始**

   メディアセッションの追跡を開始するには、`media` オブジェクトの [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) を呼び出します。

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` では、再生の開始ではなく、ユーザーの再生の意図を追跡します。この API は、ビデオのデータ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >2 つ目の値は、手順 2 で作成した、カスタムのビデオメタデータオブジェクトの名前です。カスタムのビデオメタデータを使用しない場合は、前述の iOS の例でコメントアウトされている行に示されているように、`trackSessionStart` の `data` 引数に空のオブジェクトを送信します。

1. **実際の再生開始を追跡**

   ビデオの再生開始（ビデオの最初のフレームが画面に表示）に関するイベントをビデオプレーヤーから識別し、[trackPlay](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay) を呼び出します。

   ```
   ADBMobile.media.trackPlay();
   ```

1. **再生の完了を追跡**

   ビデオの再生完了（ユーザーがコンテンツを最後まで視聴）に関するイベントをビデオプレーヤーから識別し、[trackComplete](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete) を呼び出します。

   ```
   ADBMobile.media.trackComplete();
   ```

1. **セッションの終了を追跡**

   ビデオ再生のアンロード／終了（ユーザーがビデオを閉じる、またはビデオの再生が完了してアンロードされる）に関するイベントをビデオプレーヤーから識別し、[trackSessionEnd](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd) を呼び出します。

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` は、ビデオトラッキングセッションの終わりをマークします。セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。`trackSessionEnd` の後は、他のすべての `track*` API 呼び出しは無視されます（新しいビデオトラッキングセッション用の `trackSessionStart` を除く）。

1. **考えられるすべての一時停止シナリオを追跡**

   ビデオの一時停止に関するイベントをビデオプレーヤーから識別し、[trackPause](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause) を呼び出します。

   ```
   ADBMobile.media.trackPause();
   ```

   **一時停止のシナリオ**

   ビデオプレーヤーが一時停止するあらゆるシナリオを識別して、`trackPause` が適切に呼び出されるようにします。以下のシナリオでは、アプリで `trackPause()` () を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリケーション*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリケーションのセッションを開いたままにしておきたい。
   * （*モバイルアプリケーション*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。例：ユーザーに電話がかかってきた場合や、別のアプリケーションのポップアップが表示された場合でも、アプリケーションのセッションを終了せず、ユーザーが中断した場所からビデオを再開できるようにしたい。

1. 一時停止からのビデオ再生およびビデオ再開に関するイベントをプレーヤーから識別し、[trackPlay](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete) を呼び出します。

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >これは、手順 4 で使用したのと同じイベントソースである可能性があります。ビデオ再生が再開される際に、各 `trackPause()` API 呼び出しが後続の `trackPlay()` API 呼び出しと対になっていることを確認します。

* トラッキングのシナリオ：[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Chromecast SDK に含まれている、追跡の完全な例を示すサンプルプレーヤー
