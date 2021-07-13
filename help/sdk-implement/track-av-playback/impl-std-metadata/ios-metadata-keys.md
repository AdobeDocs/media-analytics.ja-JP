---
title: iOSのメタデータキーの説明
description: 使用可能なiOSのメタデータキーについて説明します。
uuid: 8eb90111-c9dd-4ca7-9766-91530a8ae6cf
exl-id: a4bbbcba-9644-486a-95f4-65e5dc57623e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 90%

---

# iOS のメタデータキー{#ios-metadata-keys}

[iOS API リファレンス](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/)

送信元 `ADBStandardMetadataKeys.h`:

## ビデオのメタデータキー

| 定数名 | 説明 | タイプ |
|---|---|---|
| `ADBVideoMetadataKeySHOW` | 番組 | ビデオ |
| `ADBVideoMetadataKeySEASON` | シーズン | ビデオ |
| `ADBVideoMetadataKeyEPISODE` | エピソード | ビデオ |
| `ADBVideoMetadataKeyASSET_ID` | アセット | ビデオ |
| `ADBVideoMetadataKeyGENRE` | ジャンル | ビデオ |
| `ADBVideoMetadataKeyFIRST_AIR_DATE` | 初回放送日 | ビデオ |
| `ADBVideoMetadataKeyFIRST_DIGITAL_DAT` | 初回デジタル日 | ビデオ |
| `ADBVideoMetadataKeyRATING` | レーティング | ビデオ |
| `ADBVideoMetadataKeyORIGINATOR` | 作成者 | ビデオ |
| `ADBVideoMetadataKeyNETWORK` | ネットワーク | ビデオ |
| `ADBVideoMetadataKeySHOW_TYPE` | 番組タイプ | ビデオ |
| `ADBVideoMetadataKeyAD_LOAD` | 広告読み込み | ビデオ |
| `ADBVideoMetadataKeyMVPD` | mvpd | ビデオ |
| `ADBVideoMetadataKeyAUTHORIZED` | Authorization | ビデオ |
| `ADBVideoMetadataKeyDAY_PART` | 日パート | ビデオ |
| `ADBVideoMetadataKeyFEED` | フィード | ビデオ |
| `ADBVideoMetadataKeySTREAM_FORMAT` | ストリーム形式 | ビデオ |

## オーディオのメタデータキー

| 定数名 | 説明 | タイプ |
|---|---|---|
| `ADBAudioMetadataKeyALBUM` | 番組 | Audio |
| `ADBAudioMetadataKeyARTIST` | シーズン | オーディオ |
| `ADBAudioMetadataKeyAUTHOR` | シーズン | オーディオ |
| `ADBAudioMetadataKeyLABEL` | エピソード | オーディオ |
| `ADBAudioMetadataKeyPUBLISHER` | アセット | オーディオ |
| `ADBAudioMetadataKeySTATION` | ジャンル | オーディオ |

## 広告のメタデータキー

| 定数名 | 説明 | タイプ |
|---|---|---|
| `ADBAdMetadataKeyADVERTISER` | 広告主 | 広告 |
| `ADBAdMetadataKeyCAMPAIGN_ID` | キャンペーン ID | 広告 |
| `ADBAdMetadataKeyCREATIVE_ID` | クリエイティブ ID | 広告 |
| `ADBAdMetadataKeyPLACEMENT_ID` | プレースメント ID | 広告 |
| `ADBAdMetadataKeySITE_ID` | サイト ID | 広告 |
| `ADBAdMetadataKeyCREATIVE_URL` | クリエイティブ URL | 広告 |
