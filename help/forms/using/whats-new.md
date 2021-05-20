---
title: 新機能の概要 | AEM 6.5 Forms
seo-title: 新機能の概要 | AEM 6.5 Forms
description: 世界で最も高度なデジタルエクスペリエンス管理ソリューションのフォームとドキュメントに対する最新の機能と改善点です。
seo-description: 世界で最も高度なデジタルエクスペリエンス管理ソリューションのフォームとドキュメントに対する最新の機能と改善点です。
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 16%

---

# 新機能の概要 | AEM 6.5 Forms{#new-features-summary-aem-forms}

## トランザクションレポート{#transaction-reports}

トランザクションレポートでは、送信されたフォーム、処理されたドキュメント、レンダリングされたドキュメントの数を取得し、トラッキングすることができます。 これらのトランザクションを追跡する目的は、製品の使用状況に関する十分な情報に基づく判断を下し、ハードウェアとソフトウェアに対する投資を再調整することです。 トランザクションの例を次に示します。

* アダプティブフォーム、HTML5フォーム、フォームセットの送信
* インタラクティブ通信の印刷またはWeb版のレンディション
* あるファイル形式から別のファイル形式へのドキュメントの変換

トランザクションレポートの設定と使用について詳しくは、[トランザクションレポートの概要](../../forms/using/transaction-reports-overview.md)を参照してください。

![サンプルトランザクションレポート](assets/surface_transaction_reporting.png)

## インタラクティブコミュニケーション {#interactive-communications}

**データの表示パターンの定義**

