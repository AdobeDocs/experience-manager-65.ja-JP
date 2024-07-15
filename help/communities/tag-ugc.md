---
title: ユーザー生成コンテンツのタグ付け
description: ユーザー生成コンテンツ（UGC）のタグ付けは、コミュニティメンバーが他のメンバーがコンテンツを検索するのを支援する方法です
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 9%

---

# ユーザー生成コンテンツのタグ付け {#tagging-user-generated-content}

## 概要 {#overview}

ユーザー生成コンテンツ（UGC）のタグ付けは、コミュニティメンバーが他のメンバーのコンテンツ検索を支援する手段です。

通常、タグは作成者とオーサー環境の管理者が適用します。 UGC のタグ付けは、UGC タグがパブリッシュ環境のコミュニティメンバーによって適用されるという点でユニークです。

タグの名前空間と分類は、両方のアプリケーションで同じです。

## Communities の機能 {#communities-features}

タグ付けを許可するように設定できるAEM Communities機能は次のとおりです。

* [ブログ](blog-feature.md)
* [Calendar](calendar.md)
* [ファイルライブラリ](file-library.md)
* [フォーラム](forum.md#configuretheaddedforum)
* [質問と答え](working-with-qna.md)

## タグの管理 {#administering-tags}

タグ名前空間と分類の作成と管理については、[ タグの管理 ](../../help/sites-administering/tags.md#tagging-console) を参照してください。

開発者向け情報については、[ タグの基本事項 ](tag.md) を参照してください。

適用されたタグを使用して投稿済み UGC を簡単に検索できるようにソーシャルタグクラウドコンポーネントをページに追加する方法については、[ ソーシャルタグクラウドの使用 ](tagcloud.md) を参照してください。

### タグの権限 {#tag-permissions}

デフォルトの権限は、パブリッシュ環境の全員がタグの名前空間を読み取ることができないように設定されています。

タグはパブリッシュ環境の UGC に適用されるので、コミュニティメンバーが適用するタグを選択できるようにするには、読み取り権限を有効にする必要があります。

[ タグ権限の設定 ](../../help/sites-administering/tags.md#setting-tag-permissions) を参照してください。

管理者がグループ `Community Engage Members` の `/etc/tag/discussions` に読み取り権限を適用した場合、CRXDE での表示は次のようになります。

![tag-permissions](assets/tag-permissions.png)
