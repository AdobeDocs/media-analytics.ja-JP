---
seo-title: テスト呼び出しの詳細
title: テスト呼び出しの詳細
uuid: d3a0e62f-2fc3-413d- ac56- adbbc9b3e983
translation-type: tm+mt
source-git-commit: 400c7ada4ab269017c3c2948c9056b4c1031d793

---


# テスト呼び出しの詳細{#test-call-details}

## ビデオプレーヤーの起動 {#section_qts_xff_f2b}

### Media Analyticsの開始呼び出し

| パラメーター | 値（サンプル）   |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| `a.media.name` | 123456 |
| `a.media.length` | 120 |
| `a.media.playerName` | HTML5 |
| `a.media.view` | true |
| `a.contentType` | vod |
| `custom.[value]` | カスタムメタデータフィールド |
| `a.media.[value]` | 標準メタデータフィールド |

**注意：**

* これら以外にも、メタデータを含むコンテキストデータ変数が存在します。メタデータについて詳しくは、以下を参照してください。
* リニアストリームの長さは、現在の番組の推定値に設定します。

### Media Analyticsの開始呼び出しの標準メタデータ

| パラメーター | 値（サンプル）   |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Heartbeat Start 呼び出し

| パラメーター | 値（サンプル）   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `l:asset:name` | Episode Title |
| `l:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | main |
| `s:meta:custom.[value]` | カスタムメタデータフィールド |
| `s:meta:a.media.[value]` | 標準メタデータフィールド |

### Media Analyticsの開始呼び出しのビデオメタデータ

| パラメーター | 値（サンプル）   |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

**注意：**

* これら以外にも、メタデータを含むコンテキストデータ変数が存在します。メタデータについて詳しくは、以下を参照してください。
* ビデオ開始時点でのリニアストリームの再生ヘッドの位置は、0 ではなく、現在の番組の開始から経過した秒数に設定する必要があります。

### Heartbeat Analytics Start 呼び出し

| パラメーター | 値（サンプル）   |
|---|---|
| `s:event:type` | aa_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `l:asset:name` | Episode Title |
| `l:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | main |

### Heartbeat Start 呼び出しのビデオメタデータ

| パラメーター | 値（サンプル）   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Heartbeat Start 呼び出しの標準メタデータ

| パラメーター | 値（サンプル）   |
|---|---|
| `s:meta:a.media.show` | 番組 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

**注意：**

* この呼び出しは、分析の pev2 が ms_s である呼び出しを分析サーバーに送信するようにハートビートライブラリがリクエストしたことを示します。
* この呼び出しには、カスタムメタデータは含まれません。

## 広告再生の視聴 {#section_wz3_yff_f2b}

### Media Analytics広告開始呼び出し

| パラメーター | 値（サンプル）   |
|---|---|
| `pev2` | msa_s |
| `a.media.name` | 123456 |
| `a.media.ad.name` | 9378 |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| `a.media.ad.length` | 15 |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| `a.media.ad.view` | True |
| `custom.[value]` | メタデータフィールド |
| `a.media.[value]` | 標準メタデータフィールド |

**注意：**&#x200B;これら以外にも、メタデータを含むコンテキストデータ変数が存在します。メタデータについて詳しくは、以下を参照してください。

### Heartbeat Ad Start 呼び出し

| パラメーター | 値（サンプル）   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `l:asset:ad_id` | 9378 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |
| `s:meta:custom.[value]` | カスタムメタデータフィールド |
| `s:meta:a.media.[value]` | 標準メタデータフィールド |

### Media Analytics広告開始呼び出しのビデオメタデータ

| パラメーター | 値（サンプル）   |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics広告開始呼び出しの標準メタデータ

| パラメーター | 値（サンプル）   |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

**注意：**

* これら以外にも、メタデータを含むコンテキストデータ変数が存在します。メタデータについて詳しくは、以下を参照してください。
* 広告の長さは、開始時に得られない場合、-1 に設定することができます。

### Heartbeat Analytics Ad Start 呼び出し

| パラメーター | 値（サンプル）   |
|---|---|
| `s:event:type` | aa_ad_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `l:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |

### Heartbeat Ad Start 呼び出しのビデオメタデータ

| パラメーター | 値（サンプル）   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Heartbeat Ad Start 呼び出しの標準メタデータ

| パラメーター | 値（サンプル）   |
|---|---|
| `s:meta:a.media.show` | 番組 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

**注意：**

* これら以外にも、メタデータを含むコンテキストデータ変数が存在します。メタデータについて詳しくは、以下を参照してください。
* 広告の長さは、開始時に得られない場合、-1 に設定することができます。

### Heartbeat Ad Complete 呼び出し

| パラメーター | 値（サンプル）   |
|---|---|
| `s:event:type` | complete |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `l:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |

### Heartbeat Ad Play 呼び出し

| パラメーター | 値（サンプル）   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `l:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |

## メインコンテンツの再生 {#section_u1l_1gf_f2b}

### Heartbeat Play 呼び出し

| パラメーター | 値（サンプル）   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 29 |
| `l:event:duration` | 10189 |
| `l:asset:name` | Episode Title |
| `l:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | main |

**注意：**

* 再生ヘッドの位置は、1 回の再生呼び出しにつき 10 ずつ増やす必要があります。
* `l:event:duration` の値は、前回のトラッキングコールからのミリ秒数を表し、10 秒の呼び出しのたびにほぼ同じ値である必要があります。

