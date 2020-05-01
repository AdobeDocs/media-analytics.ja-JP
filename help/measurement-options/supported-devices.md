---
title: サポートされるデバイス
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 3a237ee31412784f708e772cc3a58047630e2184

---


# サポートされるデバイス {#devices-supported}

オーディオおよびビデオ用のAdobe Analyticsでは、各メディアストリームがすべてのデバイスで収集され、レポートされるようにします。

オーディオおよびビデオ用のAdobe Analyticsは、次の主要デバイスをすべてサポートしています。

* iOS および Android のスマートフォンおよびタブレット
* ROKU、Apple TV、FireTV、Android TV の OTT デバイス
* デスクトップおよびラップトップの JavaScript ブラウザー

新しいバージョンのデバイスがリリースされると、メディアSDKは定期的に更新されます。SDKを使用して、BrightcoveやOoyalaを含む現在最も大きなメディアプレイヤーと統合できます。

SDKが現在サポートされていないデバイスやプラットフォーム、またはSDKを使用したくない状況では、Media Collection APIを実装できます。 メディア収集APIを使用すると、デバイスまたはプラットフォームからMedia Analyticsバックエンドに直接RESTful API呼び出しを行うことができます。

現在サポートされているリストの表を次に示します。 この SDK の最新バージョンをダウンロードするには、[SDK のダウンロード](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html)を参照してください。デバイスが一覧に表示されない場合は、そのデバイスのステータスについて、カスタマーケアまたはソリューションコンサルタントにお問い合わせください。


| ストリーミングプラットフォーム/デバイス |  | AEP SDKを含むメディア起動拡張 | メディア SDK | メディアコレクション API |
|---------------------------|-----------------------------------------------|:----------------------------:|:-------------------:|:--------------------:|
| Web/モバイルWeb |  |  |  |  |
|  | JavaScriptブラウザー | X | X | X |
| モバイルアプリ |  |  |  |  |
|  | iOS デバイス | X | X | X |
|  | Android デバイス | X | X | X |
|  | Windowsデバイス |  |  | X |
| OTT |  |  |  |  |
|  | Apple TV（レガシー、TVOS） |  | X | X |
|  | ROKU |  | X<br>(BrightScript) | X<br>（ネイティブ） |
|  | Fire TV(Fire OS) |  | X | X |
|  | Android TV |  | X | X |
|  | Chromecast |  | X | X |
|  | ゲームコンソール（Xbox ONE、ソニーPS3/PS4など） |  |  | X |
|  | トップ・ボックスの設定（Xfinity X1など） |  |  | X |
|  | スマートTV（Samsung、LG、Sony、Vizioなど） |  | X<br>（Webベース） | X |
| その他 |  |  |  |  |
|  | 新しく接続されたデバイス |  |  | X |


メディア SDK については、[サポートされる最小プラットフォームバージョン](/help/sdk-implement/setup/setup-overview.md#minimum-platform-version)も参照してください。
