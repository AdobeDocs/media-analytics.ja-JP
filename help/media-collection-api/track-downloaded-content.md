---
seo-title: ダウンロードされたコンテンツの追跡
title: ダウンロードされたコンテンツの追跡
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# ダウンロードされたコンテンツの追跡{#track-downloaded-content}

## 概要 {#section_hcy_3pk_cfb}

Downloaded Content API では、ユーザーがオフライン時のメディア視聴を追跡できます。例えば、ユーザーがモバイルデバイスでアプリをダウンロードし、インストールします。その後、アプリを使用してコンテンツをデバイスのローカルストレージにダウンロードします。このダウンロードされたデータを追跡するために、アドビは Downloaded Content API を開発しました。この API を使用すると、デバイスの接続状態に関係なく、ユーザーがデバイスのストレージからコンテンツを再生した場合に、トラッキングデータがデバイスに保存されます。ユーザーが再生セッションを完了し、デバイスがオンラインのときに、保存された追跡情報が単一のペイロード内でメディア収集APIに送信されます。そこから、この API の基になっているメディアコレクション API で通常どおり処理とレポート作成が実行されます。

2つのアプローチのコントラスト:

* メディアコレクション API

   このリアルタイムアプローチを使用すると、メディアプレイヤーは各プレーヤーイベントでトラッキングデータを送信し、（広告用に1秒ごとに1秒ごとに）ネットワークpingを1秒ごとに1回ごとに送信します。

* ダウンロードされたコンテンツAPI

   このバッチ処理アプローチでは、同じセッションイベントを生成する必要がありますが、単一のセッションとしてバックエンドに送信されるまで、デバイスに保存されます（以下の例を参照）。

各アプローチには長所と短所があります。メディアコレクション API はリアルタイムで追跡しますが、そのためには各ネットワーク呼び出しの前に接続を確認する必要があります。Downloaded Content API ではネットワーク接続の確認が必要なのは一度だけですが、デバイスに大きなメモリフットプリントも必要になります。

## 実装 {#section_jhp_jpk_cfb}

### イベントスキーマ

ダウンロードされたコンテンツAPIはメディア収集APIに基づいているので、プレーヤーがバッチおよび送信するイベントデータは、メディア収集APIと同じイベントスキーマを使用する必要があります。For information on these schemas, see: [Overview;](/help/media-collection-api/mc-api-overview.md) and [Validating event requests.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### イベントの順序

* バッチペイロードの最初のイベントは、`sessionStart` でなければなりません。
* You must include `media.downloaded: true` in the standard metadata parameters ( `params` key) on the `sessionStart` event. このパラメーターが存在しないか、false に設定されている場合、Downloaded Content API は応答コード 400（Bad Request）を返します。これにより、バックエンドで、ダウンロードされたコンテンツとライブコンテンツを区別し、それに応じて処理することができます。（ライブセッションで `media.downloaded: true` が設定されている場合、メディアコレクション API からの応答も同様に 400 になります）。

* プレーヤーイベントを発生順に正しく保存するのは実装側の責任です。

### 応答コード

* 201 - Created: Successful Request。データが有効であり、セッションが作成されたので、処理されます。
* 400 - Bad Request。スキーマの検証に失敗し、すべてのデータが破棄されたので、セッションデータは処理されません。

## Adobe Analtyics との統合 {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called `ts`. これらは、受信した最初と最後のイベントのタイムスタンプです（開始および完了）。このメカニズムにより、完了したメディアセッションを正しい時点で配置することができます（つまり、ユーザーが数日間オンラインに戻らない場合でも、メディアセッションは、コンテンツが実際に視聴された時点で発生したと報告されます）。*タイムスタンプオプションのレポートスイート*&#x200B;を作成して、Adobe Analytics 側でこのメカニズムを有効にする必要があります。To enable a timestamp optional report suite, see [Timestamps Optional.](https://marketing.adobe.com/resources/help/en_US/reference/timestamp-optional.html)

## サンプルセッションの比較 {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### メディアコレクション API

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

### ダウンロードされたコンテンツAPI

```
[{ 
    eventType: "sessionStart", 
    playerTime:{playhead: 0, ts: 1529997923478},  
    params:{
        "media.downloaded": true
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

