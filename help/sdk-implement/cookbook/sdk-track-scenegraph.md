---
title: SceneGraph（Roku）でのトラッキング
description: Roku SceneGraph XML プログラミングフレームワークを使用してメディアを追跡します。
uuid: fa85e546-c79b-4df4-8c03-d6593fa296d5
exl-id: e428d3cd-dbc7-48bb-82ff-61b6b892884c
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '1171'
ht-degree: 100%

---

# SceneGraph（Roku）でのトラッキング {#tracking-in-scenegraph-roku}

## はじめに {#introduction}

Roku では、アプリケーションを開発するための新たなプログラミングフレームワークである SceneGraph XML プログラミングフレームワークを導入しました。この新しいフレームワークの特徴は、次の 2 つの新しい重要な概念です。

* アプリケーション画面の SceneGraph レンダリング
* SceneGraph 画面の XML 設定

Adobe Mobile SDK for Roku は BrightScript で記述されています。SDK では、SceneGraph 上で実行されるアプリでは利用できない様々なコンポーネントを使用します（スレッドなど）。したがって、SceneGraph フレームワークの使用を考えている Roku アプリケーション開発者は Adobe Mobile SDK API を呼び出すことができません（後者はレガシー BrightScript アプリで利用可能なものに類似しています）。

## アーキテクチャ {#architecture}

SceneGraph サポートを AdobeMobile SDK に追加するために、アドビは AdobeMobile SDK と `adbmobileTask` の接続ブリッジを作成する新たな API を追加しました。後者は、SDK の API 実行に使用される SceneGraph ノードです（`adbmobileTask` の使用方法については、このドキュメントの後半で詳しく説明します）。

コネクタブリッジは以下のように設計されています。

* ブリッジは、AdobeMobile SDK の SceneGraph 互換インスタンスを返します。SceneGraph 互換 SDK は、レガシー SDK で提供されているすべての API を備えています。
* SceneGraph での AdobeMobile SDK API の使用方法は、レガシー API の使用方法とほぼ同じです。
* ブリッジには、データを返す API のコールバックをリッスンするメカニズムも用意されています。

![](assets/SceneGraph_arch.png)

## コンポーネント {#components}

**SceneGraph アプリケーション：**

* SceneGraph 接続ブリッジ API を介して `AdobeMobileLibrary` API を利用します。
* 予期される出力データ変数に関して、`adbmobileTask` で応答コールバックを登録します。

**AdobeMobileLibrary：**

* コネクタブリッジ API を含む一連の公開 API（レガシー）を提供します。
* 従来の公開 API をすべて含む SceneGraph 接続インスタンスを返します。
* API 実行時には、`adbmobileTask` の SceneGraph ノードと通信します。

**adbmobileTask Node：**

* `AdobeMobileLibrary` API をバックグラウンドスレッドで実行する SceneGraph タスクノードです。
* データをアプリケーションシーンに戻すデリゲートとして機能します。

## 公開 SceneGraph API {#public-scenegraph-apis}

### ADBMobileConnector

