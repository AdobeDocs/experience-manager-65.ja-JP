---
title: コンテンツのプロパティを使用したコンテンツの書き出し
seo-title: コンテンツのプロパティを使用したコンテンツの書き出し
description: 以下のページでは、アプリのプロパティとノードについて説明します。
seo-description: 以下のページでは、アプリのプロパティとノードについて説明します。
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 30%

---

# コンテンツのプロパティを使用したコンテンツの書き出し{#using-content-properties-to-export-content}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

アプリは、AEMでは&#x200B;*cq:Pages*&#x200B;と表されます。

これらは、*cq:Page*&#x200B;で見つかる共通のプロパティと、以下に示す統合をサポートするプロパティを表す共通のプロパティを共有します。

## アプリのプロパティ {#app-properties}

次の表に、**アプリのプロパティとノード**&#x200B;を示します。

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
   <td><p>設定済みのMobile On-DemandCloud Serviceへのパス。 AEM MobileからMobile On-Demandへのアクション（API呼び出し）に使用</p> <p>この関連付けは、作成者がアプリの関連付け先となるMobile On-DemandCloud Serviceを選択すると、接続を管理タイルで設定されます。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>String:Path</td>
   <td><p>アプリの書き出し設定のパス。 書き出し設定は、2つの子ContentSync書き出し設定テンプレートを持つフォルダーです。</p> <p><i>dps-article</i>:記事のコンテンツを書き出すためのContentSync書き出し設定</p> <p><i>dps-HTMLResources</i>:アプリ/記事の共有リソースを書き出すためのコンテンツ同期書き出し設定</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>文字列</td>
   <td><p>このアプリがリンク/バインドされるMobile On-DemandプロジェクトのID/URI。</p> <p>この関連付けは、作成者が関連するMobile On-DemandCloud Serviceで使用可能なプロジェクトのリストからプロジェクトを選択すると、接続を管理タイルで設定されます。</p> </td>
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
   <td>AEMからAEM Mobileへの共有リソースリクエストの最後のアップロードを実行したユーザーのID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>String:Path</td>
   <td>ダッシュボード設定へのパス。 パスは、必要に応じてカスタムのダッシュボード設定にリダイレクトできます。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>文字列:パス</td>
   <td><p><i>mobileapps/core/components/instance.</i>を拡張または拡張するcq:Componentへのパス。</p> <p>これにより、アプリカタログに表示とレンダリングが提供されます。</p> </td>
  </tr>
 </tbody>
</table>

***コンテンツのプロパティ***&#x200B;を使用して、コンテンツを作成できます。 記事および共有リソースの作成と書き出しについては、以下のリソースを参照してください。

* [コンテンツのプロパティ](/help/mobile/content-properties.md)
* [記事の書き出し設定の作成](/help/mobile/creating-article-export-configuration.md)
* [共有リソースの書き出し設定の作成](/help/mobile/creating-shared-resources-export-configuration.md)
