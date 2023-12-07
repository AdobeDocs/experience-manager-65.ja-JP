---
title: AEM Forms のインストールに永続性タイプを選択する
description: 永続性タイプを選択することをお勧めします。 これにより、効率的で拡張性の高いAEM Forms環境を構築できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 17%

---

# AEM Forms のインストールに永続性タイプを選択する {#choosing-a-persistence-type-for-an-aem-forms-installation}

永続性タイプを選択することをお勧めします。 これにより、効率的で拡張性の高いAEM Forms環境を構築できます。

永続性は、物理ストレージにコンテンツを保存する方法です。 データの実際のデータ構造と保存メカニズムを定義します。 MicroKernel は、AEM Formsの永続性マネージャーとして機能します。 AEM Formsは、TarMK、MongoMK、RDBMK の永続性 (MicroKernals) をサポートします。 AEM Formsインスタンスの目的とデプロイメントの種類（シングルサーバー、ファーム、クラスター）に応じて、AEM Formsの永続性タイプを選択できます。

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
   <th><strong>スタンドアロン設定</strong></th>
   <td>サポート対象<br /> </td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <th><strong>クラスターの設定</strong></th>
   <td>サポート対象外</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <th><strong>ライセンスコスト</strong></th>
   <td>AEM に含まれる </td>
   <td>別個のライセンスが必要です</td>
   <td>別個のライセンスが必要です</td>
  </tr>
 </tbody>
</table>

TarMK はパフォーマンスを目的として設計されていますが、MongoMK と RDBMK はスケーラビリティを目的として設計されています。 Adobeでは、オーサーインスタンスとパブリッシュインスタンスの両方について、すべてのAEM Formsデプロイメントシナリオのデフォルトの永続化テクノロジーとして TarMK を強く推奨しています。ただし、の節で説明する使用例は除きます [TarMK での Mongo またはリレーショナルデータベースマイクロカーネルの選択](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

サポートされる Microkernel の一覧については、 [AEM Forms on OSGi の技術要件](/help/sites-deploying/technical-requirements.md) または [JEE 上のAEM Formsでサポートされているプラットフォームの組み合わせ](/help/forms/using/aem-forms-jee-supported-platforms.md) 記事。

## TarMK での Mongo またはリレーショナルデータベースマイクロカーネルの選択 {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

スケーラブル（クラスター化）AEM Forms環境は、水平に設定された 2 つ以上のアクティブなオーサーインスタンスのセットです。 すべての同時オーサリングアクティビティをサポートする単一のサーバーが持続可能でなくなった場合は、複数のオーサーインスタンスを実行するよう選択できます。

JEE 環境上のスケーラブルな（クラスター化された）AEM Formsに対しては、MongoMK と RDBMK の永続性タイプのみがサポートされます。 サーバーの数やスケーラブル環境のサイズは、インストールごとに異なります。 考慮事項と例のリストについては、 [推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md) およびまたは [AEM Formsのアーキテクチャとデプロイメントトポロジ](/help/forms/using/aem-forms-architecture-deployment.md) 記事。 また、RDBMK および TarMK を使用したAEM Formsの容量計画の詳細については、AEM Formsサポートにお問い合わせください。
