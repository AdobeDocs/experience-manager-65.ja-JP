---
title: AEM Forms のインストールでの永続性タイプの選択
description: 永続性タイプを適切に選択することをお勧めします。これにより、効率的で拡張性の高い AEM Forms 環境を構築することができます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '372'
ht-degree: 100%

---

# AEM Forms のインストールでの永続性タイプの選択 {#choosing-a-persistence-type-for-an-aem-forms-installation}

永続性タイプを適切に選択することをお勧めします。これにより、効率的で拡張性の高い AEM Forms 環境を構築することができます。

永続性とは、物理ストレージにコンテンツを保存する方法です。これは、実際のデータ構造とデータのストレージの仕組みを定義します。MicroKernel は、AEM Forms の永続性マネージャーとして機能します。AEM Forms は TarMK、MongoMK、RDBMK の永続性タイプ（MicroKernals）をサポートしています。AEM Forms インスタンスの用途とデプロイの種類（シングルサーバー、ファーム、クラスター環境）に応じて、AEM Forms の永続性タイプを選択できます。

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

TarMK はパフォーマンスを考慮して設計されています。一方、MongoMK と RDBMK はスケーラビリティを考慮して設計されています。オーサーインスタンスとパブリッシュインスタンスの両方において、「[TarMK の代わりに Mongo またはリレーショナルデータベース Microkernel を選択する](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p)」セクションで説明されている使用例を除き、すべての AEM Forms デプロイメントシナリオのデフォルトの永続性テクノロジーとして TarMK を使用することを強くお勧めします。

サポートされる Microkernel リストについては、「[AEM Forms on OSGi の技術要件](/help/sites-deploying/technical-requirements.md)」または「[AEM Forms on JEE でサポートされるプラットフォームの組み合わせ](/help/forms/using/aem-forms-jee-supported-platforms.md)」の記事を参照してください。

## TarMK の代わりに Mongo またはリレーショナルデータベース Microkernel を選択する {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

スケーラブルなクラスター化された AEM Forms 環境は、並列に設定された 2 つ以上のアクティブなオーサーインスタンスの組み合わせです。そのため、すべての同時オーサリングのアクティビティをサポートする 1 つのサーバーが維持できなくなるような場合は、複数のオーサリングインスタンスを実行することができます。

スケーラブルな（クラスター化された）AEM Forms on JEE 環境に対応しているのは、MongoMK および RDBMK の永続性タイプのみです。サーバーの数やスケーラブル環境の規模は、インストールごとに異なります。考慮事項と使用例のリストについては、「[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)」および「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」の記事を参照してください。RDBMK や TarMK を使用した AEM Forms の運用規模を計画するにあたって詳細情報が必要な場合は、AEM Forms のサポートにお問い合わせいただくこともできます。
