---
seo-title: ダウンロードされたコンテンツの追跡
title: ダウンロードされたコンテンツの追跡
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# ダウンロードされたコンテンツの追跡{#track-downloaded-content}

## 概要 {#section_hcy_3pk_cfb}

ダウンロードされたコンテンツ機能を使用すると、ユーザーがオフラインの間にメディアの消費を追跡できます。 例えば、ユーザーがモバイルデバイスでアプリをダウンロードし、インストールします。その後、アプリを使用してコンテンツをデバイスのローカルストレージにダウンロードします。To track this downloaded data, Adobe has developed the Downloaded Content feature. With this feature, when the user plays content from a device's storage, tracking data is stored on the device, regardless of the device's connectivity. ユーザーが再生セッションを終了し、デバイスがオンラインに戻ると、保存されたトラッキング情報が、単一のペイロード内のMedia Collection APIバックエンドに送信されます。 ここから、メディアコレクションAPIでは通常どおり処理とレポートが実行されます。

2つのアプローチを比較する：

* オンライン

   このリアルタイムアプローチを使用すると、メディアプレイヤーは各プレーヤーイベントに対してトラッキングデータを送信し、10秒（広告の場合は1秒ごとに）ごとに、1回ずつバックエンドにネットワークpingを送信します。

* オフライン（ダウンロード済みコンテンツ機能）

   このバッチ処理アプローチでは、同じセッションイベントを生成する必要がありますが、単一のセッションとしてバックエンドに送信されるまで、それらはデバイスに保存されます（以下の例を参照）。

各アプローチには利点と欠点があります。
* オンラインシナリオはリアルタイムで追跡し、これには、各ネットワーク呼び出しの前に接続チェックが必要です。
* オフラインシナリオ（ダウンロードされたコンテンツ機能）では、ネットワーク接続の確認が1つだけ必要ですが、デバイスのメモリ使用量も増えます。

## 実装 {#section_jhp_jpk_cfb}

### イベントスキーマ

ダウンロードされたコンテンツ機能は、（標準の）オンラインメディアコレクションAPIのオフラインバージョンなので、プレーヤーがバッチ処理してバックエンドに送信するイベントデータは、オンライン呼び出しを行う際に使用するのと同じイベントスキーマを使用する必要があります。 For information on these schemas, see:
* [概要;](/help/media-collection-api/mc-api-overview.md)
* [イベントリクエストの検証](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### イベントの順序

* バッチペイロードの最初のイベントは、Media Collection API `sessionStart` で通常どおりに設定する必要があります。
* **You must include`media.downloaded: true`** in the standard metadata parameters (`params` key) on the `sessionStart` event to indicate to the back-end that you are sending downloaded content. If this parameter is not present or is set to false when you send downloaded data, the API will return a 400 response code (Bad Request). This parameter distinguishes downloaded versus live content to the back-end. (Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* プレーヤーイベントを発生順に正しく保存するのは実装側の責任です。

### Response codes

* 201 - Created: Successful Request。データが有効であり、セッションが作成されたので、処理されます。
* 400 - Bad Request。スキーマの検証に失敗し、すべてのデータが破棄されたので、セッションデータは処理されません。

## Adobe Analtyics との統合 {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called  These are timestamps for the first and last events received (start and complete). `ts.`このメカニズムを使用すると、完了したメディアセッションを正しい時点に配置できます（例えば、ユーザーが数日間オンラインに戻らなかった場合でも、コンテンツが実際に表示された時点でメディアセッションが発生したと報告されます）。 _タイムスタンプオプションのレポートスイートを作成して、Adobe Analytics 側でこのメカニズムを有効にする必要があります。_ タイムスタンプオプションのレポートスイートを有効にする方法については、タイムスタンプオプシ [ョンを参照してください。](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## サンプルセッションの比較 {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### Online Content

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

### Downloaded Content

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

