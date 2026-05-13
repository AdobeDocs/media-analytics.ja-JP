---
title: テスト呼び出しの詳細
description: 実装の検証に必要な呼び出しについて説明します。
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/98Oa98xntOkB9Fe3NQ30FUdvVk0JNKJMyzjgSTvncdI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 616
ht-degree: 78%

---

# テスト呼び出しの詳細{#test-call-details}

## メディアプレーヤーを開始する {#start-the-media-player}

### Adobe Analytics（AppMeasurement）Start 呼び出し {#aa-start-call}

| パラメーター |  値（サンプル）  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _&#x200B;**`a.media.name`**&#x200B;_ | _&#x200B;**123456**&#x200B;_ |
| _&#x200B;**`a.media.length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `a.media.playerName` | HTML5 |
| _&#x200B;**`a.media.view`**&#x200B;_ | _&#x200B;**true**&#x200B;_ |
| `a.contentType` | vod |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**カスタムメタデータフィールド**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**標準メタデータフィールド**&#x200B;_ |

**メモ:**

* 追加のコンテキストデータ変数が存在し、メタデータが含まれている必要があります。 以下のメタデータの詳細を参照してください。
* リニアストリームの長さは、現在の番組に最適な見積もりに設定する必要があります。

### Adobe Analytics（AppMeasurement）Start 呼び出しの標準メタデータ {#std-metadata-aa}

| パラメーター |  値（サンプル）  |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | réseau |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Adobe Analytics（AppMeasurement）Start 呼び出しのカスタムメタデータ {#custom-metadata-aa}

| パラメーター |  値（サンプル）  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Media Analytics（ハートビート）Start 呼び出し {#ma-start-call}

| パラメーター |  値（サンプル）  |
|---|---|
| `s:event:type` | start |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**0**&#x200B;_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**カスタムメタデータフィールド**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**標準メタデータフィールド**&#x200B;_ |

**メモ:**

* 追加のコンテキストデータ変数が存在し、メタデータが含まれている必要があります。 以下のメタデータの詳細を参照してください。
* ビデオ開始時のリニアストリームの再生ヘッドの位置は、現在の番組の開始以降に経過した秒数に設定する必要があります（0ではなく）。

### Media Analytics（ハートビート）Start 呼び出しの標準メタデータ {#std-metadata-ma}

| パラメーター |  値（サンプル）  |
|---|---|
| `s:meta:a.media.show` | 番組 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | réseau |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Media Analytics（ハートビート）Start 呼び出しのカスタムメタデータ {#custom-metadata-ma}

| パラメーター |  値（サンプル）  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics（ハートビート）Adobe Analytics Start 呼び出し {#ma-aa-start}

| パラメーター |  値（サンプル）  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**メモ:**

* この呼び出しは、Adobe Analytics（AppMeasurement）サーバーに送信される Adobe Analytics `pev2=ms_s` 呼び出しをメディア SDK がリクエストしたことを示します。
* この呼び出しにはカスタムメタデータが含まれていません。

## 広告の再生を表示 {#view-ad-playback}

### Adobe Analytics（AppMeasurement）Ad Start 呼び出し {#aa-ad-start-call}

| パラメーター |  値（サンプル）  |
|---|---|
| _&#x200B;**`pev2`**&#x200B;_ | _&#x200B;**msa_s**&#x200B;_ |
| `a.media.name` | 123456 |
| _&#x200B;**`a.media.ad.name`**&#x200B;_ | _&#x200B;**9378**&#x200B;_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _&#x200B;**`a.media.ad.length`**&#x200B;_ | _&#x200B;**15**&#x200B;_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _&#x200B;**`a.media.ad.view`**&#x200B;_ | _&#x200B;**True**&#x200B;_ |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**メタデータフィールド**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**標準メタデータフィールド**&#x200B;_ |

**メモ:**

* 追加のコンテキストデータ変数が存在し、メタデータが含まれている必要があります。 以下のメタデータの詳細を参照してください。
* 広告開始時に使用できない場合は、広告の長さを–1に設定できます。

### Adobe Analytics（AppMeasurement）Ad Start 呼び出しの標準メタデータ {#std-metadata-aa-ad-start}

| パラメーター |  値（サンプル）  |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | réseau |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Adobe Analytics（AppMeasurement）Ad Start 呼び出しのカスタムメタデータ {#custom-metadata-aa-ad-start}

| パラメーター |  値（サンプル）  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics（ハートビート）Ad Start 呼び出し {#ma-ad-start-call}

| パラメーター |  値（サンプル）  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _&#x200B;**`l:asset:length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**カスタムメタデータフィールド**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**標準メタデータフィールド**&#x200B;_ |

**メモ:**

* 追加のコンテキストデータ変数が存在し、メタデータが含まれている必要があります。 以下のメタデータの詳細を参照してください。
* 広告開始時に使用できない場合は、広告の長さを–1に設定できます。

### Media Analytics（ハートビート）Ad Start 呼び出しの標準メタデータ {#std-metadata-ma-ad-start}

| パラメーター |  値（サンプル）  |
|---|---|
| `s:meta:a.media.show` | 番組 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | réseau |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Media Analytics（ハートビート）Ad Start 呼び出しのカスタムメタデータ {#custom-metadata-ma-ad-start}

| パラメーター |  値（サンプル）  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics（ハートビート）Adobe Analytics Ad Start 呼び出し {#ma-aa-ad-start-call}

| パラメーター |  値（サンプル）  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_ad_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Media Analytics（ハートビート）Ad Play 呼び出し {#ma-ad-play-call}

| パラメーター |  値（サンプル）  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**play**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

### Media Analytics（ハートビート）Ad Pause 呼び出し {#ma-ad-pause-call}

| パラメーター |  値（サンプル）  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pause**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

### Media Analytics（ハートビート）Adobe Analytics Ad Complete 呼び出し {#ma-aa-ad-complete-call}

| パラメーター |  値（サンプル）  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**complete**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

## メインコンテンツの再生 {#play-main-content}

### Media Analytics（ハートビート）Play 呼び出し {#ma-play-call}

| パラメーター |  値（サンプル）  |
|---|---|
| `s:event:type` | play |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| _&#x200B;**`l:event:duration`**&#x200B;_ | _&#x200B;**10189**&#x200B;_ |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**メモ:**

* 再生ヘッドの位置は、1 回の再生呼び出しにつき 10 秒ずつ増やす必要があります。
* `l:event:duration` の値は、前回のトラッキングコールからのミリ秒数を表し、10 秒の呼び出しのたびにほぼ同じ値である必要があります。

## メインコンテンツの一時停止 {#pause-main-content}

### Media Analytics（ハートビート）Pause 呼び出し {#ma-pause-call}

| パラメーター |  値（サンプル）  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pause**&#x200B;_ |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