インタラクティブ通信の作成者は、フィールド、変数、フォームデータモデル要素の[データ表示パターン](create-interactive-communication.md#datadisplaypatterns)を定義できるようになりました。 例えば、日付、通貨、電話の形式などです。

**新しい種類のグラフを使用する**

複数の系列](../../forms/using/chart-component-interactive-communications.md)を持つ[QuadrantグラフとグラフをInteractive Communicationsに追加できるようになりました。

**テーブルの列の並べ替え**

インタラクティブ通信内のテーブル](../../forms/using/create-interactive-communication.md#sortcolumns)の列を[並べ替えることができるようになりました。 静的テキストまたはデータモデルオブジェクトを使用して、テーブルの列を連結および並べ替えることができます。

**Webチャネルでの新しいコンポーネントの使用**

Webチャネルにボタンコンポーネントと区切り文字コンポーネントを追加できるようになりました。 詳しくは、[Webチャネル](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel)にボタンコンポーネントを追加するおよび[Webチャネル](../../forms/using/create-interactive-communication.md#separatorcomponent)の区切り文字コンポーネントを参照してください。

**コンポーネントのサイズを変更するレイアウトモード**

WYSIWYGインターフェイスを使用して、[レイアウトモード](../../forms/using/resize-using-layout-mode.md)に切り替え、Webチャネル内のコンポーネントのサイズを変更できるようになりました。

**ユーザビリティの改善**

インタラクティブ通信の作成者は、通信の作成時に様々な使いやすい操作を利用できるようになりました。 操作のリストには、次のものが含まれます。

* [印刷チャネルとWebチャネルでの取り消し/やり直し操作の実行](../../forms/using/create-interactive-communication.md#undoredoactions)
* [@記号を使用してドキュメントフラグメントに変数を追加する](../../forms/using/texts-interactive-communications.md#searchvariables)
* [@記号を使用して、ドキュメントフラグメントにデータモデル要素を追加する](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [既存のインタラクティブ通信にWebチャネルを削除または追加する](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [ドラッグ&amp;ドロップ操作を使用したフィールドと変数へのデータソース要素の連結](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [インタラクティブ通信の作成中に、連結されていないフィールドと変数をハイライト表示する](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Webチャネル内の継承されたコンポーネントに対して、コピー、グループ化などの追加アクションを実行する](../../forms/using/create-interactive-communication.md#componenttoolbar)

**同期プロセスの改善**

印刷チャネルを使用して自動生成されるWebチャネルレイアウトには、いくつかの改善点があります。

![インタラクティブ通信チャート](assets/interactive-communication-charts.png)

## アダプティブフォーム {#adaptive-forms}

### アダプティブFormsでAdobe Signのクラウドベースのデジタル署名を使用する{#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[クラウドベースの電子署名（リモート署名）は、デスクトップ、モバイル、Web 上で機能する新世代のデジタル署名で、署名者の認証に関する最高レベルのコンプライアンスと保証を満たします。](https://helpx.adobe.com/jp/sign/kb/digital-certificate-providers.html)クラウドベースの電子署名を使用して、アダプティブフォーム](../../forms/using/working-with-adobe-sign.md)に[署名できるようになりました。

#### AEM Sitesのシングルページアプリケーションにアダプティブフォームまたはインタラクティブ通信を埋め込む{#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Formsでは、AEM Sitesのシングルページアプリケーション(SPA)にアダプティブフォーム](../../forms/using/embed-adaptive-form-aem-sites-spa.md)やインタラクティブ通信を[シームレスに埋め込むことができます。 埋め込まれたアダプティブフォームとインタラクティブ通信は完全に機能し、ユーザーはページを離れることなくフォームに入力して送信できます。 これにより、ユーザーはWebページ上の他の要素のコンテキストを維持し、アダプティブフォームやインタラクティブ通信と同時にやり取りすることができます。

#### アダプティブフォームテーブルの列の並べ替え{#sort-columns-of-adaptive-form-tables}

[アダプティブフォームの表の任意の列を昇順または降順に並べ替えることができます。](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) 静的テキスト、データモデルオブジェクトのプロパティ、または静的テキストとデータモデルオブジェクトのプロパティの組み合わせを含むテーブル列に並べ替えを適用できます。

#### アダプティブFormsテンプレートの使用可能なパスを特定のパスに制限する{#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

アダプティブフォームでは、cq:allowedPathsプロパティのサポートが追加されました。 プロパティ[は、アダプティブFormsテンプレートの使用を特定のパス](creating-adaptive-form.md#adaptive-form-templates)に制限します。

#### アダプティブフォームにチェックボックスを動的に追加する{#add-check-boxes-to-the-adaptive-form-dynamically}

カスタム関数、フォームオブジェクト、またはオブジェクトプロパティに基づいて、[アダプティブフォームにチェックボックスを動的に追加するルールを定義できるようになりました。](../../forms/using/rule-editor.md#setpropertyrule)

## AEM ワークフロー {#aem-workflows}

### AEMワークフローでの変数の使用{#use-variables-in-aem-workflows}

変数を使用すると、ワークフローステップで、実行時にワークフローステップ間でメタデータを保持して渡すことができます。 様々なタイプの変数を作成して、様々なタイプのデータを保存できます。例えば、整数、文字列、ドキュメント、フォームデータモデルインスタンスなどです。 一般に、変数または変数のコレクションを使用するのは、変数が保持する値に基づいて決定する必要がある場合、またはプロセスで後で必要になる情報を保存する場合です。

変数は、以前のバージョンで使用可能な[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html?lang=ja)インターフェイスの拡張です。 メタデータ値の取得と更新に使用するカスタムECMAScriptコードの開発に費やす時間を節約できます。 引き続きMetaDataMapインターフェイスとECMAScriptコードを使用して、メタデータを操作します。 MetaDataMapやECMAScriptよりも変数を使用する利点は次のとおりです。

* カスタムコードに依存せずに、ワークフロー全体で変数に格納された値を動的に保存、更新、使用する
* 送信されたフォームのフォームデータモデルとデータファイル(XML/JSON )に値を直接取得して更新する
* ドキュメント処理を実行するために、変数に完全なドキュメントを格納する

移動ステップ（OR分割ステップ）と、すべてのAEM Formsワークフローステップは変数をサポートします。 MetaDataMapインターフェイスを使用して、変数をネイティブでサポートしていないワークフローステップの変数にアクセスできます。 詳しくは、「AEMワークフローの変数[」を参照してください。](../../forms/using/variable-in-aem-workflows.md)

![ワークフローのの変数の設定](assets/variable.png)

#### 別のアダプティブFormsでのワークフローの使用{#use-a-workflow-with-different-adaptive-forms}

[タスクの割り当て](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step)と、ランタイム上のフォーム中心のワークフローのレコードのドキュメントステップに対して、アダプティブフォームを指定できます。 これにより、ワークフローが異なるアダプティブFormsで動作するようになります。 ワークフローのデザイン中に、アダプティブフォームを選択する方法を決定することができます。 アダプティブフォームは、絶対パスに配置したり、ワークフローにペイロードとして送信したり、変数を使用して計算されたパスに配置したりできます。

#### フォーム中心のワークフローステップの拡張ログ機能を使用する{#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

フォーム中心のワークフローステップのログ機能は標準化されています。 現在は、フォーム中心のすべてのワークフローステップで、同様に標準化されたログが生成されます。 これは、デバッグ速度の向上に役立ちます。

## データ統合 {#data-integration}

次の操作が可能になっています。

* [制約のリスト](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) に基づいて入力データベースを検証します。有効なデータのみがデータソースに送信されるようにします。
* [WSDL (Web Services Description Language)フ](../../forms/using/configure-data-sources.md#configure-soap-web-services) ァイルで定義されたデフォルトのエンドポイントを上書きします。

* [Swagger定義](../../forms/using/configure-data-sources.md#configure-restful-web-services) [ファイルで定義されたdefaultscheme、host、お](../../forms/using/configure-data-sources.md#configure-restful-web-services) よびbaseパスを上書きします。

## プラットフォームとセキュリティの更新{#platform-and-security-updates}

### 主なプラットフォーム更新{#major-platform-updates}

サポート対象のオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK サーバー、LDAP サーバー、電子メールサーバーを自由に組み合わせて、AEM Forms をセットアップすることができます。次に、[サポートされるプラットフォーム](../../forms/using/aem-forms-jee-supported-platforms.md)の主な変更点を示します。

<table>
 <tbody>
  <tr>
   <td>コンポーネント</td>
   <td>サポート対象から除外</td>
  </tr>
  <tr>
   <td>オペレーティングシステム</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>アプリケーションサーバー<br /> </td>
   <td>
    <ul>
    <li>WebSphere Libertyプロファイル</li>
    <li>Oracle WebLogic ／</li>
    </ul> </td>
  </tr>
  <tr>
   <td>データベース</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>OracleRAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP サーバー</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>電子メールサーバー</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>コネクタ</td>
   <td>
    <ul>
     <li>Connector for Microsoft Sharepoint 2013</li>
     <li>Connector for EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms アプリケーション<br /> </td>
   <td>
    <ul>
     <li>Windows 8.1のサポート</li>
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

*別のプラットフォームへの移行に関する情報については、Adobeサポートにお問い合わせください。

#### 新しいHTML5ベースのUI {#new-html-based-uis}

AdobeFlash Playerの計画的なEOLと、Flashベースのコンテンツをオープン標準に移行する全体的な方向性に合わせて、AEM 6.5 Formsは、JEE上のAEM FormsのFlashベースのUI、Process Management、Reader拡張、およびカテゴリ管理UIのHTML5ベースのUIに置き換えました。

#### セキュリティの強化{#security-improvements}

* JEE上のAEM 6.5 Forms管理コンソールのUIが、Apache Struts 2.5に基づいています。
* AEM 6.5 Formsでは、jQueryを3.2.1およびjQuery UI 1.12.1に使用するようになりました。変更の影響については、[アップグレードに関するドキュメント](/help/forms/home.md)を参照してください。

#### アクセシビリティの改善{#accessibility-improvements}

AEM 6.5 FormsのAEM Forms Workspaceのアクセシビリティが向上しました。
