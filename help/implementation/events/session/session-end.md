---
title: セッション終了
description: 視聴者がコンテンツを放棄した場合は、直ちにメディアセッションを閉じます。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 5%
---

# セッション終了

セッション終了イベントは、メディア追跡セッションを直ちに不可逆的に閉じます。 セッション終了はハードクローズです。送信されると、セッションは終了され、それ以降のイベントは追跡できません。 プレーヤーが破壊されたり、ページがアンロードされたりするなど、追加のイベントが続かないことが確実な場合にのみ、セッション終了を使用します。 多くの場合、セッションの有効期限を自然発生的に切り落とすリスクを回避する方が安全です。 視聴者がコンテンツを完了した場合は、代わりに[ セッション完了](session-complete.md)に電話してください。

明示的なセッション終了がなければ、イベントなしの10分または再生ヘッドなしの30分が経過すると、セッションは自動的に終了します。

>[!NOTE]
>
>同じセッションに対してセッション終了を複数回呼び出すことができます。 バックエンドは、最初のイベントのセッションを閉じ、2番目のセッション終了を含む、そのセッション IDの後続のすべてのイベントをサイレントにドロップします。 視聴者がプレーヤーを閉じると同じ瞬間に30分のタイムアウトが期限切れになるなど、レース条件で重複した呼び出しを防ぐ必要はありません。

* **前提条件**: [ セッション開始](session-start.md)
* **関連する指標**：なし

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.sessionEnd"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

ビューアーがプレーヤーを閉じるか、離れるときに`trackSessionEnd`に電話します。

```swift
tracker.trackSessionEnd()
```

>[!TAB Android]

ビューアーがプレーヤーを閉じるか、離れるときに`trackSessionEnd`に電話します。

```kotlin
tracker.trackSessionEnd()
```

>[!TAB Edge六]

`sendMediaEvent`を`eventType: "media.sessionEnd"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

>[!TAB Media Edge API]

[sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

ビューアーがプレーヤーを閉じるか、離れるときに`trackSessionEnd`に電話します。

```javascript
tracker.trackSessionEnd();
```

>[!TAB Chromecast]

ビューアーがプレーヤーを閉じるか、離れるときに`trackSessionEnd`に電話します。

```javascript
ADBMobile.media.trackSessionEnd();
```

>[!TAB Roku 2.x]

ビューアーがプレーヤーを閉じるか、離れるときに`mediaTrackSessionEnd`に電話します。

```brightscript
ADBMobile().mediaTrackSessionEnd()
```

>[!TAB Media Collection API]

`sessionEnd`件の投稿を[ イベントエンドポイント ](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events)に送信します：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```

>[!ENDTABS]
