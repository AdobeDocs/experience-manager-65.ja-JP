---
title: コンテンツのプロパティを使用したコンテンツのエクスポート
description: 次のページは、アプリのプロパティとノードを示しています。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 15%

---

# コンテンツのプロパティを使用したコンテンツのエクスポート{#using-content-properties-to-export-content}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

アプリは次のように表されます *cq:Pages* をAEMで行います。

共通のプロパティは次のとおりです *cq:Page* 統合をサポートするプロパティを表す以下のプロパティに加えて、

## アプリのプロパティ {#app-properties}

次の表に示します **アプリのプロパティとノード**.

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
   <td><p>設定済みのモバイルオンデマンドCloud Serviceーへのパス。 AEM Mobileから Mobile オンデマンドアクションへの変換（API 呼び出し）に使用</p> <p>この関連付けは、作成者がアプリを関連付けるモバイルオンデマンドCloud Serviceを選択したときに、接続を管理タイルで設定されます。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>String:Path</td>
   <td><p>アプリの書き出し設定のパス。 エクスポート設定は、2 つの子 ContentSync エクスポート設定テンプレートを含むフォルダーです。</p> <p><i>dps-article</i>：記事のコンテンツをエクスポートするための ContentSync エクスポート設定</p> <p><i>dps-HTMLResources</i>：アプリ/記事の共有リソースをエクスポートするための ContentSync エクスポート設定</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>文字列</td>
   <td><p>このアプリがリンク/バインドされている Mobile On-Demand プロジェクトの ID/URI。</p> <p>この関連付けは、作成者が関連するモバイルオンデマンドCloud Serviceで使用可能なプロジェクトのリストからプロジェクトを選択すると、「接続を管理」タイルで設定されます。</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>文字列</td>
   <td>アプリのタイトル。</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>文字列</td>
   <td>コンテンツタイプ。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>日付</td>
   <td>AEMからAEM Mobileへの共有リソースの最終アップロード日。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:userid</td>
   <td>AEMからAEM Mobileへの共有リソースリクエストの最後のアップロードを実行したユーザーの ID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>String:Path</td>
   <td>ダッシュボード設定のパス。 必要に応じて、パスをカスタムダッシュボード設定にリダイレクトできます。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>String:Path</td>
   <td><p>または拡張される cq:Component へのパス <i>mobileapps/core/components/instance です。</i></p> <p>これにより、アプリカタログにプレゼンスとレンダリングが提供されます。</p> </td>
  </tr>
 </tbody>
</table>

次を使用できます ***コンテンツのプロパティ*** コンテンツを作成します。 記事および共有リソースの作成と書き出しについては、次のリソースを参照してください。

* [コンテンツのプロパティ](/help/mobile/content-properties.md)
* [記事のエクスポート設定の作成](/help/mobile/creating-article-export-configuration.md)
* [共有リソースのエクスポート設定の作成](/help/mobile/creating-shared-resources-export-configuration.md)
