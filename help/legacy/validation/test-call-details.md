---
title: テスト呼び出しの詳細
description: 実装の検証に必要な呼び出しについて説明します。
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# テスト呼び出しの詳細{#test-call-details}

## メディアプレーヤーを開始する {#start-the-media-player}

### Adobe Analytics（AppMeasurement）Start 呼び出し {#aa-start-call}

| パラメーター |  値（サンプル） |
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

* これら以外にも、メタデータを含むコンテキストデータ変数が存在します。メタデータについて詳しくは、以下を参照してください。
* リニアストリームの長さは、現在の番組の推定値に設定します。

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

* これら以外にも、メタデータを含むコンテキストデータ変数が存在します。メタデータについて詳しくは、以下を参照してください。
* ビデオ開始時点でのリニアストリームの再生ヘッドの位置は、0 ではなく、現在の番組の開始から経過した秒数に設定する必要があります。

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
* この呼び出しには、カスタムメタデータは含まれません。

## 広告再生の視聴 {#view-ad-playback}

### Adobe Analytics（AppMeasurement）Ad Start 呼び出し {#aa-ad-start-call}

| パラメーター |  値（サンプル） |
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

* これら以外にも、メタデータを含むコンテキストデータ変数が存在します。メタデータについて詳しくは、以下を参照してください。
* 広告の長さは、開始時に得られない場合、-1 に設定することができます。

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

* これら以外にも、メタデータを含むコンテキストデータ変数が存在します。メタデータについて詳しくは、以下を参照してください。
* 広告の長さは、開始時に得られない場合、-1 に設定することができます。

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
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_ad_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Media Analytics（ハートビート）Ad Play 呼び出し {#ma-ad-play-call}

| パラメーター |  値（サンプル） |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**play**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

### Media Analytics（ハートビート）Ad Pause 呼び出し {#ma-ad-pause-call}

| パラメーター |  値（サンプル） |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pause**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

### Media Analytics（ハートビート）Adobe Analytics Ad Complete 呼び出し {#ma-aa-ad-complete-call}

| パラメーター |  値（サンプル） |
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

| パラメーター |  値（サンプル） |
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

| パラメーター |  値（サンプル） |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pause**&#x200B;_ |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
