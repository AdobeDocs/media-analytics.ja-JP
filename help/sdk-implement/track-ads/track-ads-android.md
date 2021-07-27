---
title: Android で広告をトラッキングする方法
description: メディア SDK を使用して、Android アプリケーションに広告トラッキングを実装します。
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4
exl-id: 1f96dde9-c924-4fce-8b14-7dec7137f265
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: ht
source-wordcount: '357'
ht-degree: 100%

---

# Android での広告の追跡{#track-ads-on-android}

以下の手順は、SDK 2.x を使用した実装についてのガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

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
   | `name` | プリロール、ミッドロール、ポストロールなど、広告ブレークの名前 | ○ |
   | `position` | コンテンツ内の広告ブレークの位置番号（1 から始まる）。 | ○ |
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
   | `adId` | 広告の一意の ID。 | ○ |
   | `position` | 広告ブレーク内の広告の位置番号（1 から始まる）。 | ○ |
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

   * [Android での標準広告メタデータの実装 ](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
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

詳しくは、追跡シナリオの[プリロール広告のある VOD 再生](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md)を参照してください。
