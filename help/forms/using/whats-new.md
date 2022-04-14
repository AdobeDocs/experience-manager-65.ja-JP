---
title: 新機能の概要 | AEM 6.5 Forms
seo-title: New features summary | AEM 6.5 Forms
description: 世界で最も高度なデジタルエクスペリエンス管理ソリューションのフォームとドキュメントに対する最新の機能と改善点です。
seo-description: Latest features and improvements to forms and documents of world’s most advanced digital experience management solution.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1224'
ht-degree: 100%

---

# 新機能の概要 | AEM 6.5 Forms{#new-features-summary-aem-forms}

## トランザクションレポート {#transaction-reports}

トランザクションレポートでは、送信されたフォーム、処理されたドキュメント、レンダリングされたドキュメントの数を追跡できます。これらのトランザクションを追跡する目的は、プロダクトの使用状況について十分な情報を基に判断を行い、ハードウェアとソフトウェアに対する投資の割合を調整することにあります。 トランザクションの例を次に示します。

* アダプティブフォーム、HTML5 フォーム、またはフォームセットの送信
* インタラクティブ通信の印刷または web バージョンのレンディション
* あるファイル形式から別のファイル形式へのドキュメントの変換

トランザクションレポートの設定と使用については、[トランザクションレポートの概要](../../forms/using/transaction-reports-overview.md)を参照してください。

![トランザクションレポートのサンプル](assets/surface_transaction_reporting.png)

## インタラクティブコミュニケーション {#interactive-communications}

**データの表示パターンの定義**

