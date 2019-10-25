---
title: メディアトラッキングの外側のメディアサイズ
seo-title: メディアトラッキングの外側のメディアサイズ
translation-type: tm+mt
source-git-commit: 5d20df537cd244a10f6c2e66cea622e98aa17a16

---


# メディアトラッキングの外側のメディアサイズ

この機能を使用すると、追加の処理ルールやカスタム変数を必要とせずに、アプリケーションアクションをメディアトラッキングデータにリンクできます。

これで、ページビュー数やカスタムリンクなど、他のすべての解析呼び出しに、任意のメディアディメンションを追加できるようになりました。 導入時に、Analyticsトラックコールにメディアコンテキストデータパラメーターを追加する必要があります。 メディアに使用するコンテキストデータパラメーターの完全なリストは、次のURLから入手できます。オーディ [オとビデオのパラメーター。](/help/metrics-and-metadata/audio-video-parameters.md)

また、この機能を有効にする各レポートに対して、管理コンソールからメディアトラッキング設定を再度有効にする必要があります。

>[!NOTE]
>メディア指標は __ 、ほとんどがMedia Analyticsによって計算されるので、メディアトラッキング以外では使用できません
>ハートビートイベントに基づいています。 また、メディア指標が異なる実装によって水増しされないことが重要です。

## 方法

以下のJavaScriptの例では、名前が「Hero Banner」に設定されたカスタムリンクトラッキングコールを生成します。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Analyticsレポートでは、eVarを使用してデータを分類で `Show` き、リンクトラッキングインスタンスをカウントできます。 レポートは次のようになります。

![](/assets/myShow-rpt-1.png)

## ユースケース

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
