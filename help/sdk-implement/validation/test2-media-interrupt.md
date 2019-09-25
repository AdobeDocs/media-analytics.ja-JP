---
seo-title: テスト2メディア割り込み
title: テスト2メディア割り込み
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# Test 2: Media interruption{#test-media-interruption}

This test case validates mobile interruption behavior. It is a required element of your certification request.

## Certification Request Form

**次のURLから証明書申請フォームをダウンロードします。==&gt;**[Certification Request Form.](cert_req_form.docx)

## Test procedure

次の順序でタスクを実行して記録する必要があります。

1. **メディアプレイヤーの起動**

   メディアプレイヤーが起動すると、次の呼び出しが次の順序で送信されます。

   1. Adobe Analytics (AppMeasurement) Start
   1. Media Analytics (heartbeats) Start
   1. Media Analytics (heartbeats) Adobe Analytics Start call requested
   The first two calls above contain additional metadata and variables. For call parameters and metadata, see Test call details.[](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   The third call above tells the Media Analytics server that the Media SDK requested that the Adobe Analytics Start call () be sent to the Adobe Analytics server.`pev2=ms_s`

1. **Play main content for at least 5 minutes uninterrupted**

   **コンテンツの再生**

   During content playback, the Media SDK sends play calls (heartbeats) to the Media Analytics server every ten seconds.

   For call parameters and metadata, see Test call details.[](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **アプリまたはブラウザーをバックグラウンドに移動する**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **アプリまたはブラウザーを前面へ戻す**

   バックグラウンドからフォアグラウンドに戻したとき、コンテンツの再生が再開される必要があります。

1. **Play main content media for at least 5 minutes uninterrupted**

   For call parameters and metadata, see Test Call Details.[](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Close media player**

   No additional tracking calls should fire after the media player is closed.

