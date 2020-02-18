---
title: 新機能の概要 | AEM 6.5 Forms
seo-title: 新機能の概要 | AEM 6.5 Forms
description: 世界で最も高度なデジタルエクスペリエンス管理ソリューションのフォームとドキュメントに対する最新の機能と改善。
seo-description: 世界で最も高度なデジタルエクスペリエンス管理ソリューションのフォームとドキュメントに対する最新の機能と改善。
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
translation-type: tm+mt
source-git-commit: eb6ecc224c4fdd8c1af6f7800dc30de419f5ef68

---


# 新機能の概要 | AEM 6.5 Forms{#new-features-summary-aem-forms}

## トランザクションレポート {#transaction-reports}

トランザクションレポートでは、送信されたフォーム、処理されたドキュメント、およびレンダリングされたドキュメントの数を取得し、追跡できます。 これらのトランザクションをトラッキングする目的は、製品の使用状況に関する十分な情報を得た上で判断し、ハードウェアとソフトウェアに対する投資の再バランシングを行うことです。 トランザクションの例を次に示します。

* アダプティブフォーム、HTML5フォーム、またはフォームセットの送信
* インタラクティブ通信の印刷またはWebバージョンのレンディション
* あるファイル形式から別のファイル形式へのドキュメントの変換

トランザクションレポートの設定と使用に関する詳細は、「トランザクションレポ [ートの概要」を参照してくださ](../../forms/using/transaction-reports-overview.md)い。

![サンプルトランザクションレポート](assets/surface_transaction_reporting.png)

## インタラクティブコミュニケーション {#interactive-communications}

**データ表示パターンの定義**

