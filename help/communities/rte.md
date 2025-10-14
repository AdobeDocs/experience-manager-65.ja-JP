---
title: リッチテキストエディターの基本事項
description: マークアップを使用してテキストを入力できるリッチテキストエディターの基本と機能について説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 7%

---

# リッチテキストエディターの基本事項 {#rich-text-editor-essentials}

## 概要 {#overview}

リッチテキストエディター（RTE）を使用すると、マークアップでテキストを入力できます。

Communities コンポーネントの場合は、オーサー環境の [&#x200B; リッチテキストエディター &#x200B;](../../help/sites-authoring/rich-text-editor.md) と同様に、パブリッシュ環境で入力されるテキストに影響します。

![rich-text-editor](assets/rich-text-editor.png)

## リッチテキストエディターの有効化 {#enabling-rich-text-editor}

ユーザー生成コンテンツ（UGC）を許可する Communities コンポーネントを有効にして、RTE を許可できます。 コンポーネントがページに追加された場合や [function](functions.md) 内に含まれた場合、RTE はデフォルトで有効になっている場合とされていない場合があります。

有効にしない場合は、[&#x200B; オーサー編集モード &#x200B;](sites-console.md#authoring-site-content) に入り、編集するコンポーネントを選択して、「`Rich Text Editor`」チェックボックスをオンにします。

RTE は、次の Communities コンポーネントで使用できます。

* [ブログ](blog-feature.md)
* [Calendar](calendar.md)
* [コメント](comments.md)
* [Filelibrary](file-library.md)
* [フォーラム](forum.md)
* [メッセージ](configure-messaging.md)
* [Q&amp;A](working-with-qna.md)
* [レビュー](reviews.md)

## カスタマイズ {#customization}

[CKEditor](https://ckeditor.com/) に基づいた実装なので、リッチテキストエディターのカスタマイズが可能です。

Communities コンポーネントの現在の設定は、`cq.social.  scf   clientlib` ージ、次のリポジトリにあります

`/libs/clientlibs/social/commons/scf/ckrte.js`

今後のアップグレードでは編集内容が上書きされる可能性があるので、cq.social.scf clientlib の変更はお勧めしません。

### カスタマイズの例：インラインリンク {#example-customization-inline-links}

セキュリティ上の問題があるため、既定でメンバーに表示されるリッチ テキスト アイコンのセットには、ハイパーリンク オプションは含まれません。 UGC で hrefs が許可されている場合、いたずらの能力は広範囲です。

ツールバーにハイパーリンクオプションを追加するには：

* 「`links`」という名前のツールバーを追加
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 「**[!UICONTROL すべて保存]**」を選択します。

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links',
           items: [ 'Link','Unlink','Anchor' ]
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```
