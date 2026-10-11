---
title: ユーザー生成コンテンツのタグ付け
description: UGCのタグ付けは、コミュニティメンバーがコンテンツを検索して他のメンバーを支援する方法です
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 9%
---
# ユーザー生成コンテンツのタグ付け {#tagging-user-generated-content}

## 概要 {#overview}

ユーザー生成コンテンツ（UGC）のタグ付けとは、コミュニティメンバーがコンテンツを検索する際に役立つ手段のことです。

通常、タグはオーサー環境のオーサーと管理者によって適用されます。 UGCのタグ付けは、UGC タグがパブリッシュ環境のコミュニティメンバーによって適用されるという点で一意です。

タグの名前空間と分類は、両方のアプリケーションで同じです。

## Communities の機能 {#communities-features}

タグ付けを許可するように設定できるAEM Communitiesの機能は次のとおりです。

* [ブログ](blog-feature.md)
* [Calendar](calendar.md)
* [ファイルライブラリ](file-library.md)
* [フォーラム](forum.md#configuretheaddedforum)
* [質問と答え](working-with-qna.md)

## タグの管理 {#administering-tags}

タグの名前空間と分類の作成と管理については、[ タグの管理](../../help/sites-administering/tags.md#tagging-console)を参照してください。

開発者の情報については、[Tag Essentials](tag.md)を参照してください。

ソーシャルタグクラウドコンポーネントをページに追加し、適用されたタグを使用して投稿されたUGCを簡単に検索する方法については、[ ソーシャルタグクラウドの使用](tagcloud.md)を参照してください。

### タグの権限 {#tag-permissions}

デフォルトの権限は、パブリッシュ環境のすべてのユーザーがタグ名前空間を読み取ることを許可しないように設定されています。

タグはパブリッシュ環境のUGCに適用されるため、適用するタグを選択できるようにするには、コミュニティメンバーに対して読み取り権限を有効にする必要があります。

[ タグ権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions)を参照してください。

次に、管理者がグループ `Community Engage Members`に対して`/etc/tag/discussions`に読み取り権限を適用する場合のCRXDEでの表示方法を示します。

![tag-permissions](assets/tag-permissions.png)
