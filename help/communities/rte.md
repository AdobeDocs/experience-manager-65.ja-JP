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

コミュニティ コンポーネントの場合は、に類似しています。 [オーサー環境でのリッチテキストエディター](../../help/sites-authoring/rich-text-editor.md)は、パブリッシュ環境に入力されるテキストに影響します。

![rich-text-editor](assets/rich-text-editor.png)

## リッチテキストエディターの有効化 {#enabling-rich-text-editor}

ユーザー生成コンテンツ（UGC）を許可する Communities コンポーネントを有効にして、RTE を許可できます。 コンポーネントがページに追加されたか、内に含まれているか [関数](functions.md)、RTE はデフォルトで有効になっている場合とされていない場合があります。

有効になっていない場合は、 [オーサー編集モード](sites-console.md#authoring-site-content)で、編集するコンポーネントを選択し、 `Rich Text Editor` チェックボックス。

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

実装は以下に基づいているので、リッチテキストエディターのカスタマイズが可能です [CKEditor](https://ckeditor.com/).

Communities コンポーネントの現在の設定は、 `cq.social.  scf   clientlib`、のリポジトリにあります。

`/libs/clientlibs/social/commons/scf/ckrte.js`

今後のアップグレードでは編集内容が上書きされる可能性があるので、cq.social.scf clientlib の変更はお勧めしません。

### カスタマイズの例：インラインリンク {#example-customization-inline-links}

セキュリティ上の問題があるため、既定でメンバーに表示されるリッチ テキスト アイコンのセットには、ハイパーリンク オプションは含まれません。 UGC で hrefs が許可されている場合、いたずらの能力は広範囲です。

ツールバーにハイパーリンクオプションを追加するには：

* 「」という名前のツールバーを追加 `links`“
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* を選択 **[!UICONTROL すべて保存]**

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