| カテゴリ | メソッド名 | 説明 |
|---|---|---|
| **定数** |  |  |
|  | `sceneGraphConstants` | `SceneGraphConstants` を含むオブジェクトを返します。詳しくは、前出の表を参照してください。 |
|  |  |  |
| **デバッグのログ** |  |  |
|  | `setDebugLogging` | ADBMobile SDK でデバッグのログを設定する SceneGraph API です。 |
|  | `getDebugLogging` | ADBMobile SDK からデバッグのログを取得する SceneGraph API です。 |
|  | 詳しくは、レガシー SDK の、デバッグのログに関する節を参照してください。 |  |
|  |  |  |
| **プライバシーステータス／オプトアウト** |  |  |
|  | `setPrivacyStatus` | ADBMobile SDK でプライバシーステータスを設定する SceneGraph API です。 |
|  | `getPrivacyStatus` | ADBMobile SDK からプライバシーステータスを取得する SceneGraph API です。 |
|  | 詳しくは、レガシー SDK の、オプトアウト／プライバシーステータスに関する節を参照してください。 |  |
|  |  |  |
| **Analytics** |  |  |
|  | `trackState` | ADBMobile SDK のステータスを追跡する SceneGraph API です。 |
|  | `trackAction` | ADBMobile SDK のアクションを追跡する SceneGraph API です。 |
|  | `trackingIdentifier` | ADBMobile SDK から追跡 ID を取得する SceneGraph API です。 |
|  | `userIdentifier` | ADBMobile SDK からユーザー ID を取得する SceneGraph API です。 |
|  | `setUserIdentifier` | ADBMobile SDK でユーザー ID を設定する SceneGraph API です。 |
|  | `getAllIdentifiers` | Roku SDK が認識している永続的なユーザー ID をすべて取得する SceneGraph API です。 |
|  | 詳しくは、レガシー SDK の Analytics に関する節を参照してください。 |  |
|  |  |  |
| **Experience Cloud** |  |  |
|  | `visitorSyncIdentifiers` | ADBMobile SDK で Experience Cloud ID を同期する SceneGraph API です。 |
|  | `visitorMarketingCloudID` | ADBMobile SDK から訪問者 Experience Cloud ID を取得する SceneGraph API です。 |
|  | 詳しくは、レガシー SDK の、Experience Cloud に関する節を参照してください。 |  |
|  |  |  |
| **Audience Manager** |  |  |
|  | `audienceSubmitSignal` | 特性を持つオーディエンス管理シグナルを送信する SceneGraph API です。 |
|  | `audienceVisitorProfile` | ADBMobile SDK から Audience Manager の訪問者プロファイルを取得する SceneGraph API です。 |
|  | `audienceDpid` | ADBMobile SDK からオーディエンス DPID を取得する SceneGraph API です。 |
|  | `audienceDpuuid` | ADBMobile SDK からオーディエンス DPUUID を取得する SceneGraph API です。 |
|  | `audienceSetDpidAndDpuuid` | ADBMobile SDK でオーディエンス DPID およびオーディエンス DPUUID を設定する SceneGraph API です。 |
|  | 詳しくは、レガシー SDK の、Audience Manager に関する節を参照してください。 |  |
|  |  |  |
| **MediaHeartbeat** |  |  |
|  | `mediaTrackLoad` | MediaHeartbeat 追跡用にビデオコンテンツを読み込む SceneGraph API です。 |
|  | mediaTrackStart | MediaHeartbeat を使用してビデオトラッキングセッションを開始する SceneGraph API です。 |
|  | `mediaTrackUnload` | MediaHeartbeat 追跡からビデオコンテンツをアンロードする SceneGraph API です。 |
|  | `mediaTrackPlay` | ビデオコンテンツの再生を追跡する SceneGraph API です。 |
|  | mediaTrackPause | 一時停止されたビデオコンテンツを追跡する SceneGraph API です。 |
|  | `mediaTrackComplete` | ビデオコンテンツの再生完了を追跡する SceneGraph API です。 |
|  | `mediaTrackError` | 再生エラーを追跡する SceneGraph API です。 |
|  | mediaTrackEvent | 追跡中の再生イベントを追跡する SceneGraph API です。例：広告、チャプター。 |
|  | `mediaUpdatePlayhead` | ビデオのトラッキング中に MediaHeartbeat に再生ヘッドの更新を送信する SceneGraph API です。 |
|  | `mediaUpdateQoS` | ビデオのトラッキング中に MediaHeartbeat に QoS の更新を送信する SceneGraph API です。 |
|  | 詳しくは、レガシー SDK の、MediaHeartbeat に関する節を参照してください。 |  |

### SceneGraphConstants

| 定数名 | 説明 |
|---|---|
| `API_RESPONSE` | `adbmobileTask` ノードの `adbmobileApiResponse` フィールドからの応答オブジェクトを取得するために使用されます |
| `DEBUG_LOGGING` | `getDebugLogging` の `apiName` として使用されます |
| `PRIVACY_STATUS` | `getPrivacyStatus` の `apiName` として使用されます |
| `TRACKING_IDENTIFIER` | `trackingIdentifier` の `apiName` として使用されます |
| `USER_IDENTIFIER` | `userIdentifier` の `apiName` として使用されます |
| `VISITOR_MARKETING_CLOUD_ID` | `visitorMarketingCloudID` の `apiName` として使用されます |
| `AUDIENCE_VISITOR_PROFILE` | `audienceVisitorProfile` の `apiName` として使用されます |
| `AUDIENCE_DPID` | `audienceDpid` の `apiName` として使用されます |
| `AUDIENCE_DPUUID` | `audienceDpuuid` の `apiName` として使用されます |

