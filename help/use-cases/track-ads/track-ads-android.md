---
title: Android で広告をトラッキングする方法
description: メディア SDK を使用して、Android アプリケーションに広告トラッキングを実装します。
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4
exl-id: 1f96dde9-c924-4fce-8b14-7dec7137f265
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/9TbZkzhIR-b4nvKcVgmCAKsvN-nljf3YCDNPNEUA4yI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 381
ht-degree: 88%

---

# Android での広告の追跡{#track-ads-on-android}

以下の手順は、SDK 2.x を使用した実装についてのガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

## 広告トラッキングの定数

| 定数名 | 説明 |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | 追跡する AdBreak Start イベントの定数 |
| `MediaHeartbeat.Event.AdBreakComplete` | 追跡する AdBreak Complete イベントの定数 |
| `MediaHeartbeat.Event.AdStart` | 追跡する Ad Start イベントの定数 |
| `MediaHeartbeat.Event.AdComplete` | 追跡する Ad Complete イベントの定数 |
| `MediaHeartbeat.Event.AdSkip` | 追跡する Ad Skip イベントの定数 |

## 実装手順

1. プリロールを含め、いつ広告ブレークの境界が開始するかを識別し、広告ブレーク情報を使用して `AdBreakObject` を作成します。

   `AdBreakObject` リファレンス：

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | プリロール、ミッドロール、ポストロールなどの広告ブレーク名。 | ○ |
   | `position` | コンテンツ内の広告ブレークの位置（1から始まる）。 | ○ |
   | `startTime` | 広告ブレーク開始時の再生ヘッド値 | ○ |

   広告ブレークオブジェクトの作成：

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. `MediaHeartbeat` インスタンスの `AdBreakStart` で `trackEvent()` を呼び出し、広告ブレークの追跡を開始します。

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null);
   }
   ```

1. いつ広告が開始するかを識別し、広告情報を使用して `AdObject` インスタンスを作成します。

   `AdObject` リファレンス：

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | 広告のわかりやすい名前. | ○ |
   | `adId` | 広告の一意のID。 | ○ |
   | `position` | 広告ブレーク内の広告の位置を1から始めます。 | ○ |
   | `length` | 広告の長さ | ○ |

   広告オブジェクトの作成：

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME>
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. オプションで、コンテキストデータ変数を使用して標準または広告メタデータをメディアトラッキングセッションにアタッチします。

   * [Android での標準広告メタデータの実装](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)

   help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md

   * **カスタムの広告メタデータ** - カスタムのメタデータの場合は、カスタムデータ変数の変数オブジェクトを作成し、現在の広告のデータを設定します。

     ```java
     // Setting Ad Metadata
     HashMap<String, String> adMetadata = new HashMap<String, String>();
     adMetadata.put("affiliate", "Sample affiliate");
     adMetadata.put("campaign", "Sample ad campaign");
     ```

1. `MediaHeartbeat` インスタンスの `AdStart` イベントで `trackEvent()` を呼び出し、広告再生の追跡を開始します。

   カスタムメタデータ変数（または空のオブジェクト）への参照を、イベント呼び出しの 3 番目のパラメーターとして含めます。

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata);
   }
   ```

1. 広告の再生が広告の終わりに到達したら、`AdComplete` イベントで `trackEvent()` を呼び出します。

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null);
   }
   ```

1. ユーザーが広告のスキップを選択したので広告再生が完了しなかった場合は、`AdSkip` イベントを追跡します。

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null);
   }
   ```

1. 同じ `AdBreak` にその他の広告がある場合、手順 3 ～ 7 を繰り返します。
1. 広告ブレークが完了したら、`AdBreakComplete` イベントを使用して追跡します。

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null);
   }
   ```

詳しくは、追跡シナリオの[プリロール広告のある VOD 再生](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)を参照してください。
