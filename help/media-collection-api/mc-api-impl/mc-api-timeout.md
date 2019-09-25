---
seo-title: タイムアウト条件
title: タイムアウト条件
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# タイムアウト条件{#timeout-conditions}

**メディアコレクションAPIのタイムアウト条件**

Media Collection APIは、ステートレスで、タイムアウト条件が発生した場合に新しいセッションIDを発行するMedia SDKと同じメカニズムを備えていません。 タイムアウト条件が発生すると、バックエンドはセッションを閉じます。さらに、そのセッション ID に対しておこなわれた後続のすべての呼び出しが破棄されます。セッションタイムアウトを処理するロジックは、クライアントで処理する必要があります。つまり、プレーヤーは、タイムアウト条件を監視して、タイムアウトが発生したときに新しいセッション ID を取得する必要があります。

* **10分：APIイベントなし**

   バックエンドがAPIイベントを受け取らない場合は、セッションを閉じます。
* **30分：再生ヘッドの変更なし**

   再生ヘッドが30分間移動しない場合（例：ユーザーが一時停止をヒットして離れた場合）、バックエンドはセッションを閉じます。

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

