---
title: メディアストリーム属性とは何ですか。
description: 追加の処理ルールおよびカスタム変数を使用せずに、アプリケーションアクションをメディアトラッキングデータにリンクする方法を説明します。
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 100%

---

# メディアストリームアトリビューション

この機能を使用すると、追加の処理ルールおよびカスタム変数なしに、アプリケーション操作をメディアトラッキングデータにリンクできます。

## メディアトラッキングの外側にあるメディアディメンション

メディアストリームアトリビューションを使用すると、お客様は、任意のメディアディメンションを他のすべての Analytics 呼び出し（ページビューおよびカスタムリンクなど）に追加できます。実装時に、メディアコンテキストデータパラメーターを Analytics トラッキングコールに追加する必要があります。メディアに使用されるコンテキストデータパラメーターの完全なリストについては、[オーディオおよびビデオパラメーター](/help/metrics-and-metadata/audio-video-parameters.md)を参照してください。

また、この機能を有効にする各レポートに対して、Admin Console からメディアトラッキング設定を再度有効にする必要があります。

>[!NOTE]
>
>メディア指標は、ほとんどがハートビートイベントに基づいて Media Analytics で計算されるので、メディアトラッキングの外部では使用&#x200B;_できません_。また、メディア指標が異なる実装によって水増しされないことは重要です。

## 方法

次の JavaScript の例は、名前が「Hero Banner」に設定されたカスタムリンクトラッキングコールを生成します。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Analytics レポートでは、`Show` eVar を使用してデータを分類したり、追跡リンクインスタンスをカウントしたりできます。レポートは次のようになります。

![](/assets/myShow-rpt-1.png)

## ユースケース

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
