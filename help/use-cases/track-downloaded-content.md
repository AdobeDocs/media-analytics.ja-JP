---
title: オフラインでダウンロードしたコンテンツをストリーミングメディアコレクションでトラッキングする方法
description: ユーザーがオフラインの場合にダウンロード済みコンテンツ機能を使用してメディア視聴をトラッキングする方法について説明します。
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 98%

---

# ダウンロードされたコンテンツの追跡 {#track-downloaded-content}

## 概要  {#overview}

Downloaded Content 機能では、ユーザーがオフライン時のメディア視聴を追跡できます。例えば、ユーザーがモバイルデバイスにアプリをダウンロードしてインストールした後、そのアプリを使用してコンテンツをデバイスのローカルストレージにダウンロードするとします。ダウンロードされたデータを追跡するために、アドビは Downloaded Content 機能を開発しました。この機能を使用すると、デバイスの接続状態に関係なく、ユーザーがデバイスのストレージからコンテンツを再生した場合に、トラッキングデータがデバイスに保存されます。ユーザーが再生セッションを終了し、デバイスがオンラインに戻ると、保存されたトラッキング情報が単一のペイロード内でメディアコレクション API バックエンドに送信されます。保存されたトラッキング情報は、通常どおりメディアコレクション API で処理およびレポートされます。

2 つのアプローチの対比：

* オンライン

  このリアルタイムアプローチでは、メディアプレーヤーが各プレーヤーイベントの発生時にトラッキングデータを送信し、10 秒ごと（広告の場合は 1 秒ごと）にネットワーク ping を 1 つずつバックエンドに送信します。

* オフライン（Downloaded Content 機能）

  このバッチ処理アプローチでは、同じセッションイベントを生成する必要がありますが、単一セッションとしてバックエンドに送信されるまで、デバイスに保存されます（後述の例を参照）。

どちらのアプローチにもそれぞれ長所と短所があります。
* オンラインシナリオは、リアルタイムに追跡します。各ネットワーク呼び出しの前に接続性チェックが必要です。
* オフラインシナリオ（Downloaded Content 機能）は、1 つのネットワーク接続性チェックのみ必要ですが、デバイスに、より大きなメモリフットプリントが必要です。

## 実装 {#implementation}

### サポート対象のプラットフォーム

コンテンツのトラッキングは、iOS および Android モバイルデバイスでサポートされます。

### イベントスキーマ

Downloaded Content 機能は、（標準）オンラインメディアコレクション API のオフラインバージョンなので、プレーヤーがバックエンドにバッチおよび送信するイベントデータは、オンライン呼び出しをおこなう際に使用するのと同じイベントスキーマを使用する必要があります。これらのスキーマについて詳しくは、次を参照してください。
* [概要;](/help/implementation/media-collection-api/mc-api-overview.md)
* [イベントリクエストの検証](/help/implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### イベントの順序

* バッチペイロードの最初のイベントは、メディアコレクション API で通常おこなうように、`sessionStart` である必要があります。
* **ダウンロードされたコンテンツを送信していることをバックエンドに示すために、`media.downloaded: true`** イベントの標準メタデータパラメーター（`params` キー）に `sessionStart` を含める必要があります。ダウンロードされたデータを送信する際に、このパラメーターが存在しないか、false に設定されている場合、API は応答コード 400（無効な要求）を返します。このパラメーターは、バックエンドに対して、ダウンロードされたコンテンツとライブコンテンツを区別します。ライブセッションに `media.downloaded: true` が設定されている場合、同様に API からの応答が 400 になります。
* プレーヤーイベントを発生順に正しく保存するのは実装側の責任です。

### 応答コード

* 201 - Created: Successful Request。データが有効であり、セッションが作成されたので、処理されます。
* 400 - Bad Request。スキーマの検証に失敗し、すべてのデータが破棄されたので、セッションデータは処理されません。

## Adobe Analtyics との統合 {#integration-with-adobe-analtyics}

ダウンロードされたコンテンツシナリオ用に Analytics 開始／終了呼び出しを計算する際に、バックエンドは、`ts.` と呼ばれる追加の Analytics フィールドを設定します。これらは、受け取った最初および最後のイベント（開始および終了）のタイムスタンプです。このメカニズムにより、完了したメディアセッションを正しい時点に配置できます（つまり、ユーザーが数日間オンラインに戻らなくても、コンテンツが実際に視聴された時点でメディアセッションが発生したと報告されます）。_タイムスタンプオプションのレポートスイートを作成して、Adobe Analytics 側でこのメカニズムを有効にする必要があります。_ タイムスタンプオプションのレポートスイートを有効にするには、[タイムスタンプオプション](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html?lang=ja)を参照してください。

## サンプルセッションの比較 {#sample-session-comparison}

### オンラインコンテンツ

```
POST /api/v1/sessions HTTP/1.1

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
POST /api/v1/downloaded HTTP/1.1

[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },  
    params:{...},
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

### サポート終了のお知らせ

>[!IMPORTANT]
>
>ダウンロードしたコンテンツは、以前は `/api/v1/sessions` API にも送信することができました。この方法によるダウンロードコンテンツのトラッキングは、**非推奨**&#x200B;となり、今後&#x200B;**削除**&#x200B;される予定です。


`/api/v1/sessions` API は、セッション初期化イベントのみを受け付けます。
新しい API を使用する場合、以前は必須だった `media.downloaded` フラグは不要になりました。
新たにダウンロードしたコンテンツの実装には `/api/v1/downloaded` API を使用することと、古い API に依存する既存の実装を更新することを強くお勧めします。


```
POST /api/v1/sessions HTTP/1.1
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },
    params:{
        "media.downloaded": true,
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

## メディアトラッカー API リファレンス

ダウンロードしたコンテンツの設定方法について詳しくは、[メディアトラッカー API リファレンス](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)を参照してください。
