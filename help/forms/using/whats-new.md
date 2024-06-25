---
title: 新機能の概要 | AEM 6.5 Forms
description: 世界で最も高度なデジタルエクスペリエンス管理ソリューションの AEM Forms とドキュメントに対する最新の機能と改善点です。
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
solution: Experience Manager, Experience Manager Forms
feature: Release Information
role: Admin, User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: ht
source-wordcount: '637'
ht-degree: 100%

---

# 新機能の概要 | AEM 6.5 Forms{#new-features-summary-aem-forms}

| 製品 | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.19.0 |
| タイプ | サービスパックのリリース |
| 日付 | 2023年12月8日金曜日（PT） |

## Adobe Experience Manager 6.5 Forms サービスパック 19（6.5.19.0）の内容

Experience Manager 6.5.19.0 には、2019年4月の 6.5 の初公開以降にリリースされた新しい機能、お客様から要望のあった主な機能強化、バグ修正およびパフォーマンスや安定性、セキュリティの向上が含まれています。Experience Manager 6.5 で[このサービスパックをインストール](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=ja)します。

### 新機能

#### 新しいアダプティブフォームコアコンポーネント

垂直タブ、利用条件、チェックボックスが追加され、フォームのスケーラビリティが向上します。

* **[チェックボックスコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html?lang=ja)**：コアコンポーネントに基づくアダプティブフォームに、チェックボックスコンポーネントを含めることができるようになりました。これにより、ユーザーは特定のオプションを選択または選択解除する二者択一の選択を行うことができます。通常、小さなボックスとして表示され、クリックまたはタップすると、オンとオフの 2 つの状態を切り替えることができます。チェックボックスは、はい／いいえ、または真／偽の選択肢を提示するために使用される一般的なフォーム要素です。

* **[利用条件コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html?lang=ja)**：コアコンポーネントに基づくアダプティブフォームに利用条件コンポーネントを含めることができるようになりました。これにより、フォーム作成者は、サービス、製品、プラットフォームの使用に関連する利用条件または法的合意をユーザーに提示するフォーム内に特定のセクションを導入できます。このコンポーネントは、フォームを送信することで同意するルール、規制、義務についてユーザーに通知するように設計されています。

  ![垂直タブ、利用条件およびチェックボックスコンポーネント](/help/forms/using/assets/forms-components.png)

* **[垂直タブコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html?lang=ja)**：コアコンポーネントに基づくアダプティブフォームでは、フォームのコンテンツをタブの垂直リストに整理し、構造化されたナビゲートしやすいレイアウトを提供できるようになりました。フォームで垂直タブを使用すると、特にフォームに複数のセクションや複雑な情報が含まれている場合、ナビゲーションが簡素化され、フォームコンテンツの整理が改善され、全体的なユーザーエクスペリエンスが向上します。

#### 64 ビット版の AEM Forms Designer

[64 ビット版の AEM Forms Designer](/help/forms/using/installing-configuring-designer.md) では、パフォーマンス、スケーラビリティ、メモリ管理が強化され、フォーム作成エクスペリエンスを支援します。64 ビットアーキテクチャを使用すると、さらに大規模で複雑なプロジェクトに簡単に取り組むことができ、シームレスな設計ワークフローと最適化された効率が保証されます。この最先端のリリースでフォームデザイン機能を強化し、AEM Forms Designer の未来を体現します。

#### アダプティブフォームと Microsoft® SharePoint リストの接続

AEM Forms では、[フォームデータを SharePoint リストに直接送信](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)する標準の統合を提供し、SharePoint のリスト機能を使用できます。Microsoft® SharePoint リストをフォームデータモデルのデータソースとして設定し、「フォームデータモデルを使用して送信」送信アクションを使用して、アダプティブフォームを SharePoint リストに接続できます。

#### アダプティブフォームフラグメントのレコードのドキュメントプロパティの設定のサポート

[アダプティブフォームエディターでアダプティブフォームフラグメントとそのフィールドを簡単にカスタマイズ](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)できるようになりました。

#### 64 ビット版の XMLFM を含む

