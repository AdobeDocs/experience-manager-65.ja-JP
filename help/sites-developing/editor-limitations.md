---
title: 編集者の制限事項
description: タッチ操作対応 UI のエディターは、オーバーレイを使用して iframe に含まれるコンテンツを操作します。 この操作には、エディターの使用と開発者に対していくつかの制限事項があります。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 59%

---

# 編集者の制限事項{#editor-limitations}

タッチ操作対応 UI のエディターは、オーバーレイを使用して iframe に含まれるコンテンツを操作します。 この操作には、エディターの使用と開発者に対していくつかの制限事項があります。このページでは、これらの制限事項をまとめ、可能な限り解決策や回避策を提供します。

## 機能の制限事項 {#functional-limitations}

作成者は、エディターを使用してページを作成する際に、次の機能上の制限を受ける場合があります。

### リンクがアクティブにならない {#links-not-active}

[ページの編集](/help/sites-authoring/editing-content.md)時に、リンクがアクティブになりません。

* [コンテンツ内のリンクを使用して移動するには、**プレビュー**&#x200B;モード](/help/sites-authoring/editing-content.md#preview-mode)に切り替えます。

### 構造ページ {#structure-pages}

ページに名前を付けることはできません `structure`. という名前のページ `structure` は、ページエディターで編集できません。

## CSS の制限 {#css-limitations}

開発者は、エディターでの CSS の操作に次の制限を受ける場合があります。

### 要素が絶対配置される {#absolutely-positioned-elements}

絶対配置された要素により、そのオーバーレイの位置に問題が生じる可能性があります。

* この場合、エディターはまったく同じ寸法のオーバーレイを作成するので、絶対位置にある要素の寸法が正しいことを確認してください。

### vh 単位 {#vh-units}

`vh` iframe の高さはAdobe Experience Manager(AEM) によって自動的に調整される必要があるので、単位はサポートされません。

### 固定の背景画像 {#fixed-background-images}

固定の背景画像は iframe 内に埋め込まれるので、スクロール時に固定されて表示されない場合があります。

* ヘッダーバーのアクションで「**公開済みとしてページを表示**」を選択すると、ページが正しく表示されます。

### 100 ％の高さ {#height}

ページの body 要素では、100 ％の高さはサポートされていません。

* 次のように body 要素を「拡張」することで、全画面の body を実装できます。

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 余白の折りたたみ {#margin-collapsing}

余白の折りたたみの問題は、body 要素の最初の子要素に余白がある場合に発生することがあります。

* 解決策として、次のように body 要素レベルに clearfix を追加します。

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
