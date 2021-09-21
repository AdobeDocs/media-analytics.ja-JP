---
title: Roku でコア再生をトラッキングする方法
description: Roku で Media SDK を使用してコアトラッキングを実装する方法を説明します。
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d7cb36c2dd6b35da4531ca975c7fc730e387b750
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 93%

---

# Roku でのコア再生の追跡{#track-core-playback-on-roku}

このドキュメントでは、バージョン 2.x の SDK でのトラッキングについて説明しています。

>[!IMPORTANT]
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

1. **トラッキングの初期設定**

   いつユーザーが再生の意図をトリガーする（ユーザーが再生をクリックする、または自動再生がオンになる）かを識別し、`MediaObject` インスタンスを作成します。

   **`MediaObject`リファレンス：**

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | ビデオ名 | ○ |
   | `mediaid` | ビデオの一意の ID | ○ |
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

   [Roku での標準メタデータの実装 ](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
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
   >2 つ目の値は、手順 2 で作成した、カスタムのビデオメタデータオブジェクトの名前です。

   >[!IMPORTANT]
   >`trackSessionStart` では、再生の開始ではなく、ユーザーの再生の意図を追跡します。この API は、ビデオのデータ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >カスタムのビデオメタデータを使用しない場合は、前述の iOS の例でコメントアウトされている行に示されているように、`trackSessionStart` の `data` 引数に空のオブジェクトを送信します。

1. **実際の再生開始を追跡**

   ビデオの再生開始（ビデオの最初のフレームが画面に表示）に関するイベントをビデオプレーヤーから識別し、`trackPlay` () を呼び出します。

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **再生ヘッド値の更新**

   メディアの再生ヘッドが変更されると、 `mediaUpdatePlayhead` APIを呼び出してSDKに通知します。 ビデオオンデマンド(VOD)の場合、値はメディアアイテムの開始時からの時間（秒）を返します。 ライブストリーミングの場合、この値はその日の午前0時(UTC)からの秒数として指定されます。

   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

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
   * （*モバイルアプリケーション*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。例：ユーザーに電話がかかってきた場合や、別のアプリケーションのポップアップが表示された場合でも、アプリケーションのセッションを終了せず、ユーザーが中断した場所からビデオを再開できるようにしたい。

1. 一時停止からのビデオ再生およびビデオ再開に関するイベントをプレーヤーから識別し、`trackPlay` を呼び出します。

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >これは、手順 4 で使用したのと同じイベントソースである可能性があります。ビデオ再生が再開される際に、各 `trackPause()` API 呼び出しが後続の `trackPlay()` API 呼び出しと対になっていることを確認します。

* トラッキングのシナリオ：[広告のない VOD 再生](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Roku SDK に含まれている、追跡の完全な例を示すサンプルプレーヤー