64 ビット反復の XMLFM により、パフォーマンス、スケーラビリティ、洗練されたメモリ管理が導入されます。これは、サーバーサイドにデプロイされた最初の 64 ビットネイティブサービスです。XMLFM 64 ビットでは、32 ビット版と比較して大幅により大きなメモリリソースにアクセスする固有の機能を利用することで、より大きなレンダリングワークロードをシームレスに処理できます。このマイルストーンは、パフォーマンスの飛躍的な向上を示すだけでなく、AEM Forms サーバー内のネイティブサービスフレームワークに重要な機能強化も導入します。この更新により、AEM Forms サーバーでは 64 ビットのネイティブサービスをシームレスにサポートできます。



## バグの修正

このリリースには、お客様から報告された 20 件以上の問題の修正も含まれています。サービスパックに含まれる修正のリストについて詳しくは、[リリースノート](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=ja#forms-6519)を参照してください


## サービスパックのインストール

このサービスパックには、JEE 上の AEM Forms と OSGi 上の AEM Forms の両方に新機能とバグ修正が含まれます。インストール手順は、以前のサービスパックと比較して変更されます。インストール手順について詳しくは、[AEM Forms サービスパックのインストール手順](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=ja)を参照してください。






<!-- 
## Transaction Reports {#transaction-reports}



Transaction reports lets you capture and track the number of submitted forms, processed documents, and rendered documents. The objective behind tracking these transactions is to make an informed decision about the product usage and rebalancing investments in hardware and software. Some examples of transactions include:

* Submission of an Adaptive Form, an HTML5 Form, or a Form Set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For information about configuring and using transaction reports, see [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md).

![A sample transaction report](assets/surface_transaction_reporting.png)

## Interactive Communications {#interactive-communications}

**Define data display patterns**

Interactive Communication authors can now define [data display patterns](create-interactive-communication.md#datadisplaypatterns) for fields, variables, and form data model elements. For example, date, currency, or phone formats.

**Use new types of charts**

You can now add [Quadrant charts and charts with multiple series](../../forms/using/chart-component-interactive-communications.md) to Interactive Communications.

**Sort columns in a table**

You can now [sort columns of a table](../../forms/using/create-interactive-communication.md#sortcolumns) in the Interactive Communication. You can bind and sort table columns with static text or data model objects.

**Use new components in a web channel**

You can now add Button and Separator components to the web channel. For more information, see [Add Button component to the web channel](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) and [Separator component in web channel](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Layout mode to resize components**

You can now switch to [Layout mode](../../forms/using/resize-using-layout-mode.md) to resize components in the Web channel using a WYSIWYG interface.

**Usability improvements**

Interactive Communication authors can now utilize various easy-to-use operations while creating correspondences. The list of operations includes:

* [Perform undo-redo actions in print and web channels](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Add variables in a document fragment using @ symbol](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Add data model elements in a document fragment using @ symbol](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Delete or add a web channel to an existing Interactive Communication](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Bind data source elements with fields and variables using drag-and-drop actions](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Highlight unbound fields and variables while authoring Interactive Communication](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Perform additional actions such as copy, group, or more on inherited components in a web channel](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Improvements in sync process**

There are several improvements in the Web channel layout auto-generated using the Print channel.

![Interactive Communications Charts](assets/interactive-communication-charts.png)

## Adaptive Forms {#adaptive-forms}

### Use Adobe Sign's cloud-based digital signatures in Adaptive Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Cloud-based digital signatures](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) or remote signatures are a new generation of digital signatures that work across desktop, mobile, and the web — and meet the highest levels of compliance and assurance for signer authentication. You can now [sign an Adaptive Form](../../forms/using/working-with-adobe-sign.md) with Cloud-based digital signatures.

#### Embed an Adaptive Form or Interactive Communication in AEM Sites Single Page Applications {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms lets you [seamlessly embed an Adaptive Form](../../forms/using/embed-adaptive-form-aem-sites-spa.md) or Interactive Communication in an AEM Sites single page application (SPA). The embedded Adaptive Form and Interactive Communication is fully functional and users can fill and submit the form without leaving the page. It helps user remain in context of other elements on the web page and simultaneously interact with the adaptive form or Interactive Communication.

#### Sort columns of Adaptive Form tables {#sort-columns-of-adaptive-form-tables}

You can [sort any column of an Adaptive Form table](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) in an ascending or descending order. You can apply sorting to table columns with static text, data model object properties, or a combination of static text and data model object properties.

#### Restrict the availability of Adaptive Forms templates to specific paths {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Adaptive forms has added support for the cq:allowedPaths property. The property [restricts availability of Adaptive Forms templates to specific paths](creating-adaptive-form.md#adaptive-form-templates).

#### Add check boxes to the Adaptive Form dynamically {#add-check-boxes-to-the-adaptive-form-dynamically}

You can now define rules to [add checkboxes to the Adaptive Form dynamically](../../forms/using/rule-editor.md#setpropertyrule) based on custom function, a form object, or an object property.

## AEM Workflows {#aem-workflows}

### Use variables in AEM Workflows {#use-variables-in-aem-workflows}

Variables enable workflow steps to hold and pass metadata across workflow steps at runtime. You can create different types of variables for storing different types of data. For example, integers, strings, documents, or form data model instances. Typically, you use a variable or a collection of variables when you need to make a decision based on the value that it holds or to store information that you need later in a process.

Variables are an extension of [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) interface available in the previous version. It helps save time spent in developing custom ECMAScript code used to retrieve and update metadata values. You continue using MetaDataMap interface and ECMAScript code to manipulate metadata. Some benefits of using variables over MetaDataMap and ECMAScript are:

* Dynamically store, update, and use values stored in a variable across the workflow without relying on custom code
* Retrieve and update values directly to a form data model and data file (XML/JSON ) of a submitted form
* Store complete documents in a variable to perform document processing

The Go To step, OR Split step, and all AEM Forms workflow steps support variables. You can use MetaDataMap interface to access variables in workflow steps that do not have a native support for variables. For more information, see [Variables in AEM Workflows](../../forms/using/variable-in-aem-workflows.md).

![Setting a variable for in a workflow](assets/variable.png)

#### Use a workflow with different Adaptive Forms  {#use-a-workflow-with-different-adaptive-forms}

You can [specify an Adaptive Form for the assign task](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) and document of record step of form-centric workflows on the runtime. It allows a workflow to work with different Adaptive Forms. You can decide the method to select an Adaptive Form while designing the workflow. The Adaptive Form can be located at an absolute path, submitted as payload to the workflow, or available at a path calculated using a variable.

#### Use enhanced logging capabilities of forms-centric workflow steps {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Logging capabilities of forms-centric workflow steps are standardized. Now, all form-centric workflow steps produce similarly standardized logs. It helps improve debugging speed.

## Data Integration {#data-integration}

You can now:

* [Validate input data](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) based on a list of constraints. It helps ensure that only valid data is submitted to data source.
* [Override default endpoint](../../forms/using/configure-data-sources.md#configure-soap-web-services) defined in a WSDL (Web Services Description Language) file.

* [Override default](../../forms/using/configure-data-sources.md#configure-restful-web-services) [scheme, host, and base path](../../forms/using/configure-data-sources.md#configure-restful-web-services) defined in Swagger definition file.

## Platform and Security updates {#platform-and-security-updates}

### Major platform updates {#major-platform-updates}

AEM Forms can be set up using any combination of supported operating systems, application servers, databases, database drivers, JDK, LDAP servers, and email servers. The following are the major changes in [supported platforms](../../forms/using/aem-forms-jee-supported-platforms.md):

<table>
 <tbody>
  <tr>
   <td>Component</td>
   <td>Support Removed</td>
  </tr>
  <tr>
   <td>Operating systems</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Application servers<br /> </td>
   <td>
    <ul>
    <li>WebSphere Liberty profile</li>
    <li>Oracle WebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Databases</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP servers</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Email servers</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Connectors</td>
   <td>
    <ul>
     <li>Connector for Microsoft Sharepoint 2013</li>
     <li>Connector for EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms app<br /> </td>
   <td>
    <ul>
     <li>Windows 8.1 support</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

&#42; Contact Adobe Support for information on migrating to a different platform

#### New HTML5-based UIs {#new-html-based-uis}

In line with planned EOL of Adobe Flash Player and overall direction of migrating Flash-based content to open standards, AEM 6.5 Forms has replaced Flash-based UI of Health Monitor, Process Management, Reader Extension, and Category Management UI of AEM Forms on JEE Administration Console with HTML5-based UI.

#### Security improvements {#security-improvements}

* AEM 6.5 Forms on JEE administration console UI is now based on Apache Struts 2.5.
* AEM 6.5 Forms now uses jQuery to 3.2.1 and jQuery UI 1.12.1. See, [upgrade documentation](/help/forms/using/introduction-aem-forms.md) for the impact of the change.

#### Accessibility improvements {#accessibility-improvements}

AEM 6.5 Forms has improved accessibility of AEM Forms Workspace. 
!-->

