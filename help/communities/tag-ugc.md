---
title: ユーザー生成コンテンツのタグ付け
seo-title: ユーザー生成コンテンツのタグ付け
description: ユーザー生成コンテンツ（UGC）のタグ付けは、コミュニティメンバーが他のメンバーによるコンテンツの検索を支援するための手段です
seo-description: ユーザー生成コンテンツ（UGC）のタグ付けは、コミュニティメンバーが他のメンバーによるコンテンツの検索を支援するための手段です
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Administrator
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 76%

---

# ユーザー生成コンテンツのタグ付け {#tagging-user-generated-content}

## 概要 {#overview}

ユーザー生成コンテンツ（UGC）のタグ付けは、コミュニティメンバーが他のメンバーによるコンテンツの検索を支援するための手段です。

通常、タグは作成者と管理者によってオーサー環境で適用されます。UGCのタグ付けは、UGCタグがパブリッシュ環境のコミュニティメンバーによって適用される点で一意です。

タグ名前空間と分類は、どちらで適用する場合も同じです。

## Communities の機能  {#communities-features}

AEM Communitiesの機能でタグ付けを許可するように設定できるものは次のとおりです。

* [ブログ](blog-feature.md)
* [Calendar](calendar.md)
* [ファイルライブラリ](file-library.md)
* [フォーラム](forum.md#configuretheaddedforum)
* [Q＆A](working-with-qna.md)

## タグの管理 {#administering-tags}

タグ名前空間と分類の作成と管理については、[タグの管理](../../help/sites-administering/tags.md#tagging-console)を参照してください。

開発者向けの情報については、[タグの重要事項](tag.md)を参照してください。

タグを使用した UGC 検索を容易にするために Social タグクラウドコンポーネントをページに追加するには、[Social タグクラウドの使用](tagcloud.md)を参照してください。

### タグ権限 {#tag-permissions}

デフォルトの権限では、パブリッシュ環境の全員がタグ名前空間を読み取れない設定になっています。

タグはパブリッシュ環境で UGC に適用されるので、適用するタグをコミュニティメンバーが選択できるようにするには、コミュニティメンバーに読み取り権限を付与にする必要があります。

[タグ権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions)を参照してください。

管理者が`/etc/tag/discussions`グループ`Community Engage Members`に対して読み取り権限を適用すると、CRXDEでは次のように表示されます。

![tag-permissions](assets/tag-permissions.png)
