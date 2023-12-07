---
title: ユーザー生成コンテンツのタグ付け
description: ユーザー生成コンテンツ (UGC) のタグ付けは、コミュニティメンバーが他のメンバーがコンテンツを検索する際に役立つ方法です
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 9%

---

# ユーザー生成コンテンツのタグ付け {#tagging-user-generated-content}

## 概要 {#overview}

ユーザー生成コンテンツ (UGC) のタグ付けは、コミュニティメンバーが他のメンバーがコンテンツを検索する際に役立つ手段です。

通常、タグはオーサー環境で作成者および管理者が適用します。 UGC のタグ付けは、UGC タグがパブリッシュ環境のコミュニティメンバーによって適用される点で一意です。

タグの名前空間と分類は、両方のアプリケーションで同じです。

## Communities の機能 {#communities-features}

AEM Communitiesの機能は、タグ付けを許可するように設定できます。

* [ブログ](blog-feature.md)
* [Calendar](calendar.md)
* [ファイルライブラリ](file-library.md)
* [フォーラム](forum.md#configuretheaddedforum)
* [質問と答え](working-with-qna.md)

## タグの管理 {#administering-tags}

詳しくは、 [タグの管理](../../help/sites-administering/tags.md#tagging-console) タグ名前空間と分類の作成と管理

詳しくは、 [タグの基本事項](tag.md) 」を参照してください。

詳しくは、 [Social タグクラウドの使用](tagcloud.md) ページに Social タグクラウドコンポーネントを追加して、適用したタグを使用して、投稿された UGC を検索しやすくする。

### タグ権限 {#tag-permissions}

デフォルトの権限では、パブリッシュ環境の全員がタグ名前空間を読み取れないように設定されています。

タグはパブリッシュ環境で UGC に適用されるので、コミュニティメンバーが適用するタグを選択できるようにするには、読み取り権限をコミュニティメンバーに対して有効にする必要があります。

詳しくは、 [タグ権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions).

管理者がに読み取り権限を適用すると、CRXDE では次のように表示されます。 `/etc/tag/discussions` グループの `Community Engage Members`.

![tag-permissions](assets/tag-permissions.png)
