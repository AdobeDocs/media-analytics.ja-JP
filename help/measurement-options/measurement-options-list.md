---
title: 測定オプション
description: null
uuid: null
translation-type: ht
source-git-commit: 967a126723ebbbe02097bd07edc2ed967cd35f4c
workflow-type: ht
source-wordcount: '293'
ht-degree: 100%

---


# 測定オプション {#measurement-options}

Adobe Media Analytics 拡張機能、メディア SDK およびメディアコレクション API を備えた Adobe Launch を使用して、オーディオとビデオを追跡できます。

## Adobe Media Analytics 拡張機能を備えた Adobe Launch

Launch は、アドビが提供する次世代タグ管理ソリューションです。Launch は、顧客体験の実現に必要なすべての分析、マーケティングおよび広告のタグをデプロイおよび管理するためのシンプルな手段を提供します。Launch との統合を構築して維持するには、拡張機能を使用します。拡張機能は、Launch UI とクライアント機能を拡張する JavaScript、HTML および CSS のパッケージです。詳しくは、[Experience Platform Launch ユーザーガイド](https://docs.adobe.com/content/help/ja-JP/launch/using/overview.html)を参照してください

Adobe Media Analytics（MA）の拡張機能により、オーディオおよびビデオ用のコア JavaScript Media SDK（Media 2.x SDK）が追加されます。この拡張機能では、Launch サイトまたはプロジェクトに `MediaHeartbeat` トラッカーインスタンスを追加する機能を提供します。

Media Analytics 拡張機能を備えた Adobe Launch では、以下が必要です。
* Adobe Experience Cloud のお客様である必要があります。
* Web ページに Launch または DTM 埋め込みコードをデプロイする必要があります。
* [Analytics 拡張機能](https://docs.adobe.com/content/help/ja-JP/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID 拡張機能](https://docs.adobe.com/content/help/ja-JP/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## メディア SDK

メディア SDK は、最もよく利用されるメディアプレーヤーと統合されます。

## メディアコレクション API（RESTful API）

SDK をサポートしていないプレーヤーと統合、または SDK 統合が不要な場合に統合します。<br>v2.2.0 リリース以降、オーディオおよびビデオの追跡をサポートするため、ビデオハートビートライブラリ（VHL）SDK の名前が Media Analytics SDK へと変更されました。Media 2.2.0 SDK は、VHL 2.x SDK シリーズと完全な下位互換性があります。名前の変更は、命名規則の変更に過ぎず、機能の変更を表すものではありません。
