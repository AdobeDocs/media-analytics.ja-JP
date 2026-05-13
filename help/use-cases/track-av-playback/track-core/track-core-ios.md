---
title: iOS でコア再生をトラッキングする方法
description: iOS で Media SDK を使用してコアトラッキングを実装する方法を説明します。
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/M-BlP6PGMAzyieFg3QDJTBcKE-Tw2PFCoNlB6G1E3KI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
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
source-wordcount: 707
ht-degree: 90%

---

# iOS でのコア再生の追跡{#track-core-playback-on-ios}

このドキュメントでは、バージョン 2.x の SDK でのトラッキングについて説明しています。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

1. **トラッキングの初期設定**

   いつユーザーが再生の意図をトリガーする（ユーザーが再生をクリックする、または自動再生がオンになる）かを識別し、`MediaObject` インスタンスを作成します。

   [createMediaObjectWithName API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | 変数名 | 説明 | 必須 |
   |---|---|---|
   | `name` | ビデオ名 | ○ |
   | `mediaid` | ビデオの一意のID | ○ |
   | `length` | ビデオの長さ | ○ |
   | `streamType` | ストリームタイプ（後述の _StreamType 定数_ を参照） | ○ |
   | `mediaType` | メディアタイプ（後述の&#x200B;_MediaType 定数_ を参照） | ○ |

   **`StreamType`定数：**

   | 定数名 | 説明 |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | ビデオオンデマンドのストリームタイプ |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Live コンテンツのストリームタイプ |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Linear コンテンツのストリームタイプ |
   | `ADBMediaHeartbeatStreamTypeAOD` | オーディオオンデマンドのストリームタイプ。 |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | オーディオブックのストリームタイプ。 |
   | `ADBMediaHeartbeatStreamTypePODCAST` | ポッドキャストのストリームタイプ。 |

   **`MediaType`定数：**

   | 定数名 | 説明 |
   |---|---|
   | `ADBMediaTypeAudio` | オーディオストリームのメディアタイプ。 |
   | `ADBMediaTypeVideo` | ビデオストリームのメディアタイプ。 |

   `MediaObject` を作成するための一般的な形式：

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                                          mediaId:<MEDIA_ID>
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE>
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **ビデオメタデータのアタッチ**

   オプションで、コンテキストデータ変数を使用して標準またはカスタムのビデオメタデータオブジェクトをビデオトラッキングセッションにアタッチします。

   * **標準のビデオメタデータ**

      * [iOS での標準メタデータの実装](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **ビデオメタデータキー**
        [iOS のメタデータキー](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

     >[!NOTE]
     >
     >メディアオブジェクトへの標準のビデオメタデータオブジェクトのアタッチはオプションです。

   * **カスタムメタデータ**

     カスタム変数の変数オブジェクトを作成し、このビデオのデータを設定します。 次に例を示します。

     ```
     NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
     [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
     [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
     ```

1. **意図を追跡して再生を開始**

   メディアセッションの追跡を開始するには、メディアハートビートインスタンスの `trackSessionStart` を呼び出します。

   >[!TIP]
   >
   >2 つ目の値は、手順 2 で作成した、カスタムのビデオメタデータオブジェクトの名前です。

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification {
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil];
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` では、再生の開始ではなく、ユーザーの再生の意図を追跡します。 この API は、ビデオのデータ／メタデータを読み込み、開始時間の QoS 指標（`trackSessionStart` と `trackPlay` の間の時間）を見積もるために使用します。

   >[!NOTE]
   >
   >カスタムのビデオメタデータを使用しない場合は、前述の iOS の例でコメントアウトされている行に示されているように、`trackSessionStart` の `data` 引数に空のオブジェクトを送信します。

1. **実際の再生開始を追跡**

   ビデオの再生開始（ビデオの最初のフレームが画面に表示）に関するイベントをビデオプレーヤーから識別し、`trackPlay` () を呼び出します。

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

1. **再生の完了を追跡**

   ビデオの再生完了（ユーザーがコンテンツを最後まで視聴）に関するイベントをビデオプレーヤーから識別し、`trackComplete` () を呼び出します。

   ```
   - (void)onVideoComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackComplete];
   }
   ```

1. **セッションの終了を追跡**

   ビデオ再生のアンロード／終了（ユーザーがビデオを閉じる、またはビデオの再生が完了してアンロードされる）に関するイベントをビデオプレーヤーから識別し、`trackSessionEnd` () を呼び出します。

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification {
       [_mediaHeartbeat trackSessionEnd];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` は、ビデオトラッキングセッションの終わりをマークします。 セッションが最後まで適切に視聴された場合（ユーザーがコンテンツを最後まで視聴）は、`trackComplete` の前に `trackSessionEnd` を呼び出すようにしてください。 `trackSessionEnd` の後は、他のすべての `track*` API 呼び出しは無視されます（新しいビデオトラッキングセッション用の `trackSessionStart` を除く）。

1. **考えられるすべての一時停止シナリオを追跡**

   ビデオの一時停止に関するイベントをビデオプレーヤーから識別し、`trackPause` を呼び出します。

   ```
   - (void)onVideoPause:(NSNotification *)notification {
       [_mediaHeartbeat trackPause];
   }
   ```

   **一時停止のシナリオ**

   ビデオプレーヤーが一時停止するあらゆるシナリオを識別して、`trackPause` が適切に呼び出されるようにします。 以下のシナリオでは、アプリで `trackPause()` () を呼び出す必要があります。

   * アプリ内でユーザーが明示的に一時停止をクリックする。
   * プレーヤー自体が一時停止状態になる。
   * （*モバイルアプリケーション*）- ユーザーがアプリケーションをバックグラウンドに移行した場合でも、アプリケーションのセッションを開いたままにしておきたい。
   * （*モバイルアプリケーション*）- 何らかのシステムの割り込みが生じ、アプリケーションがバックグラウンドに移行する。 例えば、ユーザーが電話を受け取ったり、別のアプリケーションからポップアップが発生したりしますが、セッションを維持して、中断した時点からビデオを再開する機会をユーザーに提供するアプリケーションが必要です。

1. 一時停止からのビデオ再生およびビデオ再開に関するイベントをプレーヤーから識別し、`trackPlay` を呼び出します。

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

   >[!TIP]
   >
   >これは、手順 4 で使用したのと同じイベントソースである可能性があります。 ビデオ再生が再開される際に、各 `trackPause()` API 呼び出しが後続の `trackPlay()` API 呼び出しと対になっていることを確認します。

コア再生のトラッキングについて詳しくは、次を参照してください。

* トラッキングのシナリオ：[広告のない VOD 再生](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* IOS SDKに含まれているサンプルプレイヤーを使用して、包括的なトラッキングの例を示します。
