---
title: エディターの制限事項
seo-title: Editor Limitations
description: タッチ操作対応の UI のエディターは、オーバーレイを使用して iframe 内に含まれるコンテンツを操作します。この操作には、エディターの使用と開発者に対していくつかの制限事項があります。
seo-description: The editor in the touch-enabled UI makes use of overlays to interact with content confined in an iframe. This interaction creates some limitations in both usage of the editor and also for developers.
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 100%

---

# エディターの制限事項{#editor-limitations}

タッチ操作対応の UI のエディターは、オーバーレイを使用して iframe 内に含まれるコンテンツを操作します。この操作には、エディターの使用と開発者に対していくつかの制限事項があります。このページでは、これらの制限事項をまとめ、可能な限り解決策や回避策を提供します。

## 機能の制限 {#functional-limitations}

作成者がエディターを使用してページを作成する際、以下の機能の制限が発生する可能性があります。

### リンクがアクティブにならない {#links-not-active}

[ページの編集](/help/sites-authoring/editing-content.md)時に、リンクがアクティブになりません。

* [コンテンツ内のリンクを使用して移動するには、**プレビュー**&#x200B;モード](/help/sites-authoring/editing-content.md#preview-mode)に切り替えます。

### 構造ページ {#structure-pages}

ページに `structure` と名前が付けられない 。`structure` と名前が付けられたページは、ページエディターで編集できません。

## CSS の制限 {#css-limitations}

開発者は、エディターの CSS のインタラクションに関して以下の制限が発生する可能性があります。

### 要素が絶対配置される {#absolutely-positioned-elements}

絶対配置された要素により、そのオーバーレイの位置に問題が生じる可能性があります。

* エディターではまったく同じサイズでオーバーレイが作成されるので、この問題が発生した場合は、絶対配置された要素のサイズが正しいことを確認します。

### vh 単位 {#vh-units}

iframe の高さは AEM によって自動調整されるので、`vh` 単位はサポートされません。

### 固定の背景画像 {#fixed-background-images}

固定の背景画像は、iframe 内に埋め込まれるので、スクロール時に固定されているように表示されない可能性があります。

* ヘッダーバーのアクションで「**公開済みとしてページを表示**」を選択すると、ページが正しく表示されます。

### 100 ％の高さ {#height}

ページの body 要素では、100 ％の高さはサポートされていません。

* フルスクリーンの body を実装するためには、次のように body 要素を「拡張」することで、回避策が可能になります。

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
