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
translation-type: tm+mt
source-git-commit: a417094c1d7b28ec54a6e84303d7a9747bb0c510
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 11%

---


# 新機能の概要 | AEM 6.5 Forms{#new-features-summary-aem-forms}

## トランザクションレポート{#transaction-reports}

トランザクションレポートでは、送信されたフォーム、処理されたドキュメント、レンダリングされたドキュメントの数を取得し、追跡できます。 これらのトランザクションをトラッキングする目的は、製品の使用とハードウェアおよびソフトウェアに対する投資のリバランスに関する十分な情報に基づく判断を行うことです。 トランザクションの例を次に示します。

* アダプティブフォーム、HTML5フォーム、またはフォームセットの送信
* インタラクティブな通信の印刷またはWeb版のレンディション
* あるファイル形式から別のファイル形式へのドキュメントの変換

トランザクションレポートの設定と使用について詳しくは、[トランザクションレポートの概要](../../forms/using/transaction-reports-overview.md)を参照してください。

![サンプルトランザクションレポート](assets/surface_transaction_reporting.png)

## インタラクティブコミュニケーション {#interactive-communications}

**データ表示パターンの定義**

対話型通信の作成者は、フィールド、変数、フォームデータモデル要素に対して[データ表示パターン](create-interactive-communication.md#datadisplaypatterns)を定義できるようになりました。 例えば、日付、通貨、電話の形式などです。

**新しいタイプのグラフの使用**

複数のシリーズ](../../forms/using/chart-component-interactive-communications.md)を含む[クアドラントグラフとグラフをInteractive Communicationsに追加できるようになりました。

**テーブルの列の並べ替え**

対話型通信で、テーブル](../../forms/using/create-interactive-communication.md#sortcolumns)の列を[並べ替えることができるようになりました。 スタティックテキストオブジェクトやデータモデルオブジェクトを使用して、テーブルの列を連結したり、並べ替えたりできます。

**Webチャネルーでの新しいコンポーネントの使用**

Webチャネルーにボタンコンポーネントとセパレーターコンポーネントを追加できるようになりました。 詳しくは、Webチャネル](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel)の[追加ボタンコンポーネントおよびWebチャネル](../../forms/using/create-interactive-communication.md#separatorcomponent)の[セパレータコンポーネントを参照してください。

**コンポーネントのサイズを変更するレイアウトモード**

WYSIWYGインターフェイスを使用して、Webチャネルーのコンポーネントのサイズを変更する場合に、[レイアウトモード](../../forms/using/resize-using-layout-mode.md)に切り替えることができるようになりました。

**操作性の向上**

インタラクティブコミュニケーションの作成者は、通信の作成時に様々な使いやすい操作を利用できるようになりました。 操作のリストには、次のものがあります。

* [印刷およびWebチャネルで元に戻す/やり直し操作を実行する](../../forms/using/create-interactive-communication.md#undoredoactions)
* [@追加記号を使用したドキュメントフラグメント内の変数](../../forms/using/texts-interactive-communications.md#searchvariables)
* [@追加記号を使用したドキュメントフラグメント内のデータモデル要素](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [既存のInteractive Communicationに対するWebチャネルの削除または追加](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [ドラッグ&amp;ドロップ操作によるデータソース要素とフィールドおよび変数の連結](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [インタラクティブ通信の作成中に、連結されていないフィールドと変数を強調表示する](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Webチャネルー内の継承されたコンポーネントに対して、コピー、グループなどの追加操作を実行します](../../forms/using/create-interactive-communication.md#componenttoolbar)

**同期プロセスの改善点**

印刷チャネルを使用して自動生成されるWebチャネルレイアウトには、いくつかの改善点があります。

![対話型通信グラフ](assets/interactive-communication-charts.png)

## アダプティブフォーム {#adaptive-forms}

### アダプティブFormsでAdobe Signのクラウドベースのデジタル署名を使用{#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[クラウドベースのデジタル](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 署名またはリモート署名は、デスクトップ、モバイル、Web上で機能する新しい世代のデジタル署名で、署名者の認証に関する最高レベルのコンプライアンスと保証を満たします。Cloudベースの電子署名を使用して、アダプティブフォーム](../../forms/using/working-with-adobe-sign.md)に[署名できるようになりました。

#### AEM Sitesのシングルページアプリにアダプティブフォームやインタラクティブなコミュニケーションを埋め込む{#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Formsでは、AEM Sitesのシングルページアプリ(SPA)に[アダプティブフォーム](../../forms/using/embed-adaptive-form-aem-sites-spa.md)やインタラクティブコミュニケーションをシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームとインタラクティブ通信は完全に機能し、ユーザーはページを離れることなくフォームに入力して送信できます。 Webページ上の他の要素のコンテキストを維持し、アダプティブフォームやインタラクティブコミュニケーションと同時にやり取りするのに役立ちます。

#### アダプティブフォームテーブルの列の並べ替え{#sort-columns-of-adaptive-form-tables}

[アダプティブフォームのテーブル](../../forms/using/adaptive-forms-tables.md#sortcolumnstable)の列は、昇順または降順で並べ替えることができます。 静的テキストを含むテーブル列、データモデルオブジェクトプロパティ、または静的テキストとデータモデルオブジェクトプロパティの組み合わせに対して、並べ替えを適用できます。

#### アダプティブFormsテンプレートの可用性を特定のパス{#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}に制限

アダプティブフォームでは、cq:allowedPathsプロパティのサポートが追加されました。 [プロパティは、アダプティブFormsテンプレートの使用を特定のパス](creating-adaptive-form.md#adaptive-form-templates)に制限します。

#### アダプティブフォーム追加のチェックボックスがダイナミックに{#add-check-boxes-to-the-adaptive-form-dynamically}

カスタム関数、フォームオブジェクト、またはオブジェクトプロパティに基づいて、[アダプティブフォームにチェックボックスを動的に](../../forms/using/rule-editor.md#setpropertyrule)追加するためのルールを定義できるようになりました。

## AEM ワークフロー {#aem-workflows}

### AEMワークフローで変数を使用{#use-variables-in-aem-workflows}

変数を使用すると、ワークフローステップで、実行時にワークフローステップ間でメタデータを保持および渡すことができます。 様々なタイプの変数を作成して、様々なタイプのデータを保存できます。例えば、整数、文字列、ドキュメント、フォームデータモデルのインスタンスなどです。 一般に、変数または変数のコレクションを使用するのは、変数が保持する値に基づいて決定する必要がある場合、またはプロセスで後で必要になる情報を保存する場合です。

変数は、以前のバージョンで使用可能な[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)インターフェイスの拡張です。 メタデータ値の取得と更新に使用するカスタムECMAScriptコードの開発に費やす時間を節約できます。 MetaDataMapインターフェイスとECMAScriptコードを使用して、メタデータを操作し続けます。 MetaDataMapおよびECMAScriptで変数を使用するメリットは次のとおりです。

* カスタムコードに依存せずに、ワークフロー全体で変数に格納された値を動的に保存、更新、使用
* 送信されたフォームのフォームデータモデルとデータファイル(XML/JSON)に直接値を取得して更新する
* ドキュメント処理を実行するために、完全なドキュメントを変数に格納する

「移動先」、「分割」の各ステップと、すべてのAEM Formsワークフローステップで、変数がサポートされています。 MetaDataMapインターフェイスを使用して、変数をネイティブでサポートしていないワークフロー手順の変数にアクセスできます。 詳しくは、[AEMワークフローの変数](../../forms/using/variable-in-aem-workflows.md)を参照してください。

![ワークフロー内での変数の設定](assets/variable.png)

#### 別のアダプティブFormsでワークフローを使用する{#use-a-workflow-with-different-adaptive-forms}

割り当てタスク](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step)に対するアダプティブフォームを[指定し、ランタイム上でフォーム中心のワークフローのレコードステップのドキュメントを指定できます。 これにより、異なるアダプティブFormsでワークフローを機能させることができます。 ワークフローのデザイン中に、アダプティブフォームを選択する方法を決定できます。 アダプティブフォームは、絶対パスに配置したり、ワークフローへのペイロードとして送信したり、変数を使用して計算されたパスに配置したりできます。

#### フォーム中心のワークフロー手順{#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}の強化されたログ機能を使用する

フォーム中心のワークフローステップのログ機能は標準化されています。 現在は、フォーム中心のすべてのワークフローステップで、同様に標準化されたログが生成されます。 これはデバッグ速度の向上に役立ちます。

## データ統合 {#data-integration}

次の操作が可能になっています。

* [制約のリストに基づいて入力](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) データベースを検証します。有効なデータのみがデータソースに送信されることを確認するのに役立ちます。
* [WSDL(Web Services Description Language)ファイルで定義されたデフォルトの](../../forms/using/configure-data-sources.md#configure-soap-web-services) エンドポイントを上書きします。

* [Swagger定義ファイルで定義されている](../../forms/using/configure-data-sources.md#configure-restful-web-services) [defaultscheme、host、およびbase](../../forms/using/configure-data-sources.md#configure-restful-web-services) パスを上書きします。

## プラットフォームとセキュリティの更新{#platform-and-security-updates}

### 主なプラットフォームの更新{#major-platform-updates}

サポート対象のオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK サーバー、LDAP サーバー、電子メールサーバーを自由に組み合わせて、AEM Forms をセットアップすることができます。[サポートされるプラットフォーム](../../forms/using/aem-forms-jee-supported-platforms.md)の主な変更点は次のとおりです。

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
     <li>Oracle大統領</li>
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

*別のプラットフォームへの移行については、Adobeサポートにお問い合わせください。

#### 新しいHTML5ベースのUI {#new-html-based-uis}

AdobeFlash Playerに関する計画的なEOLとFlashベースのコンテンツをオープンスタンダードに移行する全体的な方向に沿って、AEM 6.5Formsは、JEE Administration Console上のHealth Monitor、Process Management、Reader拡張、カテゴリ管理UIのFlashベースのUIをHTML5ベースのUIに置き換えました。

#### セキュリティの強化{#security-improvements}

* JEE上のAEM 6.5Forms管理コンソールUIがApache Struts 2.5に基づくようになりました。
* AEM 6.5Formsでは、jQueryを3.2.1、jQuery UI 1.12.1に使用するようになりました。変更の影響については、[アップグレードドキュメント](/help/forms/home.md)を参照してください。

#### アクセシビリティの向上{#accessibility-improvements}

AEM 6.5Formsでは、AEM Formsワークスペースのアクセシビリティが向上しました。
