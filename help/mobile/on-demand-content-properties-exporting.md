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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 30%

---


# コンテンツのプロパティを使用したコンテンツの書き出し{#using-content-properties-to-export-content}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

Apps are represented as *cq:Pages* in AEM.

They share the same common properties found in any *cq:Page* in addition to others shown below that represent integration supporting properties.

## アプリのプロパティ {#app-properties}

The following table shows **App Properties and Nodes**.

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ名</strong></td>
   <td><strong>型</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>String:Path</td>
   <td><p>設定済みのMobile On-DemandCloud Serviceへのパス。 AEM MobileからMobile On-Demandへのアクション（API呼び出し）に使用</p> <p>この関連付けは、作成者がアプリを関連付けるMobile On-DemandCloud Serviceを選択した場合に、接続を管理タイルを介して設定されます。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>String:Path</td>
   <td><p>アプリのエクスポート設定のパス 書き出し設定は、2つの子ContentSync書き出し設定テンプレートを持つフォルダーです。</p> <p><i>dps-article</i>:記事のコンテンツを書き出すためのContentSync書き出し設定</p> <p><i>dps-HTMLResources</i>:アプリ/記事の共有リソースを書き出すためのContentSync書き出し設定</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>String</td>
   <td><p>このアプリがリンクまたは連結されるMobile On-DemandプロジェクトのID/URI。</p> <p>この関連付けは、関連付けられたMobile On-DemandCloud Serviceで使用可能なプロジェクトのリストから作成者がプロジェクトを選択した場合に、接続の管理タイルを介して設定されます。</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>String</td>
   <td>アプリのタイトル。</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>String</td>
   <td>コンテンツタイプ.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>日付</td>
   <td>共有リソースをAEMからAEM Mobileに最後にアップロードした日付。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:userid</td>
   <td>AEMからAEM Mobileへの共有リソース要求の最後のアップロードを実行したユーザーのID。</td>
  </tr>
  <tr>
   <td>page-ダッシュボード-config</td>
   <td>String:Path</td>
   <td>ダッシュボード設定へのパス。 パスは、必要に応じてカスタムのダッシュボード設定にリダイレクトできます。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>文字列:パス</td>
   <td><p>mobileapps/core/components/instanceを拡張または拡張するcq: <i>コンポーネントへのパス。</i></p> <p>これにより、アプリカタログでの配置とレンダリングが可能になります。</p> </td>
  </tr>
 </tbody>
</table>

You can use ***Content Properties*** to create content. 記事および共有リソースの作成と書き出しについては、以下のリソースを参照してください。

* [コンテンツのプロパティ](/help/mobile/content-properties.md)
* [記事の書き出し設定の作成](/help/mobile/creating-article-export-configuration.md)
* [共有リソースの書き出し設定の作成](/help/mobile/creating-shared-resources-export-configuration.md)
