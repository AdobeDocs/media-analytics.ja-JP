---
title: メディアストリーム属性とは何ですか。
description: 追加の処理ルールおよびカスタム変数を使用せずに、アプリケーションアクションをメディアトラッキングデータにリンクする方法を説明します。
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 87%

---

# メディアストリームのアトリビューション {#media-stream-attribution}

メディアストリームのアトリビューションを使用すると、追加の処理ルールやカスタム変数がなくても、アプリケーションアクションをメディアトラッキングデータにリンクできます。

## メディアトラッキング外部のメディアディメンション

メディアディメンションを、ページビューやカスタムリンクなどの Analytics 呼び出しに追加できます。 実装時に、メディアコンテキストデータパラメーターを Analytics トラッキングコールに追加する必要があります。メディアに使用できるコンテキストデータパラメーターの完全なリストについては、[オーディオおよびビデオパラメーター](/help/implementation/variables/audio-video-parameters.md)を参照してください。

特定のレポートに対してこの機能を有効にするには、Admin Console からメディアトラッキング設定を再度有効にします。

>[!NOTE]
>
>メディア指標はメディアトラッキング以外には使用 _できません_ これらのほとんどは、ハートビートイベントに基づいてストリーミングメディアコレクションアドオンによって計算されるからです。 また、メディア指標が異なる実装によって水増しされないことも重要です。

## メディアストリームのアトリビューションの使用

次の JavaScript の例は、名前が「Hero Banner」に設定されたカスタムリンクトラッキングコールを生成します。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Analytics レポートでは、`Show` eVar を使用してデータを分類したり、追跡リンクインスタンスをカウントしたりできます。レポートは次のようになります。

![](/assets/myShow-rpt-1.png)

## ユースケース

以下の例は、次の項目のユースケースを示します。

* カテゴリ配置
* ヒーロー配置
* エンゲージメント
* 購読

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
