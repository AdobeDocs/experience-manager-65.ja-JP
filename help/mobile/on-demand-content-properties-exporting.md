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
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 10%

---

# コンテンツのプロパティを使用したコンテンツのエクスポート{#using-content-properties-to-export-content}

{{ue-over-mobile}}

アプリは、AEMでは *cq:Pages* として表されます。

これらは、以下に示す統合サポートプロパティを表す他のプロパティに加えて、任意の *cq:Page* で見つかるのと同じ共通プロパティを共有します。

## アプリのプロパティ {#app-properties}

次の表に、**アプリのプロパティとノード** を示します。

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
   <td><p>アプリの書き出し設定のパス。 エクスポート設定は、2 つの子 ContentSync エクスポート設定テンプレートを含むフォルダーです。</p> <p><i>dps-article</i>：記事のコンテンツをエクスポートする ContentSync エクスポート設定</p> <p><i>dps-HTMLResources</i>：アプリ/記事の共有リソースを書き出すための ContentSync 書き出し設定</p> </td>
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
   <td><p><i>mobileapps/core/components/instance.</i> である、または拡張する cq:Component のパス</p> <p>これにより、アプリカタログにプレゼンスとレンダリングが提供されます。</p> </td>
  </tr>
 </tbody>
</table>

***コンテンツのプロパティ*** を使用してコンテンツを作成できます。 記事および共有リソースの作成と書き出しについては、次のリソースを参照してください。

* [コンテンツのプロパティ](/help/mobile/content-properties.md)
* [記事のエクスポート設定の作成](/help/mobile/creating-article-export-configuration.md)
* [共有リソースのエクスポート設定の作成](/help/mobile/creating-shared-resources-export-configuration.md)
