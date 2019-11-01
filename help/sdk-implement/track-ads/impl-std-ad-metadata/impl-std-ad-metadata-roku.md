---
title: Roku での標準広告メタデータの実装
description: Rokuの広告追跡で標準広告メタデータを使用する方法。
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Roku での標準広告メタデータの実装{#implement-standard-ad-metadata-on-roku}

## 実装標準広告メタデータ

標準広告メタデータの場合、プラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

