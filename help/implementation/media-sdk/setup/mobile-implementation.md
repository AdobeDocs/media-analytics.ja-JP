---
title: ストリーミングメディア用タグを使用して Mobile SDK を設定する方法
description: モバイルアプリ用の Adobe Streaming Media の実装方法を説明します。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: 1e4babe0df218342fc4836155139d908ba113510
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Mobile SDK のインストール {#install-mobile-sdks}

Android または iOS にモバイルアプリ用のストリーミングメディアを実装するには、以下をインストールして設定します。

* **Adobe Experience Platform モバイル SDK**

  データを収集するには、次のいずれかを使用します。
   * Adobe Experience Platform のタグ. Adobe Experience Platform のタグは、他のタグ要件と共に Analytics コードを導入できるタグ管理ソリューションです。
   * Adobe Experience Platform Edge

* **Android 用 Media SDK** または **iOS 用 Media SDK**

* **Adobe Media Analytics for Audio and Video 拡張機能**

SDK のダウンロード方法とその他のドキュメントリソースについては、[タグを使用した Media SDK、拡張機能、OTT SDK の取得](/help/getting-started/download-sdks.md)を参照してください

* **有効な設定パラメーターの取得**

  これらのパラメーターは、Analytics アカウントの設定後、アドビ担当者から取得できます。

* **メディアプレーヤーで以下の API を含める**

   * *プレーヤーイベントをサブスクライブするための API* - Media SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。

   * *プレーヤー情報を提供する API* - これには、メディア名、再生ヘッドの位置、広告、チャプターなど、現在再生中の情報が含まれます。
