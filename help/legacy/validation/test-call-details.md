---
title: テスト呼び出しの詳細
description: 実装の検証に必要な呼び出しについて説明します。
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 77%

---

# テスト呼び出しの詳細{#test-call-details}

## メディアプレーヤーを開始する {#start-the-media-player}

### Adobe Analytics（AppMeasurement）Start 呼び出し {#aa-start-call}

| パラメーター |  値（サンプル） |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**カスタムメタデータフィールド**_ |
| _**`a.media.[value]`**_ | _**標準メタデータフィールド**_ |

**メモ:**

* 追加のコンテキストデータ変数が存在し、メタデータを含んでいる必要があります。 以下のメタデータの詳細を参照してください。
* 線形ストリームの長さは、現在の番組に最適な見積もりに設定する必要があります。

### Adobe Analytics（AppMeasurement）Start 呼び出しの標準メタデータ {#std-metadata-aa}

| パラメーター |  値（サンプル） |
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

| パラメーター |  値（サンプル） |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Media Analytics（ハートビート）Start 呼び出し {#ma-start-call}

| パラメーター |  値（サンプル） |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**カスタムメタデータフィールド**_ |
| _**`s:meta:a.media.[value]`**_ | _**標準メタデータフィールド**_ |

**メモ:**

* 追加のコンテキストデータ変数が存在し、メタデータを含んでいる必要があります。 以下のメタデータの詳細を参照してください。
* ビデオ開始時のリニアストリームの再生ヘッドの位置は、現在の番組の開始時からの経過秒数（0 ではなく）に設定する必要があります。

### Media Analytics（ハートビート）Start 呼び出しの標準メタデータ {#std-metadata-ma}

| パラメーター |  値（サンプル） |
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

| パラメーター |  値（サンプル） |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics（ハートビート）Adobe Analytics Start 呼び出し {#ma-aa-start}

| パラメーター |  値（サンプル） |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**メモ:**

* この呼び出しは、Adobe Analytics（AppMeasurement）サーバーに送信される Adobe Analytics `pev2=ms_s` 呼び出しをメディア SDK がリクエストしたことを示します。
* この呼び出しには、カスタムメタデータは含まれません。

## 広告再生の表示 {#view-ad-playback}

### Adobe Analytics（AppMeasurement）Ad Start 呼び出し {#aa-ad-start-call}

| パラメーター |  値（サンプル） |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _**`a.media.ad.view`**_ | _**True**_ |
| _**`custom.[value]`**_ | _**メタデータフィールド**_ |
| _**`a.media.[value]`**_ | _**標準メタデータフィールド**_ |

**メモ:**

* 追加のコンテキストデータ変数が存在し、メタデータを含んでいる必要があります。 以下のメタデータの詳細を参照してください。
* 広告の開始時に利用できない場合、広告の長さは–1 に設定できます。

### Adobe Analytics（AppMeasurement）Ad Start 呼び出しの標準メタデータ {#std-metadata-aa-ad-start}

| パラメーター |  値（サンプル） |
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

| パラメーター |  値（サンプル） |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics（ハートビート）Ad Start 呼び出し {#ma-ad-start-call}

| パラメーター |  値（サンプル） |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**カスタムメタデータフィールド**_ |
| _**`s:meta:a.media.[value]`**_ | _**標準メタデータフィールド**_ |

**メモ:**

* 追加のコンテキストデータ変数が存在し、メタデータを含んでいる必要があります。 以下のメタデータの詳細を参照してください。
* 広告の開始時に利用できない場合、広告の長さは–1 に設定できます。

### Media Analytics（ハートビート）Ad Start 呼び出しの標準メタデータ {#std-metadata-ma-ad-start}

| パラメーター |  値（サンプル） |
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

| パラメーター |  値（サンプル） |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics（ハートビート）Adobe Analytics Ad Start 呼び出し {#ma-aa-ad-start-call}

| パラメーター |  値（サンプル） |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Media Analytics（ハートビート）Ad Play 呼び出し {#ma-ad-play-call}

| パラメーター |  値（サンプル） |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics（ハートビート）Ad Pause 呼び出し {#ma-ad-pause-call}

| パラメーター |  値（サンプル） |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics（ハートビート）Adobe Analytics Ad Complete 呼び出し {#ma-aa-ad-complete-call}

| パラメーター |  値（サンプル） |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## メインコンテンツの再生 {#play-main-content}

### Media Analytics（ハートビート）Play 呼び出し {#ma-play-call}

| パラメーター |  値（サンプル） |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
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

| パラメーター |  値（サンプル） |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
