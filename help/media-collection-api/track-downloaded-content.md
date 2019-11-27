---
title: ダウンロードされたコンテンツの追跡
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# ダウンロードされたコンテンツの追跡 {#track-downloaded-content}

## 概要 {#overview}

Downloaded Content 機能では、ユーザーがオフライン時のメディア視聴を追跡できます。例えば、ユーザーがモバイルデバイスでアプリをダウンロードし、インストールします。その後、アプリを使用してコンテンツをデバイスのローカルストレージにダウンロードします。このダウンロードされたデータを追跡するために、アドビは Downloaded Content 機能を開発しました。この機能を使用すると、デバイスの接続状態に関係なく、ユーザーがデバイスのストレージからコンテンツを再生した場合に、トラッキングデータがデバイスに保存されます。ユーザーが再生セッションを終了し、デバイスがオンラインに戻ると、保存されたトラッキング情報が単一のペイロード内でメディアコレクション API バックエンドに送信されます。そこから、メディアコレクション API で通常おこなうように処理とレポート作成が実行されます。

2 つのアプローチの対比：

* オンライン

   このリアルタイムアプローチでは、メディアプレーヤーが各プレーヤーイベントの発生時にトラッキングデータを送信し、10 秒ごと（広告の場合は 1 秒ごと）にネットワーク ping を 1 つずつバックエンドに送信します。

* オフライン（Downloaded Content 機能）

   このバッチ処理アプローチでは、同じセッションイベントを生成する必要がありますが、単一セッションとしてバックエンドに送信されるまで、デバイスに保存されます（後述の例を参照）。

どちらのアプローチにもそれぞれ長所と短所があります。
* オンラインシナリオは、リアルタイムに追跡します。各ネットワーク呼び出しの前に接続性チェックが必要です。
* オフラインシナリオ（Downloaded Content 機能）は、1 つのネットワーク接続性チェックのみ必要ですが、デバイスに、より大きなメモリフットプリントが必要です。

## 実装 {#implementation}

### イベントスキーマ

Downloaded Content 機能は、（標準）オンラインメディアコレクション API の単なるオフラインバージョンなので、プレーヤーがバックエンドにバッチおよび送信するイベントデータは、オンライン呼び出しをおこなう際に使用するのと同じイベントスキーマを使用する必要があります。これらのスキーマについて詳しくは、次を参照してください。
* [概要;](/help/media-collection-api/mc-api-overview.md)
* [イベントリクエストの検証](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### イベントの順序

* バッチペイロードの最初のイベントは、メディアコレクション API で通常おこなうように、`sessionStart` である必要があります。
* **ダウンロードされたコンテンツを送信していることをバックエンドに示すために、`sessionStart`イベントの標準メタデータパラメーター（`params`キー）に`media.downloaded: true`** を含める必要があります。ダウンロードされたデータを送信する際に、このパラメーターが存在しないか、false に設定されている場合、API は応答コード 400（無効な要求）を返します。このパラメーターは、バックエンドに対して、ダウンロードされたコンテンツとライブコンテンツを区別します（ライブセッションに `media.downloaded: true` が設定されている場合、同様に API からの応答が 400 になります）。
* プレーヤーイベントを発生順に正しく保存するのは実装側の責任です。

### 応答コード

* 201 - Created: Successful Request。データが有効であり、セッションが作成されたので、処理されます。
* 400 - Bad Request。スキーマの検証に失敗し、すべてのデータが破棄されたので、セッションデータは処理されません。

## Adobe Analtyics との統合 {#integration-with-adobe-analtyics}

ダウンロードされたコンテンツシナリオ用に Analytics 開始／終了呼び出しを計算する際に、バックエンドは、`ts.` と呼ばれる追加の Analytics フィールドを設定します。これらは、受け取った最初および最後のイベント（開始および終了）のタイムスタンプです。このメカニズムにより、完了したメディアセッションを正しい時点に配置できます（つまり、ユーザーが数日間オンラインに戻らなくても、コンテンツが実際に視聴された時点でメディアセッションが発生したと報告されます）。_タイムスタンプオプションのレポートスイートを作成して、Adobe Analytics 側でこのメカニズムを有効にする必要があります。_ タイムスタンプオプションのレポートスイートを有効にするには、[タイムスタンプオプション](https://docs.adobe.com/content/help/ja-JP/analytics/admin/admin-tools/timestamp-optional.html)を参照してください。

## サンプルセッションの比較 {#sample-session-comparison}

```
[url]/api/v1/sessions
```

### オンラインコンテンツ

```
{ 
  eventType: "sessionStart", 
  playerTime: { 
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ } 
}
```

### ダウンロードされたコンテンツ

```
[{ 
    eventType: "sessionStart", 
    playerTime:{
      playhead: 0, 
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
    }, 
    customMetadata:{},  
    qoeData:{} 
}, 
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559} 
}]
```

