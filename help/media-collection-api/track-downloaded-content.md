---
seo-title: ダウンロードされたコンテンツの追跡
title: ダウンロードされたコンテンツの追跡
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# ダウンロードされたコンテンツの追跡{#track-downloaded-content}

## 概要 {#section_hcy_3pk_cfb}

ダウンロードされたコンテンツ機能により、ユーザーがオフラインの間にメディア消費を追跡できます。例えば、ユーザーがモバイルデバイスでアプリをダウンロードし、インストールします。その後、アプリを使用してコンテンツをデバイスのローカルストレージにダウンロードします。このダウンロードされたデータを追跡するために、アドビはダウンロードされたコンテンツ機能を開発しました。この機能を使用すると、ユーザーがデバイスのストレージからコンテンツを再生すると、デバイスの接続性に関係なく、トラッキングデータがデバイスに保存されます。ユーザーが再生セッションを終了し、デバイスがオンラインに戻ると、保存された追跡情報が単一のペイロード内でメディア収集APIに送信されます。メディア収集APIでは、そこから処理およびレポート機能が通常どおりに進行します。

2つのアプローチのコントラスト:

* オンライン

   このリアルタイムアプローチを使用すると、メディアプレイヤーは各プレーヤーイベントでトラッキングデータを送信し、（広告用に1秒ごとに1秒ごとに）ネットワークpingを1秒ごとに1回ごとに送信します。

* オフライン（ダウンロードされたコンテンツ機能）

   このバッチ処理アプローチでは、同じセッションイベントを生成する必要がありますが、単一のセッションとしてバックエンドに送信されるまではデバイスに保存されます（以下の例を参照）。

各アプローチには、次の利点とデメリットがあります。
* オンラインシナリオはリアルタイムで追跡されます。これには、各ネットワーク呼び出しの前に接続チェックが必要です。
* オフラインのシナリオ（ダウンロードされたコンテンツ機能）には、ネットワーク接続のチェックが必要ですが、デバイス上ではより大きなメモリフットプリントが必要です。

## 実装 {#section_jhp_jpk_cfb}

### イベントスキーマ

ダウンロードされたコンテンツ機能は、単に（標準）オンラインメディア収集APIのオフラインバージョンであるので、プレーヤーがバッチ処理およびバックエンドに送信するイベントデータは、オンラインでのコールの際に使用すると同じイベントスキーマを使用する必要があります。これらのスキーマについて詳しくは、以下を参照してください。
* [概要;](/help/media-collection-api/mc-api-overview.md)
* [イベントリクエストの検証](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### イベントの順序

* バッチペイロードの最初のイベントは、メディアコレクションAPIを使用して通常どおりにする `sessionStart` 必要があります。
* **ダウンロードした`media.downloaded: true`** コンテンツを送信するバックエンドを示すために、イベントの標準メタデータパラメーター（`params``sessionStart` キー）に含める必要があります。ダウンロードしたデータを送信する場合、またはダウンロードしたデータを送信すると、APIは400応答コード（不正なリクエスト）を返します。このパラメーターは、ダウンロードされたコンテンツとライブコンテンツをバックエンドに区別します。(Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* プレーヤーイベントを発生順に正しく保存するのは実装側の責任です。

### 応答コード

* 201 - Created: Successful Request。データが有効であり、セッションが作成されたので、処理されます。
* 400 - Bad Request。スキーマの検証に失敗し、すべてのデータが破棄されたので、セッションデータは処理されません。

## Adobe Analtyics との統合 {#section_cty_kpk_cfb}

ダウンロードされたコンテンツのシナリオに対してAnalyticsの開始/終了呼び出しを計算するとき、バックエンドは、受信した最初と最後のイベントのタイムスタンプという `ts.` 追加のAnalyticsフィールドを設定します（開始および完了）。このメカニズムにより、完了したメディアセッションを正しい時点で配置することができます（つまり、ユーザーが数日間オンラインに戻らない場合でも、メディアセッションは、コンテンツが実際に視聴された時点で発生したと報告されます）。_タイムスタンプオプションのレポートスイートを作成して、Adobe Analytics 側でこのメカニズムを有効にする必要があります。_ タイムスタンプオプションのレポートスイートを有効にするには、 [タイムスタンプオプションを参照してください。](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## サンプルセッションの比較 {#section_qnk_lpk_cfb}

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

