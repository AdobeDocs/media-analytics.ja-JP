---
title: 'Roku でコア再生をトラッキングする方法 '
description: Roku で Media SDK を使用してコアトラッキングを実装する方法を説明します。
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 81%

---

# Roku でのコア再生の追跡 {#track-core-playback-on-roku}

このドキュメントでは、バージョン 2.x の SDK でのトラッキングについて説明しています。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

1. **トラッキングの初期設定**

   いつユーザーが再生の意図をトリガーする（ユーザーが再生をクリックする、または自動再生がオンになる）かを識別し、`MediaObject` インスタンスを作成します。

   **`MediaObject`リファレンス：**

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | ビデオ名 | ○ |
   | `mediaid` | ビデオの一意の識別子 | ○ |
   | `length` | ビデオの長さ | ○ |
   | `streamType` | ストリームタイプ（後述の _StreamType 定数_ を参照） | ○ |
   | `mediaType` | メディアタイプ（後述の&#x200B;_MediaType 定数_ を参照） | ○ |

   **`StreamType`定数：**

   | 定数名 | 説明   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | ビデオオンデマンドのストリームタイプ。 |
   | `MEDIA_STREAM_TYPE_LIVE` | LIVE コンテンツのストリームタイプ。 |
   | `MEDIA_STREAM_TYPE_LINEAR` | LINEAR コンテンツのストリームタイプ。 |
   | `MEDIA_STREAM_TYPE_AOD` | オーディオオンデマンドのストリームタイプ。 |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | オーディオブックのストリームタイプ。 |
   | `MEDIA_STREAM_TYPE_PODCAST` | ポッドキャストのストリームタイプ。 |

   **`MediaType`定数：**

   | 定数名 | 説明 |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | オーディオストリームのメディアタイプ。 |
   | `MEDIA_STREAM_TYPE_VIDEO` | ビデオストリームのメディアタイプ。 |

   **VOD コンテンツを含むビデオのメディア情報オブジェクトを作成します。**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

    または

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **AOD コンテンツを含むビデオのメディア情報オブジェクトを作成します。**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>",
    "<MEDIA_ID>",
    600,
    ADBMobile().MEDIA_STREAM_TYPE_AOD,
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

    または

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **メタデータのアタッチ**

   オプションで、コンテキストデータ変数を使用して標準またはカスタムメタデータオブジェクトをトラッキングセッションにアタッチします。

   * **標準メタデータ**

[Roku での標準メタデータの実装 &#x200B;](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

     >[!NOTE]
     >
     >メディアオブジェクトへの標準のビデオメタデータオブジェクトのアタッチはオプションです。

   * **カスタムメタデータ**

     カスタム変数の変数オブジェクトを作成し、このビデオのデータを設定します。次に例を示します。

     ```
     mediaContextData = {}
     mediaContextData["cmk1"] = "cmv1"
     mediaContextData["cmk2"] = "cmv2"
     ```

1. **意図を追跡して再生を開始**

   メディアセッションの追跡を開始するには、メディアハートビートインスタンスの `trackSessionStart` を呼び出します。

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >
   >2 つ目の値は、手順 2 で作成した、カスタムのビデオメタデータオブジェクトの名前です。

   >[!IMPORTANT]
   >
   >`trackSessionStart` では、再生の開始ではなく、ユーザーの再生の意図を追跡します。この API は、ビデオのデータ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >カスタムのビデオメタデータを使用しない場合は、前述の iOS の例でコメントアウトされている行に示されているように、`trackSessionStart` の `data` 引数に空のオブジェクトを送信します。

1. **実際の再生開始を追跡**

   ビデオの再生開始（ビデオの最初のフレームが画面に表示）に関するイベントをビデオプレーヤーから識別し、`trackPlay` () を呼び出します。

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **再生ヘッド値の更新**

   メディアの再生ヘッドが変更された場合は、`mediaUpdatePlayhead` API を呼び出してSDKに通知します。 <br /> ビデオオンデマンド（VOD）の場合、値はメディア項目の開始時からの秒数で指定されます。<br /> ライブストリーミングでは、プレーヤーがコンテンツのデュレーションに関する情報を提供しない場合、その日の午前 0 時（UTC）からの秒数を指定できます。

   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

   >[!NOTE]
   >
   >`mediaUpdatePlayhead` API を呼び出す際は、次の点を考慮してください。
   >* プログレスマーカーを使用する場合、コンテンツのデュレーションが必要です。また、再生ヘッドはメディアアイテムの開始時からの（0 から始まる）秒数で更新する必要があります。
   >* Media SDK を使用する場合は、`mediaUpdatePlayhead` API を 1 秒に 1 回以上呼び出す必要があります。


1. **再生の完了を追跡**

   ビデオの再生完了（ユーザーがコンテンツを最後まで視聴）に関するイベントをビデオプレーヤーから識別し、`trackComplete` () を呼び出します。

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **セッションの終了を追跡**

   ビデオ再生のアンロード／終了（ユーザーがビデオを閉じる、またはビデオの再生が完了してアンロードされる）に関するイベントをビデオプレーヤーから識別し、`trackSessionEnd` () を呼び出します。

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` は、ビデオトラッキングセッションの終わりをマークします。セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。`trackSessionEnd` の後は、他のすべての `track*` API 呼び出しは無視されます（新しいビデオトラッキングセッション用の `trackSessionStart` を除く）。

1. **考えられるすべての一時停止シナリオを追跡**

   ビデオの一時停止に関するイベントをビデオプレーヤーから識別し、`trackPause` を呼び出します。

   ```
   ADBMobile().mediaTrackPause()
   ```

   **一時停止のシナリオ**

   ビデオプレーヤーが一時停止するあらゆるシナリオを識別して、`trackPause` が適切に呼び出されるようにします。以下のシナリオでは、アプリで `trackPause()` () を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリケーション*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリケーションのセッションを開いたままにしておきたい。
   * （*モバイルアプリケーション*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。例えば、ユーザーが呼び出しを受け取った場合や、別のアプリケーションからポップアップが発生した場合に、中断した時点からビデオを再開する機会をユーザーに与えるために、アプリケーションでセッションを維持する必要があります。

1. 一時停止からのビデオ再生およびビデオ再開に関するイベントをプレーヤーから識別し、`trackPlay` を呼び出します。

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >これは、手順 4 で使用したのと同じイベントソースである可能性があります。ビデオ再生が再開される際に、各 `trackPause()` API 呼び出しが後続の `trackPlay()` API 呼び出しと対になっていることを確認します。

* トラッキングのシナリオ：[広告のない VOD 再生](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Roku SDKに付属しているサンプルプレーヤーで、トラッキングの完全な例を確認できます。
