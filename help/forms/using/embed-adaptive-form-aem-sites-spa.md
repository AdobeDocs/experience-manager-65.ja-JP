---
title: アダプティブフォームまたはインタラクティブコミュニケーションをAEM Sitesのシングルページアプリに埋め込む
seo-title: AEM Sitesページにアダプティブフォームまたはインタラクティブコミュニケーションを埋め込む
description: AEM Sitesページにアダプティブフォームまたはインタラクティブコミュニケーションを埋め込みます。 ユーザーは、サイトページを離れることなく、フォームに入力して送信できます。
seo-description: アダプティブフォームやインタラクティブコミュニケーションは、AEM Sitesページに埋め込むことができます。 ユーザーは、サイトページを離れることなく、フォームに入力して送信できます。
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 11%

---


# Embed an adaptive form or Interactive Communication in AEM Sites Single Page Application{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概要 {#overview}

AEM Formsを使用すると、アダプティブフォームやインタラクティブコミュニケーションをAEM Sitesのシングルページアプリ(SPA)にシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームとインタラクティブ通信は完全に機能し、ユーザーはページを離れることなくフォームに入力して送信できます。 Webページ上の他の要素のコンテキストを維持し、アダプティブフォームやインタラクティブコミュニケーションと同時にやり取りするのに役立ちます。

AEM Sitesシングルページアプリでは、アダプティブフォームまたはインタラクティブコミュニケーションを、 [AEM FormsSPAコンテナコンポーネントを使用して追加できます](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[。](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) これは、サイトページに追加できるAEM SitesSPAのAEM Formsコンポーネントです。

アダプティブフォームをSPA以外のAEM Sitesに埋め込む方法について詳しくは、「アダプティブフォームまたはインタラクティブなAEM Sitesをページに [埋め込む](/help/forms/using/embed-adaptive-form-aem-sites.md)」を参照してください。

## 前提条件 {#prerequisites}

AEM FormsSPAコンテナコンポーネントを使用して、アダプティブフォームまたはインタラクティブ通信をAEMサイトのSPAに埋め込むには、次の手順を実行します。

* Java SE開発キット8以降
* Apache Maven 3.3.1以降
* AEM作成者インスタンス
* [AEM Forms6.4.2オーサーインスタンス上のアドオンパッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)

## AEM FormsSPAコンテナコンポーネントのインストール {#install-aem-forms-spa-container-component}

次の手順を実行して、AEM FormsSPAコンテナコンポーネントをインストールします。

1. [SPAのAEM Formsコンポーネントをクローンまたはダウンロードします](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa)。
1. SPA用のAEM Formsコンポーネントをインストールします。 コンポーネントのインストール手順は、 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) ファイルに記載されています。

   このコンポーネントは、SPAコンテナコンポーネントとReactベースのSPAプロジェクトとの統合に使用できる [サンプルReactコンポーネント](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) を含む。