### adbmobileTask ノード

<table>
<thead>
<tr>
<td> フィールド </td><td> タイプ </td><td> デフォルト </td><td> 用途 </td>
</tr>
</thead>
<tbody>
<tr>
<td> adbmobileApiCall </td>
<td> assocarray </td>
<td> 無効 </td>
<td> このフィールドを変更したり、アプリケーションで使用したりしないでください。ADBMobile SceneGraphConnector はこのフィールドを使用して、SceneGraph ノードを経由した API 呼び出しを転送したり応答を取得したりします。したがって、このキーおよびフィールドは SceneGraph との互換性を確保するために AdobeMobileSDK で予約されています。<b>重要：</b>このフィールドに変更を加えると、AdobeMobileSDK が正しく機能しなくなるおそれがあります。</td>
</tr>
<tr>
<td> adbmobileApiResponse </td>
<td> assocarray </td>
<td> 無効 </td>
<td> 読み取り専用。AdobeMobileSDK で実行されるすべての API はこのフィールドに応答を返します。応答オブジェクトを受信するには、このフィールドの更新をリッスンするコールバックを登録します。応答オブジェクトの形式を次に示します。  
<pre>
response = {
  "apiName" : &lt;SceneGraphConstants.
               API_NAME&gt; 
  "returnValue : &lt;API_RESPONSE&gt; 
}</pre>
この応答オブジェクトのインスタンスは API リファレンスガイドに記載されているように値を返す AdobeMobileSDK の API 呼び出し用に送信されます。例えば、visitorMarketingCloudID() の API 呼び出しは以下の応答オブジェクトを返します。 
<pre>
response = {
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : "07050x25671x33760x72644x14"  
} 
</pre>
また、応答データは無効になる場合もあります。 
<pre>
response = {  
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : invalid 
} 
</pre>
</td>
</tr>
</tbody>
</table>

### `adbmobile.brs`

#### `getADBMobileConnectorInstance`

API 署名: `ADBMobile().getADBMobileConnectorInstance()`\
入力：`adbmobileTask`
戻り値の型：`ADBMobileConnector`

#### `sgConstants`

API 署名：`ADBMobile().sgConstants()`
入力：なし\
戻り値の型：`SceneGraphConstants`

>[!NOTE]
>詳しくは、`ADBMobileConnector` API リファレンスを参照してください。

### ADBMobile 定数

|  機能  | 定数名 | 説明   |
|---|---|---|
| バージョン管理 | `version` | AdobeMobileLibrary バージョン情報を取得する定数 |
| プライバシー／オプトアウト | `PRIVACY_STATUS_OPT_IN` | オプトインのプライバシーステータスを示す定数 |
|  | `PRIVACY_STATUS_OPT_OUT` | オプトアウトのプライバシーステータスを示す定数 |
| MediaHeartbeat 定数 | <br/><br/>[メディアハートビートメソッド](/help/sdk-implement/track-av-playback/track-core/track-core-roku.md)ページの定数を参照してください。 | メディアハートビート API でこれらの定数を使用します。 |
| 標準メタデータ | <br/><br/>[標準メタデータパラメーター](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)ページの定数を参照してください。 | 標準ビデオ／広告メタデータを MediaHeartbeat API にアタッチするにはこれらの定数を使用します。 |

レガシー AdobeMobileLibrary のグローバルに定義されたユーティリティ `MediaHeartbeat` API は、SceneGraph ノードでは使用できない Brightscript のコンポーネントが使用されていないので、SceneGraph 環境でそのままアクセスできます&#x200B;*。*&#x200B;これらのメソッドについて詳しくは、以下の表を参照してください。

### MediaHeartbeat のグローバルメソッド

| メソッド | 説明 |
| --- | --- |
| `adb_media_init_mediainfo` | このメソッドは初期化されたメディア情報オブジェクトを返します。`Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object` |
| `adb_media_init_adinfo` | このメソッドは初期化された広告情報オブジェクトを返します。`Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object` |
| `adb_media_init_chapterinfo` | このメソッドは初期化されたチャプター情報オブジェクトを返します。`Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object` |
| `adb_media_init_adbreakinfo` | このメソッドは初期化された AdBreak 情報オブジェクトを返します。`Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object` |
| `adb_media_init_qosinfo` | このメソッドは初期化された QoS オブジェクトを返します。`Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object` |

