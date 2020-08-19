---
title: イネーブルメントリソースのタグ付け
seo-title: イネーブルメントリソースのタグ付け
description: イネーブルメントリソースのタグ付けにより、メンバーがカタログを参照したときにリソースや学習パスのフィルタリングが可能になります
seo-description: イネーブルメントリソースのタグ付けにより、メンバーがカタログを参照したときにリソースや学習パスのフィルタリングが可能になります
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 61%

---


# イネーブルメントリソースのタグ付け {#tagging-enablement-resources}

## 概要 {#overview}

イネーブルメントリソースのタグ付けにより、メンバーが[カタログ](functions.md#catalog-function)を参照したときにリソースや学習パスのフィルタリングが可能になります。

基本的には：

* [各カタログのタグ名前空間](../../help/sites-administering/tags.md#creating-a-namespace) （タグ）の作成

   * [タグ権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions)
   * コミュニティメンバーのみ（非公開コミュニティ）

      * Allow read access for the [community site&#39;s member group](users.md#publish-group-roles)
   * サイト訪問者に対して、ログイン済みか匿名か（オープンコミュニティ）を問わず、

      * Allow read access for the `Everyone` group
   * [タグを公開する](../../help/sites-administering/tags.md#publishing-tags)



* [コミュニティサイトのタグの範囲の定義](sites-console.md#tagging)

   * [サイトの構造に存在するカタログを設定する](functions.md#catalog-function)

      * カタログインスタンスにタグを追加して、UIフィルターに表示されるタグのリストを制御できます。
      * Can add [pre-filters](catalog-developer-essentials.md#pre-filters), to restrict a catalog&#39;s included resources.

* [コミュニティサイトの公開](sites-console.md#publishing-the-site)
* [タグを有効化リソースに適用して](resources.md#create-a-resource) 、カテゴリに基づいてフィルタリングされる可能性がある
* [有効化リソースを発行する](resources.md#publish)

## コミュニティサイトタグ {#community-site-tags}

コミュニティサイトを作成または編集するときに、[タグ付け設定](sites-console.md#tagging)で既存のタグ名前空間のサブセットを選択することで、そのサイトの機能で使用可能なタグの範囲を設定します。

タグはコミュニティサイトに対していつでも作成または追加できますが、データベースの設計と同じように、あらかじめ分類を策定しておくことを推奨します。[タグの使用](../../help/sites-authoring/tags.md)を参照してください。

既存のコミュニティサイトに後からタグを追加する場合は、サイトの構造内のカタログ機能に新しいタグを追加する前に、編集を保存する必要があります。

コミュニティサイトでは、サイトを公開してタグを公開した後、コミュニティのメンバーに対する読み取りアクセスを有効にする必要があります。[タグ権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions)を参照してください。

The following is how it appears in CRXDE when an administrator applies read permissions to `/etc/tags/ski-catalog` for the group `Community Enable Members`.

![site-tags](assets/site-tags.png)

## カタログのタグ名前空間 {#catalog-tag-namespaces}

カタログ機能は、自身を定義するためにタグを使用します。コミュニティサイトでカタログ機能を設定する際、選択するタグ名前空間のセットは、コミュニティサイトに設定されたタグメッセージの範囲によって定義されます。

カタログ機能には、カタログのフィルター UI に表示されるタグを定義するタグ設定が含まれています。「すべての名前空間」の設定は、コミュニティサイトに対して選択されたタグ名前空間の範囲を指します。

![カタログ名前空間](assets/catalog-namespace.png)

## イネーブルメントリソースへのタグの適用 {#applying-tags-to-enablement-resources}

Enablement resources and learning paths will appear in all catalog when `Show in Catalog` is checked. リソースおよび学習パスにタグを追加すると、特定のカタログに事前フィルタリングしたり、カタログUIでフィルタリングしたりできます。

Restricting enablement resources and learning paths to specific catalogs is accomplished by creating [pre-filters](catalog-developer-essentials.md#pre-filters).

カタログ UI を使用すると、訪問者は、そのカタログに表示されているリソースや学習パスのリストにタグフィルターを適用できるようになります。

イネーブルメントリソースにタグを適用する管理者は、より高度な分類を可能にするサブタグを選択するために、カタログに関連付けられているタグ名前空間に加えて、分類についても理解している必要があります。

For example, if a `ski-catalog` namespace were created and set on a catalog named `Ski Catalog`, it might have two child tags: `lesson-1` and `lesson-2`.

この場合は、以下のいずれかのタグが付けられたイネーブルメントリソースが、

* ski-catalog:lesson-1
* ski-catalog:lesson-2

イネーブルメントリソースの公開後に `Ski Catalog` に表示されます。

![basic-info](assets/applytags-basicinfo.png)

## パブリッシュ環境でのカタログの表示 {#viewing-catalog-on-publish}

オーサー環境ですべてをセットアップして公開したら、パブリッシュ環境で、カタログを使用してイネーブルメントリソースを検索してみることができます。

タグ名前空間がドロップダウンメニューに表示されない場合は、パブリッシュ環境で権限が適切に設定されているかを確認してください。

タグ名前空間を追加しても見つからない場合は、タグとサイトが再公開されているかを確認してください。

カタログ表示時にタグを選択してもイネーブルメントリソースが表示されない場合は、カタログの名前空間のタグがイネーブルメントリソースに適用されているかを確認してください。

![表示カタログ](assets/viewcatalog.png)

