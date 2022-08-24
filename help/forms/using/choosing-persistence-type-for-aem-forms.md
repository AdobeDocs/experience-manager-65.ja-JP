---
title: AEM Forms のインストールに永続性タイプを選択する
seo-title: Choosing a persistence type for an AEM Forms installation
description: 永続性タイプを選択することをお勧めします。これにより、効率的で拡張性の高い AEM Forms 環境を構築することができます。
seo-description: Choose a persistence type wisely. It helps you build an efficient and scale able AEM Forms environment.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 100%

---

# AEM Forms のインストールに永続性タイプを選択する {#choosing-a-persistence-type-for-an-aem-forms-installation}

永続性タイプを選択することをお勧めします。これにより、効率的で拡張性の高い AEM Forms 環境を構築することができます。

永続性とは、物理ストレージにコンテンツを保存する方法です。これは、実際のデータ構造とデータのストレージの仕組みを定義します。MicroKernel は、AEM Forms の永続性マネージャーとして機能します。AEM Forms は TarMK、MongoMK、RDBMK の永続性タイプ（MicroKernals）をサポートしています。AEM Forms インスタンスの用途とデプロイの種類（シングルサーバー、ファーム、クラスター環境）に応じて AEM Forms の永続性タイプを選択できます。

>[!NOTE]
>
>LiveCycle ES4 SP1 では TarPM 永続性を使用してコンテンツを格納します。

次の表は、サポートしているすべての永続性タイプと各種のパラメーターを示しています。現在の環境に合わせて永続性タイプを選択する際に、この表を参照してください。

<table>
 <tbody>
  <tr>
   <th><strong>インストールのタイプ／コスト</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>スタンドアロンセットアップ</strong></th>
   <td>サポート対象<br /> </td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <th><strong>クラスターセットアップ</strong></th>
   <td>サポート対象外</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <th><strong>ライセンスコスト</strong></th>
   <td>AEM に含まれる </td>
   <td>別途ライセンスが必要</td>
   <td>別途ライセンスが必要</td>
  </tr>
 </tbody>
</table>

TarMK はパフォーマンスを考慮して設計されています。一方、MongoMK と RDBMK はスケーラビリティを考慮して設計されています。オーサーインスタンスと発行インスタンスの両方において、「[TarMK の代わりに Mongo または Relational Database Microkernel を選択する](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p)」セクションで説明されている使用例を除き、すべての AEM Forms デプロイメントシナリオのデフォルトの永続性テクノロジーとして TarMK を使用することを強くお勧めします。

サポートされる Microkernel については、「[OSGi の AEM Forms の技術要件](/help/sites-deploying/technical-requirements.md)」または「[JEE がサポートされるプラットフォームの組み合わせにおける AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md)」の記事の一覧を参照してください。

## TarMK の代わりに Mongo または Relational Database Microkernel を選択する {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

スケーラブルなクラスター化された AEM Forms 環境は、並列的に構成された 2 つ以上のアクティブなオーサーインスタンスの組み合わせです。そのため、すべての同時オーサリングのアクティビティをサポートしている 1 つのサーバーが維持できなくなるような場合に備え、2 つ以上のオーサーインスタンスを実行することができます。

JEE 環境でのスケーラブルなクラスター化された AEM Formsに対応しているのは、MongoMK および RDBMK の永続性タイプのみです。サーバーの数やスケーラブル環境の規模は各インストールに応じて異なります。考慮事項と使用例については、「[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)」および「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」の記事の一覧を参照してください。RDBMK や TarMK を使用した AEM Forms の運用規模を計画するにあたって詳細情報が必要な場合は、AEM Forms のサポートにお問い合わせいただくこともできます。