インタラクティブ通信の作成者はフィールド、変数、フォームデータモデル要素の[データ表示パターン](create-interactive-communication.md#datadisplaypatterns)を定義できるようになりました。例えば、日付、通貨、電話番号の形式などです。

**新しい種類のグラフの使用**

[四分円グラフおよび複数の系列を持つグラフ](../../forms/using/chart-component-interactive-communications.md)をインタラクティブ通信に追加できます。

**テーブルの列の並べ替え**

インタラクティブ通信内で[テーブルの列の並べ替え](../../forms/using/create-interactive-communication.md#sortcolumns)ができます。テーブルの列を、静的テキストまたはデータモデルオブジェクトで連結し、並べ替えることができます。

**Web チャンネルでの新しいコンポーネントの使用**

Web チャンネルにボタンコンポーネントとセパレーターコンポーネントを追加できるようになりました。 詳しくは、[web チャンネルにボタンコンポーネントを追加](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel)および [web チャンネルのセパレーターコンポーネント](../../forms/using/create-interactive-communication.md#separatorcomponent)を参照してください。

**レイアウトモードを使用したコンポーネントのサイズの変更**

[レイアウトモード](../../forms/using/resize-using-layout-mode.md)に変更すると、WYSIWYG インターフェイスを使用して web チャンネル内のコンポーネントのサイズを変更できます。

**ユーザビリティの向上**

インタラクティブ通信の作成者は、様々な使いやすい操作を利用して通信を作成できるようになりました。 次のような操作を利用できます。

* [印刷および web チャンネルでの取り消しおよびやり直し操作の実行](../../forms/using/create-interactive-communication.md#undoredoactions)
* [@ 記号を使用してドキュメントフラグメントに変数を追加](../../forms/using/texts-interactive-communications.md#searchvariables)
* [@ 記号を使用してドキュメントフラグメントにデータモデル要素を追加](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [既存のインタラクティブ通信に web チャンネルを削除または追加](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [ドラッグ＆ドロップ操作を使用してデータソース要素をフィールドと変数に連結](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [インタラクティブ通信の作成時に連結されていないフィールドと変数をハイライト表示](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Web チャンネル内の継承されたコンポーネントに対してコピーやグループ化などの追加のアクションを実行](../../forms/using/create-interactive-communication.md#componenttoolbar)

**同期プロセスの改善**

印刷チャンネルを使用して自動生成される web チャネルレイアウトについていくつかの点が改善されました。

![インタラクティブ通信チャート](assets/interactive-communication-charts.png)

## アダプティブフォーム {#adaptive-forms}

### アダプティブフォームで Adobe Sign のクラウドベースのデジタル署名を使用する {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[クラウドベースの電子署名（リモート署名）は、デスクトップ、モバイル、Web 上で機能する新世代のデジタル署名で、署名者の認証に関する最高レベルのコンプライアンスと保証を満たします。](https://helpx.adobe.com/jp/sign/kb/digital-certificate-providers.html)クラウドベースの電子署名を使用して[アダプティブフォームに署名](../../forms/using/working-with-adobe-sign.md)できます。

#### AEM Sites の単一ページアプリケーションへのアダプティブフォームやインタラクティブコミュニケーションの埋め込み {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms では、AEM Sites 単一ページアプリケーション（SPA）にインタラクティブ通信や[アダプティブフォームをシームレスに埋め込む](../../forms/using/embed-adaptive-form-aem-sites-spa.md)ことができます。埋め込まれたアダプティブフォームおよびインタラクティブ通信ではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームの記入および送信ができます。これにより、ユーザーは Web ページのその他の要素とのコンテキストを保ったまま、同時にアダプティブフォームやインタラクティブ通信の操作を行うことができます。

#### アダプティブフォームテーブルの列の並べ替え {#sort-columns-of-adaptive-form-tables}

昇順または降順に[アダプティブフォームテーブルの列を並べ替える](../../forms/using/adaptive-forms-tables.md#sortcolumnstable)ことができます。静的テキスト、データモデルオブジェクトプロパティ、または静的テキストとデータモデルオブジェクトプロパティの組み合わせを含むテーブル列に並べ替えを適用できます。

#### アダプティブフォームテンプレートの可用性を特定のパスに制限 {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

アダプティブフォームでは、cq:allowedPaths プロパティのサポートが追加されました。 プロパティは、[アダプティブフォームテンプレートの使用を特定のパスに制限します](creating-adaptive-form.md#adaptive-form-templates)。

#### アダプティブフォームにチェックボックスを動的に追加する {#add-check-boxes-to-the-adaptive-form-dynamically}

カスタム関数、フォームオブジェクト、またはオブジェクトプロパティに基づいて、[チェックボックスをアダプティブフォームに動的に追加](../../forms/using/rule-editor.md#setpropertyrule)するルールを定義できるようになりました。

## AEM ワークフロー {#aem-workflows}

### AEM ワークフローでの変数の使用 {#use-variables-in-aem-workflows}

変数を使用すると、ワークフロー手順で、実行時に複数の手順にわたってメタデータを保持および渡すことができます。様々なタイプの変数を作成して、様々なタイプのデータを保存できます。例えば、整数、文字列、ドキュメント、フォームデータモデルインスタンスなどです。 一般に、変数または変数のコレクションを使用するのは、変数が保持する値に基づいて決定する必要がある場合、またはプロセスで後で必要になる情報を保存する場合です。

変数は、以前のバージョンで使用可能な [MetaDataMap](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) インターフェイスの拡張です。メタデータ値の取得と更新に使用されるカスタム ECMAScript コードの開発に費やす時間を節約できます。メタデータを操作するには、引き続き MetaDataMap インターフェイスと ECMAScript コードを使用します。MetaDataMap および ECMAScript よりも変数を使用する利点は次のとおりです。

* カスタムコードに依存することなく、ワークフロー全体で変数に格納された値を動的に格納、更新、および使用します
* 送信されたフォームのフォームデータモデルとデータファイル（XML／JSON）に直接値を取得してアップデートします
* 完全なドキュメントを変数に格納して、ドキュメント処理を実行します

Go To ステップ、OR Split ステップ、およびすべての AEM Forms ワークフローステップは変数をサポートします。MetaDataMap インターフェイスを使用して、変数のネイティブサポートがないワークフローステップの変数にアクセスできます。詳しくは、[AEM Workflows の変数](../../forms/using/variable-in-aem-workflows.md)を参照してください。

![ワークフローの変数の設定](assets/variable.png)

#### 別のアダプティブフォームでのワークフローの使用  {#use-a-workflow-with-different-adaptive-forms}

[割り当てタスクのアダプティブフォームを指定](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step)し、実行時のフォーム中心のワークフローの記録ステップのドキュメントを指定できます。これにより、ワークフローを様々なアダプティブフォームで機能させることができます。ワークフローの設計時に、アダプティブフォームを選択する方法を決定できます。アダプティブフォームは、絶対パスに配置するか、ワークフローにペイロードとして送信するか、変数を使用して計算されたパスで使用できます。

#### フォーム中心のワークフローステップの拡張ロギング機能を使用する {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

フォーム中心のワークフローステップのロギング機能が標準化されています。現在、すべてのフォーム中心のワークフローステップは、同様に標準化されたログを生成します。デバッグ速度の向上に役立ちます。

## データ統合 {#data-integration}

次の操作が可能になっています。

* 制約のリストに基づいて[入力データを検証](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data)します。有効なデータのみがデータソースに送信されるようにします。
* WSDL（web サービス記述言語）ファイルで定義されている[デフォルトのエンドポイントをオーバーライド](../../forms/using/configure-data-sources.md#configure-soap-web-services)します。

* [Swagger 定義ファイルで定義されているデフォルトの](../../forms/using/configure-data-sources.md#configure-restful-web-services) [スキーム、ホスト、およびベースパス](../../forms/using/configure-data-sources.md#configure-restful-web-services)をオーバーライドします。

## プラットフォームとセキュリティのアップデート {#platform-and-security-updates}

### プラットフォームの主要なアップデート {#major-platform-updates}

サポート対象のオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK サーバー、LDAP サーバー、電子メールサーバーを自由に組み合わせて、AEM Forms をセットアップすることができます。[サポート対象のプラットフォーム](../../forms/using/aem-forms-jee-supported-platforms.md)に関する主な変更点を以下に示します。

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
    <li>WebSphere Liberty プロファイル</li>
    <li>Oracle WebLogic ／</li>
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
     <li>Windows 8.1 のサポート</li>
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

* 別のプラットフォームへの移行については、アドビサポートにお問い合わせください

#### 新しい HTML5 ベースの UI {#new-html-based-uis}

AEM 6.5 Forms では、Adobe Flash Player の計画された EOL と、Flash ベースのコンテンツをオープンスタンダードに移行する全体的な方向性に沿って、JEE 管理コンソール上の AEM Forms の Health Monitor、Process Management、Reader Extension、Category Management 各 UI の Flash ベースの UI が HTML5 ベースの UI で置き換えられました。

#### セキュリティの強化 {#security-improvements}

* JEE 上の AEM 6.5 Forms 管理コンソールの UI は、Apache Struts 2.5 に基づいたものとなりました。
* AEM 6.5 Forms は、jQuery を 3.2.1 および jQuery UI 1.12.1 で使用するようになりました。変更の影響については、[アップグレードドキュメント](/help/forms/home.md)を確認してください。

#### アクセシビリティの強化 {#accessibility-improvements}

AEM 6.5 Forms で AEM Forms Workspace のアクセシビリティが向上しました。
