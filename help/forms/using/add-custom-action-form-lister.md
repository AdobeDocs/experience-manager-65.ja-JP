---
title: フォームリスター項目にカスタムアクションボタンを追加
description: フォーム開発者は、フォームポータルページ上のフォームのリストに、さらにアクションを追加できます。 デフォルトでは、フォームリストを使用すると、フォームにアクセスして入力し、送信できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 32%

---

# フォームリスター項目にカスタムアクションボタンを追加{#adding-custom-action-on-form-lister-items}

AEM Formsでは、使用可能なフォームをリストするポータルページを作成できます。 デフォルトでは、ポータルページ上のフォームを検索してリストすることができます。 フォームを開いて、情報を入力し、送信することができます。 ポータルページに一覧表示されるフォームには、レンダリングアクションのみが標準で提供されています。 ポータルページの利用可能なアクションの詳細については、[フォームポータルページの作成](../../forms/using/creating-form-portal-page.md)を参照してください。

ポータルページに他のオプションを追加できます。 フォームポータルのテンプレートをカスタマイズすることで、これらのオプションやアクションをカスタマイズできます。

この記事では、フォームポータルページから直接フォームのリンクを送信するボタンを作成する方法を説明します。 このカスタマイズを行うには、Search &amp; Lister コンポーネントのテンプレートを更新する必要があります。

テンプレートにアクションを追加するために必要なコードは、以下で使用できます。 コードスニペットの `onclick` 属性にはメールでフォームのリンクを送信するスクリプトがあります。

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

カスタムテンプレートに同様のアクションを追加できます。 JavaScript 関数を定義するには、ページレベルのスクリプトに関数を追加し、必要なHTML要素にリンクします。 上記の例では、`onclick` 式はリンク関数です。

テンプレートに編集を行った後、サンプルのポータルページには、以下のようにフォームのリンクをメールで送信するボタンが含まれています。

![メール](assets/email.png)