Interactive Communicationの作成者は、フィールド、変数 [、およびフォームデータ](../../forms/using/create-interactive-communication.md#main-pars-header-1162517146) ・モデル要素のデータ表示パターンを定義できるようになりました。 例えば、日付、通貨、電話の形式などです。

**新しいタイプのグラフの使用**

複数のシリーズを含む四半円グ [ラフやチャートを](../../forms/using/chart-component-interactive-communications.md) Interactive Communicationsに追加できるようになりました。

**表の列の並べ替え**

インタラクティブ通 [信でテーブルの列を並べ替え](../../forms/using/create-interactive-communication.md#sortcolumns) ることができるようになりました。 表の列は、スタティックテキストオブジェクトやデータモデルオブジェクトを使用して連結および並べ替えることができます。

**Webチャネルでの新しいコンポーネントの使用**

Webチャネルにボタンとセパレーターのコンポーネントを追加できるようになりました。 詳しくは、Webチャネルにボタンコンポ [ーネントを追加するおよびWebチャネルのセパレータ](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) コンポ [ーネントを参照してください](../../forms/using/create-interactive-communication.md#separatorcomponent)。

**コンポーネントのサイズを変更するレイアウトモード**

WYSIWYGインターフェイスを使用して [](../../forms/using/resize-using-layout-mode.md) 、Webチャネル内のコンポーネントのサイズを変更するレイアウトモードに切り替えることができるようになりました。

**ユーザビリティの向上**

インタラクティブコミュニケーションの作成者は、通信の作成時に様々な使いやすい操作を利用できるようになりました。 操作のリストには、次の項目が含まれます。

* [印刷チャネルとWebチャネルで元に戻す/やり直し操作を実行する](../../forms/using/create-interactive-communication.md#undoredoactions)
* [@記号を使用したドキュメントフラグメントへの変数の追加](../../forms/using/texts-interactive-communications.md#searchvariables)
* [@記号を使用して、ドキュメントフラグメントにデータモデル要素を追加する](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [既存のインタラクティブ通信に対するWebチャネルの削除または追加](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [ドラッグ&amp;ドロップ操作を使用したデータソース要素とフィールドおよび変数の連結](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Interactive Communicationの作成中に、連結されていないフィールドと変数を強調表示する](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Webチャネル内の継承されたコンポーネントに対して、コピー、グループ、その他の追加のアクションを実行します](../../forms/using/create-interactive-communication.md#componenttoolbar)

**同期プロセスの改善**

印刷チャネルを使用して自動生成されるWebチャネルレイアウトには、いくつかの改善点があります。

![Interactive Communications Charts](assets/interactive-communication-charts.png)

## アダプティブフォーム {#adaptive-forms}

### アダプティブフォームでのAdobe signのクラウドベースの電子署名の使用 {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[クラウドベースの電子署名](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) （リモート署名）は、デスクトップ、モバイル、Webで機能する新世代の電子署名です。 署名者の認証に関する最高レベルのコンプライアンスと保証を満たします。 Cloudベースの電子署 [名を使用してアダプティブフォームに](../../forms/using/working-with-adobe-sign.md) 、署名できるようになりました。

#### Embed an Adaptive Form or Interactive Communication in AEM Sites Single Page Applications {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Formsを使用すると、アダプティブ [](../../forms/using/embed-adaptive-form-aem-sites-spa.md) フォームまたはインタラクティブ通信をAEMサイトのシングルページアプリケーション(SPA)にシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームとインタラクティブ通信は完全に機能し、ユーザーはページを離れることなくフォームに入力して送信できます。 Webページ上の他の要素のコンテキストを維持し、アダプティブフォームやインタラクティブコミュニケーションと同時にやり取りするのに役立ちます。

#### アダプティブフォームテーブルの列の並べ替え {#sort-columns-of-adaptive-form-tables}

アダプティブ [フォームテーブルの任意の列を昇順または降順に並べ替える](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) ことができます。 静的テキストを含むテーブル列、データモデルオブジェクトプロパティ、または静的テキストとデータモデルオブジェクトプロパティの組み合わせに対して、並べ替えを適用できます。

#### アダプティブフォームテンプレートの可用性を特定のパスに制限する {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

アダプティブフォームでは、cq:allowedPathsプロパティのサポートが追加されました。 このプロパティ [は、アダプティブフォームテンプレートの使用を特定のパスに制限します](../../forms/using/creating-adaptive-form.md#main-pars-text)。

#### アダプティブフォームへのチェックボックスのダイナミックな追加 {#add-check-boxes-to-the-adaptive-form-dynamically}

カスタム関数、フォームオブジェクト、またはオ [ブジェクトプロパティに基づいて動的にアダプティブフォーム](../../forms/using/rule-editor.md#setpropertyrule) にチェックボックスを追加するルールを定義できるようになりました。

## AEM ワークフロー {#aem-workflows}

### AEMワークフローでの変数の使用 {#use-variables-in-aem-workflows}

変数を使用すると、ワークフローステップで、実行時にワークフローステップ間でメタデータを保持および渡すことができます。 様々なタイプの変数を作成して、様々なタイプのデータを保存できます。例えば、整数、文字列、ドキュメント、フォームデータモデルのインスタンスなどです。 一般に、変数または変数のコレクションを使用するのは、変数が保持する値に基づいて決定する必要がある場合、またはプロセスで後で必要になる情報を保存する場合です。

変数は、前のバージョンで使 [用できる](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) MetaDataMapインターフェイスの拡張です。 メタデータ値の取得と更新に使用するカスタムECMAScriptコードの開発に費やす時間を節約できます。 MetaDataMapインターフェイスとECMAScriptコードを使用して、メタデータを操作し続けます。 MetaDataMapおよびECMAScriptで変数を使用するメリットは次のとおりです。

* カスタムコードに依存せずに、ワークフロー全体で変数に保存された値を動的に保存、更新および使用する
* 送信されたフォームのフォームデータモデルとデータファイル(XML/JSON)に対して直接値を取得し、更新する
* ドキュメント処理を実行するために、完全なドキュメントを変数に格納する

「移動先」、「分割」の各ステップ、およびすべてのAEM Formsワークフローステップで変数がサポートされます。 MetaDataMapインターフェイスを使用して、変数をネイティブでサポートしていないワークフロー手順の変数にアクセスできます。 詳しくは、AEM Workflowsでの変 [数を参照してください](../../forms/using/variable-in-aem-workflows.md)。

![ワークフロー内での変数の設定](assets/variable.png)

#### 異なるアダプティブフォームでのワークフローの使用 {#use-a-workflow-with-different-adaptive-forms}

アダプティブ [フォームは、割り当てタスクと](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) 、実行時のフォーム中心のワークフローのレコードステップのドキュメントに対して指定できます。 これにより、ワークフローが異なるアダプティブフォームで動作するようになります。 ワークフローのデザイン中にアダプティブフォームを選択する方法を決定できます。 アダプティブフォームは、絶対パスに配置したり、ワークフローへのペイロードとして送信したり、変数を使用して計算されたパスに配置したりできます。

#### フォーム中心のワークフロー手順の強化されたログ機能を使用する {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

フォーム中心のワークフローステップのログ機能は標準化されています。 現在は、フォーム中心のすべてのワークフローステップで、同様に標準化されたログが生成されます。 デバッグ速度の向上に役立ちます。

## データ統合 {#data-integration}

次の操作が可能になりました。

* [制約のリストに基づいて](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) 、入力データを検証します。 有効なデータのみをデータソースに送信するのに役立ちます。
* [WSDL(Web Services Description Language](../../forms/using/configure-data-sources.md#configure-soap-web-services) )ファイルで定義されたデフォルトのエンドポイントを上書きします。

* [Swagger定義ファイルで定義さ](../../forms/using/configure-data-sources.md#configure-restful-web-services) れているデフォルトのスキーム [](../../forms/using/configure-data-sources.md#configure-restful-web-services) 、ホストおよびベースパスを上書きします。

## プラットフォームとセキュリティの更新 {#platform-and-security-updates}

### 主なプラットフォームの更新 {#major-platform-updates}

サポート対象のオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK サーバー、LDAP サーバー、電子メールサーバーを自由に組み合わせて、AEM Forms をセットアップすることができます。The following are the major changes in [supported platforms](../../forms/using/aem-forms-jee-supported-platforms.md):

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
     <li>Oracle Weblogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>データベース</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
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

*別のプラットフォームへの移行に関する情報については、アドビサポートにお問い合わせください。

#### 新しいHTML5ベースのUI {#new-html-based-uis}

Adobe Flash playerの計画的なEOLと、Flashベースのコンテンツをオープンスタンダードに移行する全体的な方向に合わせて、AEM 6.5 formsは、ヘルスモニター、Process Management、Reader Extension、およびJEE上のAEM Formsのカテゴリ管理UIをHTML5ベースのUIに置き換えました。

#### セキュリティの強化 {#security-improvements}

* JEE上のAEM 6.5 Forms管理コンソールUIは、Apache Struts 2.5をベースにしています。
* AEM 6.5 Formsで、jQueryを3.2.1およびjQuery UI 1.12.1に使用するようになりました。変更の影響につ [いては](/help/forms/home.md) 、「アップグレードドキュメント」を参照してください。

#### アクセシビリティの強化 {#accessibility-improvements}

AEM 6.5 Formsでは、AEM Forms Workspaceのアクセシビリティが向上しました。
