---
title: ストリーミングメディア用タグを使用してモバイル SDK を設定する方法
description: モバイルアプリ用のAdobeストリーミングメディアの実装方法を説明します。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 31%

---

# Mobile SDK のインストール {#install-mobile-sdks}

Android またはiOSにモバイルアプリ用のストリーミングメディアを実装するには、以下をインストールして設定します。

* **Adobe Experience Platform モバイル SDK**

   データを収集するには、Adobe Experience Platformのタグを使用します。 Adobe Experience Platform のタグは、他のタグ要件と共に Analytics コードを導入できるタグ管理ソリューションです。

* **Android 用メディア SDK** または **iOS用メディア SDK**

* **Adobe Media Analytics for Audio and Video 拡張機能**

SDK のダウンロードとその他のドキュメントリソースについては、 [タグを使用したメディア SDK、拡張機能、OTT SDK の取得](/help/getting-started/download-sdks.md)

* **有効な設定パラメーターを取得する**

   これらのパラメーターは、Analytics アカウントの設定後、Adobeの担当者から取得できます。

* **メディアプレーヤーに次の API を含めます**

   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。

   * *プレーヤー情報を提供する API*  — これには、メディア名、再生ヘッドの位置、広告、チャプターなど、現在再生中に関する情報が含まれます。
