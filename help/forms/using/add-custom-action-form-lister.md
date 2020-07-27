---
title: フォームリスター項目にカスタムアクションボタンを追加
seo-title: フォームリスター項目にカスタムアクションボタンを追加
description: フォーム開発者は、フォームポータルページでフォームのリストに詳細アクションを追加できます。デフォルトでは、フォームリストはフォームにアクセス、入力および送信することができます。
seo-description: フォーム開発者は、フォームポータルページでフォームのリストに詳細アクションを追加できます。デフォルトでは、フォームリストはフォームにアクセス、入力および送信することができます。
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 90%

---


# フォームリスター項目にカスタムアクションボタンを追加{#adding-custom-action-on-form-lister-items}

AEM Forms では、使用可能なフォームをリストしたポータルページを作成できます。デフォルトの設定では、ポータルページで検索したりフォームをリストしたりできます。フォームを開いて、情報を入力および送信することができます。レンダリングアクションのみポータルページにリストされているフォームにデフォルトで提供されています。ポータルページの利用可能なアクションの詳細については、「[フォームポータルページの作成](../../forms/using/creating-form-portal-page.md)」を参照してください。

ポータルページには、その他のオプションも追加することができます。フォームポータルのテンプレートをカスタマイズすることで、これらのオプションをカスタマイズできます。

この記事は、フォームポータルページから直接フォームのリンクを送信するボタンの作成方法を示します。このカスタマイズは、Search &amp; Listerコンポーネントのテンプレートのアップデートを必要とします。

テンプレートにアクションを追加するのに必要なコードは以下の通りです。The `onclick` attribute in the code snippet has a script to send a link of a form via email.

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

カスタムテンプレートで同様のアクションを追加できます。JavaScript関数を定義するには、その機能をページレベルで追加して、必要なHTML要素にリンクします。In the above example, the `onclick` expression is the linked function.

テンプレートに編集を行った後、サンプルのポータルページには、以下のようにEメールでフォームのリンクの送信するためのボタンが含まれています。

![email](assets/email.png)

