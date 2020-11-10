---
title: サポートされるデバイスとプラットフォーム
description: ストリーミングメディア用Adobe Analyticsは、各メディアストリームがすべてのデバイスで収集され、レポートされるようにします。
translation-type: tm+mt
source-git-commit: fdec4da99a43d889690638f1ff3579e145548b69
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 91%

---


# サポートされるデバイスとプラットフォーム {#devices-supported}

>[!IMPORTANT]
>
>2021 年 8 月 31 日にバージョン 4 のモバイル SDK のサポートが終了するのに伴い、iOS および Android 向けの Media Analytics SDK のサポートも終了します。詳しくは、[Media Analytics SDK のサポート終了に関する FAQ](/help/sdk-implement/end-of-support-faqs.md) を参照してください。

ストリーミングメディア用Adobe Analyticsは、以下を含む主要なデバイスをすべてサポートしています。

* iOS および Android のスマートフォンおよびタブレット
* ROKU、Apple TV、FireTV、Android TV の OTT デバイス
* デスクトップおよびラップトップの JavaScript ブラウザー

このメディア SDK はデバイスの新バージョンのリリースに合わせて定期的にアップデートされ、Brightcove や Ooyala など、現在の主要メディアプレーヤーと統合できます。

SDK が現在サポートされていないデバイスやプラットフォーム、または SDK を使用したくない状況では、Media Collection API を実装できます。メディアコレクション API を使用すると、デバイスまたはプラットフォームから Media Analytics バックエンドに直接 RESTful API 呼び出しをおこなうことができます。

現在サポートされているデバイスとプラットフォームの表を次に示します。この SDK の最新バージョンをダウンロードするには、[SDK のダウンロード](https://docs.adobe.com/content/help/ja-JP/media-analytics/using/sdk-implement/download-sdks.html)を参照してください。デバイスが一覧にない場合は、そのデバイスのステータスについて、カスタマーケアまたはソリューションコンサルタントにお問い合わせください。

| ストリーミングプラットフォームとデバイス |  | AEP SDK を含むメディア Launch 拡張機能 | メディア SDK | メディアコレクション API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web／モバイル Web |  |  |  |  |
|  | JavaScript ブラウザー | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| モバイルアプリ |  |  |  |  |
|  | iOS デバイス | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android デバイス | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows デバイス |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV（tvOS） | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>（BrightScript） | ![](/help/assets/icon-blue-check.png)<br>（ネイティブ） |
|  | Fire TV（Fire OS） | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | ゲームコンソール（Xbox ONE、ソニー PS3／PS4 など） |  |  | ![](/help/assets/icon-blue-check.png) |
|  | トップボックスの設定（Xfinity X1 など） |  |  | ![](/help/assets/icon-blue-check.png) |
|  | スマート TV（Samsung、LG、Sony、Vizio など） |  | ![](/help/assets/icon-blue-check.png)   <br>（Web ベース） | ![](/help/assets/icon-blue-check.png) |
| その他 |  |  |  |  |
|  | 新しい接続デバイス |  |  | ![](/help/assets/icon-blue-check.png) |

1. 次の SDK のサポートは 2021 年 8 月 31 日に終了します。詳しくは、[Media Analytics SDK のサポート終了に関する FAQ](/help/sdk-implement/end-of-support-faqs.md) を参照してください。

各 SDK でサポートされる最小プラットフォームバージョンについて詳しくは、[サポートされる最小プラットフォームバージョン](https://docs.adobe.com/content/help/ja-JP/media-analytics/using/sdk-implement/setup/setup-overview.html)を参照してください。
