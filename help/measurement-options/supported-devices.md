---
title: サポートされるデバイスとプラットフォーム
description: オーディオおよびビデオ用のAdobe Analyticsでは、各メディアストリームがすべてのデバイスで収集され、レポートされるようにします。
translation-type: tm+mt
source-git-commit: a8fec1747e688473af7a5eabbc4f9968772b5db3
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 15%

---


# サポートされるデバイスとプラットフォーム {#devices-supported}

>[!IMPORTANT]
>
>2021年8月31日にバージョン4のモバイルSDKのサポートが終了すると、アドビはiOSおよびAndroid向けのMedia Analytics SDKのサポートも終了します。  詳しくは、 [Media Analytics SDKサポート終了FAQを参照してください](/help/sdk-implement/end-of-support-faqs.md)。

オーディオおよびビデオ用のAdobe Analyticsは、次の主要デバイスをすべてサポートしています。

* iOS および Android のスマートフォンおよびタブレット
* ROKU、Apple TV、FireTV、Android TV の OTT デバイス
* デスクトップおよびラップトップの JavaScript ブラウザー

メディアSDKは、新しいバージョンのデバイスがリリースされると定期的に更新され、SDKを使用して、BrightcoveやOoyalaを含む現在最大のメディアプレイヤーと統合できます。

SDKが現在サポートされていないデバイスやプラットフォーム、またはSDKを使用したくない状況では、Media Collection APIを実装できます。 メディア収集APIを使用すると、デバイスまたはプラットフォームからMedia Analyticsバックエンドに直接RESTful API呼び出しを行うことができます。

現在サポートされているリストとプラットフォームの表を次に示します。 この SDK の最新バージョンをダウンロードするには、[SDK のダウンロード](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html)を参照してください。デバイスが一覧に表示されない場合は、そのデバイスのステータスについて、カスタマーケアまたはソリューションコンサルタントにお問い合わせください。

| ストリーミングプラットフォームとデバイス |  | AEP SDKを含むメディア起動拡張 | メディア SDK | メディアコレクション API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/モバイルWeb |  |  |  |  |
|  | JavaScriptブラウザー | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| モバイルアプリ |  |  |  |  |
|  | iOS デバイス | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android デバイス | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windowsデバイス |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV(tvOS) | 2020年予定 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>（ネイティブ） |
|  | Fire TV(Fire OS) | 2020年予定 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | 2020年予定 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | ゲームコンソール（Xbox ONE、ソニーPS3/PS4など） |  |  | ![](/help/assets/icon-blue-check.png) |
|  | トップ・ボックスの設定（Xfinity X1など） |  |  | ![](/help/assets/icon-blue-check.png) |
|  | スマートTV（Samsung、LG、Sony、Vizioなど） |  | ![](/help/assets/icon-blue-check.png)   <br>（Webベース）    | ![](/help/assets/icon-blue-check.png) |
| その他 |  |  |  |  |
|  | 新しく接続されたデバイス |  |  | ![](/help/assets/icon-blue-check.png) |

1. これらのSDKのサポートは2021年8月31日に終了します。 詳しくは、 [Media Analytics SDKサポート終了FAQを参照してください](/help/sdk-implement/end-of-support-faqs.md)。

各SDKでサポートされる最小プラットフォームバージョンについて詳しくは、 [最小プラットフォームバージョンのサポートを参照してください](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/setup/setup-overview.html)
