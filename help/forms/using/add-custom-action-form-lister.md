---
title: フォームリスター項目にカスタムアクションボタンを追加
description: フォーム開発者は、フォームポータルページでフォームのリスト化に詳細アクションを追加できます。デフォルトでは、フォームのリスト化により、フォームにアクセス、入力および送信することができます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 100%

---

# フォームリスター項目にカスタムアクションボタンを追加{#adding-custom-action-on-form-lister-items}

AEM Forms では、使用可能なフォームをリストしたポータルページを作成できます。デフォルトの設定では、ポータルページで検索したりフォームをリストしたりできます。フォームを開いて、情報を入力および送信することができます。ポータルページにリストされているフォームには、レンダリングアクションのみがデフォルトで提供されています。ポータルページの利用可能なアクションの詳細については、[フォームポータルページの作成](../../forms/using/creating-form-portal-page.md)を参照してください。

ポータルページには、その他のオプションも追加できます。フォームポータルのテンプレートをカスタマイズすることで、これらのオプションやアクションをカスタマイズできます。

この記事は、フォームポータルページから直接フォームのリンクを送信するボタンの作成方法を示します。このカスタマイズには、検索とリスターコンポーネントのテンプレートをアップデートすることが必要です。

テンプレートにアクションを追加するのに必要なコードは以下の通りです。コードスニペットの `onclick` 属性にはメールでフォームのリンクを送信するスクリプトがあります。

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

カスタムテンプレートで同様のアクションを追加できます。JavaScript 関数を定義するには、その関数をページレベルスクリプトに追加して、必要な HTML 要素にリンクします。上記の例では、`onclick` 式はリンク関数です。

テンプレートに編集を行った後、サンプルのポータルページには、以下のようにフォームのリンクをメールで送信するボタンが含まれています。

![メール](assets/email.png)