1. [ReactベースのSPAプロジェクトのコピーまたはダウンロード](https://github.com/adobe/aem-sample-we-retail-journal)。
1. README.md [](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) ファイルの手順に従って、SPAコンテナコンポーネントをReactベースのSPAプロジェクトと統合します。

   AEM FormsSPAコンテナコンポーネントをインストールし、コンポーネントとReactベースのSPAプロジェクトを統合した後、AEM SitesページにアダプティブフォームとInteractive Communicationsを埋め込むことができます。

## アダプティブフォームまたはインタラクティブコミュニケーションを埋め込む {#af-component}

SPAコンテナコンポーネント用のAEM Formsを使用してアダプティブフォームまたはインタラクティブ通信を埋め込むには：

1. アダプティブフォームやインタラクティブコミュニケーションを埋め込むAEMサイトページを編集モードで開きます。
1. 次のいずれかのオプションを使用して、 **AEM Form for SPA** (AEM Form SPA)コンポーネントをページに挿入します。

   * サイトページでレイアウトコンテナをタップし、「 **+」をタップし** て、SPA **用** AEM Formコンポーネントを選択します。

   * From the Component browser panel, drag-drop the **AEM Form for SPA** component on the page.
   * アセットブラウザーでアダプティブフォームまたはインタラクティブコミュニケーションを検索し、サイトページにドラッグ&amp;ドロップします。 SPAコンポーネントコンテナのAEM Formsにフォームを埋め込みます。

   >[!NOTE]
   >
   >ページ上での複数のAEM FormsSPAコンテナコンポーネントのレンダリングはサポートされていません。 1つのページに複数のAEM FormsのSPAコンテナを設定できますが、一度にレンダリングされるコンポーネントは1つだけです。 不一致を避けるために、1つのページに1つのコンポーネントのみが表示されていることを確認します。

1. Tap the embedded AEM Forms SPA Container component in the sites page, and then tap ![settings_icon](assets/settings_icon.png) on the action bar. The **Edit AEM Forms SPA Container** dialog opens.
1. In the **Edit AEM Forms Container** dialog, specify the following:

   * **アセットの種類：**&#x200B;埋め込むアセットの種類を選択します。The options are **Adaptive Form** and **Interactive Communication**

   * **Asset Path**: 埋め込むアダプティブフォームまたはインタラクティブコミュニケーションを参照して選択します。 アダプティブフォームまたはインタラクティブ通信がアセットブラウザーを使用して挿入された場合、このフィールドには自動入力されます。
   * **チャネル** （Interactive Communicationのみ）: 埋め込むインタラクティブチャネルの種類を選択します。 「 **Webチャネル** 」と「 **印刷チャネル**」を選択できます。

   * **テーマ**: アダプティブフォームまたはインタラクティブコミュニケーションのコンポーネントのスタイル設定を定義するテーマを選択します。 スタイル設定には、フォントスタイル、背景色、サイズ、配置など、外観のプロパティが含まれます。

1. Tap ![done_icon](assets/done_icon.png) to save the settings. これで、アダプティブフォームまたはインタラクティブ通信がページに埋め込まれます。

## 埋め込まれたアダプティブフォームとインタラクティブ通信の発行 {#publish-embedded-adaptive-form-and-interactive-communication}

埋め込みアセット（アダプティブフォームまたはインタラクティブコミュニケーション）をAEM Sitesページに発行する場合は、次のシナリオを考慮してください。

* AEM Sitesページを初めて発行する場合で、埋め込まれたアダプティブフォームまたはインタラクティブコミュニケーションが含まれている場合は、サイトページと埋め込まれたアセットを発行します。
* 発行済みサイトページに埋め込まれたアダプティブフォームまたはインタラクティブコミュニケーションのみを変更した場合は、元のアセットを発行し、変更内容は発行済みサイトページに反映されます。 発行済みサイトページにはアセットへの参照が含まれており、ページを再発行する必要はありません。
* サイトページと、埋め込まれたアダプティブフォームまたはインタラクティブコミュニケーションを変更した場合は、サイトページと埋め込まれたアセットを再発行します。

## 埋め込まれたアダプティブフォームとインタラクティブ通信の変更 {#modify-embedded-adaptive-form-and-interactive-communication}

AEMサイトページには、AEM Formsコンテナでアダプティブフォームとインタラクティブコミュニケーションへの参照が保持されています。 したがって、元のアダプティブフォームとインタラクティブコミュニケーションで設定されたテーマ、スタイル、送信アクションなどの設定とプロパティは、埋め込まれたアダプティブフォームとインタラクティブコミュニケーションでも保持されます。

埋め込まれたアダプティブフォームおよびインタラクティブ通信の設定やプロパティを変更するには、次のいずれかを実行します。

* 各エディターでアダプティブフォームまたはインタラクティブコミュニケーションでオリジナルフォームを開き、変更します。
* Tap the adaptive form or Interactive Communication from within the Sites page in edit mode and then tap **Edit in a new window**. 元のフォームが編集モードで開きます。

## 注意点とベストプラクティス {#considerations-and-best-practices}

AEM サイトページにアダプティブフォームを埋め込む際は、以下の点に留意してください。

* 元のフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ユーザードラフトと埋め込みフォームの送信はサポートされており、フォームポータル上の「下書き」タブや「送信済みフォーム」タブに表示されます。
* 元のフォームに構築された送信アクションは、埋め込まれたフォームでも保持されます。
* 元のフォームに構築されたのエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたフォームでは動作しません。ただし、サイトページのエクスペリエンスのターゲット設定を使用して、ユーザーのプロファイルに基づいて異なるフォームを表示することができます。
* 元のフォームに対してAdobe Serverが設定されている場合、埋め込まれたフォームの分析データは、AdobeAnalyticsに取り込まれます。 ただし、フォームの分析レポートでは使用できません。

