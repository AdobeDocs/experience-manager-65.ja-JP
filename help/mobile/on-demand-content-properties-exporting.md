---
title: コンテンツのプロパティを使用したコンテンツのエクスポート
seo-title: Using Content Properties to Export Content
description: 以下のページに、アプリのプロパティとノードを示します。
seo-description: The following page shows App Properties and Nodes.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 10%

---

# コンテンツのプロパティを使用したコンテンツのエクスポート{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

アプリは、 *cq:Pages* AEMの

これらは、 *cq:Page* に加えて、統合のサポートプロパティを表す他のものも示します。

## アプリのプロパティ {#app-properties}

次の表にを示します。 **アプリのプロパティとノード**.

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ名</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>String:Path</td>
   <td><p>設定済みの Mobile On-DemandCloud Serviceへのパス。 AEM Mobileから Mobile On-Demand へのアクションに使用（API 呼び出し）</p> <p>この関連付けは、作成者がアプリの関連付け先となる Mobile On-DemandCloud Serviceを選択したときに、接続を管理タイルで設定します。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>String:Path</td>
   <td><p>アプリの書き出し設定のパス。 書き出し設定は、2 つの子 ContentSync 書き出し設定テンプレートを持つフォルダーです。</p> <p><i>dps-article</i>:記事のコンテンツを書き出すためのコンテンツ同期書き出し設定</p> <p><i>dps-HTMLResources</i>:アプリ/記事の共有リソースを書き出すためのコンテンツ同期書き出し設定</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>文字列</td>
   <td><p>このアプリがリンク/バインドされている Mobile On-Demand プロジェクトの ID/URI。</p> <p>この関連付けは、作成者が関連する Mobile On-DemandCloud Serviceで使用可能なプロジェクトのリストからプロジェクトを選択すると、接続を管理タイルを使用して設定されます。</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>文字列</td>
   <td>アプリのタイトル。</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>文字列</td>
   <td>コンテンツタイプ.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>日付</td>
   <td>AEMからAEM Mobileに共有リソースを最後にアップロードした日付。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:userid</td>
   <td>AEMからAEM Mobileへの共有リソースリクエストの最後のアップロードを実行したユーザーの ID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>String:Path</td>
   <td>ダッシュボード設定のパス。 パスは、必要に応じて、カスタムダッシュボード設定にリダイレクトできます。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>String:Path</td>
   <td><p>cq:Component へのパス（または拡張） <i>mobileapps/core/components/instance.</i></p> <p>これにより、アプリカタログに存在とレンダリングが提供されます。</p> </td>
  </tr>
 </tbody>
</table>

以下を使用できます。 ***コンテンツプロパティ*** コンテンツを作成します。 記事と共有リソースを作成および書き出すには、次のリソースを参照してください。

* [コンテンツプロパティ](/help/mobile/content-properties.md)
* [記事のエクスポート設定の作成](/help/mobile/creating-article-export-configuration.md)
* [共有リソースのエクスポート設定の作成](/help/mobile/creating-shared-resources-export-configuration.md)
