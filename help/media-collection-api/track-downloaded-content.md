---
title: ダウンロードされたコンテンツの追跡
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# ダウンロードされたコンテンツの追跡{#track-downloaded-content}

## 概要 {#overview}

ダウンロードされたコンテンツ機能を使用すると、ユーザーがオフラインの間にメディアの消費を追跡できます。 例えば、ユーザーがモバイルデバイスでアプリをダウンロードし、インストールします。その後、アプリを使用してコンテンツをデバイスのローカルストレージにダウンロードします。このダウンロードされたデータを追跡するために、アドビはダウンロードされたコンテンツ機能を開発しました。 この機能を使用すると、ユーザーがデバイスのストレージからコンテンツを再生すると、デバイスの接続状況に関係なく、デバイスに追跡データが保存されます。 ユーザーが再生セッションを終了し、デバイスがオンラインに戻ると、保存されたトラッキング情報が、単一のペイロード内のMedia Collection APIバックエンドに送信されます。 ここから、メディアコレクションAPIでは通常どおり処理とレポートが実行されます。

2つのアプローチを比較する：

* オンライン

   このリアルタイムアプローチを使用すると、メディアプレイヤーは各プレーヤーイベントに対してトラッキングデータを送信し、10秒（広告の場合は1秒ごとに）ごとに、1回ずつバックエンドにネットワークpingを送信します。

* オフライン（ダウンロード済みコンテンツ機能）

   このバッチ処理アプローチでは、同じセッションイベントを生成する必要がありますが、単一のセッションとしてバックエンドに送信されるまで、それらはデバイスに保存されます（以下の例を参照）。

各アプローチには利点と欠点があります。
* オンラインシナリオはリアルタイムで追跡し、これには、各ネットワーク呼び出しの前に接続チェックが必要です。
* オフラインシナリオ（ダウンロードされたコンテンツ機能）では、ネットワーク接続の確認が1つだけ必要ですが、デバイスのメモリ使用量も増えます。

## 実装 {#implementation}

### イベントスキーマ

ダウンロードされたコンテンツ機能は、（標準の）オンラインメディアコレクションAPIのオフラインバージョンなので、プレーヤーがバッチ処理してバックエンドに送信するイベントデータは、オンライン呼び出しを行う際に使用するのと同じイベントスキーマを使用する必要があります。 これらのスキーマの詳細は、次を参照してください。
* [概要;](/help/media-collection-api/mc-api-overview.md)
* [イベントリクエストの検証](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### イベントの順序

* バッチペイロードの最初のイベントは、Media Collection API `sessionStart` で通常どおりに設定する必要があります。
* **ダウンロードしたコ`media.downloaded: true`** ンテンツをバックエンドに通知するには、イベントの標準メ`params``sessionStart` タデータパラメーター（キー）を含める必要があります。 ダウンロードしたデータを送信する際にこのパラメーターが存在しない場合、またはfalseに設定されている場合、APIは400応答コード(Bad Request)を返します。 このパラメーターは、ダウンロード済みコンテンツとライブコンテンツをバックエンドで区別します。 (Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* プレーヤーイベントを発生順に正しく保存するのは実装側の責任です。

### 応答コード

* 201 - Created: Successful Request。データが有効であり、セッションが作成されたので、処理されます。
* 400 - Bad Request。スキーマの検証に失敗し、すべてのデータが破棄されたので、セッションデータは処理されません。

## Adobe Analtyics との統合 {#integration-with-adobe-analtyics}

ダウンロードしたコンテンツシナリオに対するAnalyticsの開始/終了呼び出しを計算する際、バックエンドは、受信した最初と最後のイベント（開始および完了）のタイムスタンプと呼ばれる追加のAnalyticsフィールドを設定します。 `ts.` このメカニズムを使用すると、完了したメディアセッションを正しい時点に配置できます（例えば、ユーザーが数日間オンラインに戻らなかった場合でも、コンテンツが実際に表示された時点でメディアセッションが発生したと報告されます）。 _タイムスタンプオプションのレポートスイートを作成して、Adobe Analytics 側でこのメカニズムを有効にする必要があります。_ タイムスタンプオプションのレポートスイートを有効にする方法については、タイムスタンプオプシ [ョンを参照してください。](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

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

### ダウンロード済みコンテンツ

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