## 実装 {#implementation}

1. **Roku ライブラリのダウンロード -** [最新の Roku ライブラリ](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.2)をダウンロードします。

1. **開発環境の設定**

   1. `adbmobile.brs`（AdobeMobileLibrary）を `pkg:/source/` ディレクトリにコピーします。

   1. Scene Graph をサポートするために、`adbmobileTask.brs` および `adbMobileTask.xml` を `pkg:/components/` ディレクトリにコピーします。

1. **初期設定**

   1. `adbmobile.brs` を Scene に読み込みます。

      ```
      <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
      ```

   1. `adbmobileTask` ノードのインスタンスを Scene に作成します。

      ```
      m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
      ```

   1. `adbmobile` インスタンスを使用して、SceneGraph 用 `adbmobileTask` コネクタを取得します。

      ```
      m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
      ```

   1. `adbmobile` SG 定数を取得します。

      ```
      m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
      ```

   1. すべての `AdbMobile` API 呼び出しの応答オブジェクトを受け取るためのコールバックを登録します。

      ```
      m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE,  
                                   "onAdbmobileApiResponse") 
      
      ' Sample implementation of the callback 
      ' Listen for all the constants for which API calls are made on the SDK 
      function onAdbmobileApiResponse() as void 
          responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE] 
      
          if responseObject <> invalid 
              methodName = responseObject.apiName 
              retVal = responseObject.returnValue 
      
              if methodName = m.adbmobileConstants.DEBUG_LOGGING 
                  if retVal 
                      print "API Response: DEBUG LOGGING: " + "True" 
                  else 
                      print "API Response: DEBUG LOGGING: " + "False" 
                  endif 
              else if methodName = m.adbmobileConstants.PRIVACY_STATUS 
                  print "API Response: PRIVACY STATUS: " + retVal 
              else if methodName = m.adbmobileConstants.TRACKING_IDENTIFIER 
                  if retVal <> invalid 
                      print "API Response: TRACKING IDENTIFIER: " + retVal 
                  else 
                      print "API Response: TRACKING IDENTIFIER: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.USER_IDENTIFIER 
                  if retVal <> invalid 
                      print "API Response: USER IDENTIFIER: " + retVal 
                  else 
                      print "API Response: USER IDENTIFIER: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.VISITOR_MARKETING_CLOUD_ID 
                  if retVal <> invalid 
                      print "API Response: MCID: " + retVal 
                  else 
                      print "API Response: MCID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_DPID 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE DPID: " + retVal 
                  else 
                      print "API Response: AUDIENCE DPID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_DPUUID 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE DPUUID: " + retVal 
                  else 
                      print "API Response: AUDIENCE DPUUID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_VISITOR_PROFILE 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE VISITOR PROFILE: Valid Object" 
                  else 
                      print "API Response: AUDIENCE VISITOR PROFILE: " + "invalid" 
                  endif 
              endif 
          endif 
      end function 
      ```

## 実装例 {#sample-implementation}

### レガシー SDK の API 呼び出しの例

```
'get an instance of SDK 
m.adbmobile = ADBMobile() 
   
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
   
'execute getter APIs 
debugLogging = m.adbmobile.getDebugLogging()
```

### SG SDK の API 呼び出しの例

```
'create adbmobileTask instance 
m.adbmobileTask = createObject("roSGNode", "adbmobileTask") 
   
'get an instance of SDK using task instance 
m.adbmobile =  
  ADBMobile().getADBMobileConnectorInstace(m.adbmobileTask) 
m.adbmobileConstants = m.adbmobile.sceneGraphConstants() 
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
  
'execute getter APIs 
m.adbmobileTask.ObserverField(m.adbConstants.API_RESPONSE,  
                              "onAdbmobileApiResponse") 
m.adbmobile.getDebugLogging() 
   
'listen for return data in registered callbacks 
function onAdbmobileApiResponse() as void 
    responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE] 
  
        if responseObject <> invalid 
            methodName = responseObject.apiName 
            retVal = responseObject.returnValue 
  
        if methodName = m.adbmobileConstants.DEBUG_LOGGING 
            if retVal 
                print "API Response: DEBUG LOGGING: " + "True" 
            else 
                print "API Response: DEBUG LOGGING: " + "False" 
         endif 
    endif 
end function
```
