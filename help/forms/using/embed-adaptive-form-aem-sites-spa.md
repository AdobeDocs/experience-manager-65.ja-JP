---
title: AEMサイトのシングルページアプリケーションにアダプティブフォームまたはインタラクティブ通信を埋め込む
seo-title: AEMサイトページにアダプティブフォームまたはインタラクティブコミュニケーションを埋め込む
description: AEMサイトページにアダプティブフォームまたはインタラクティブコミュニケーションを埋め込みます。 ユーザーは、サイトページを離れることなくフォームに入力し、送信できます。
seo-description: AEMサイトページにアダプティブフォームやインタラクティブコミュニケーションを埋め込むことができます。 ユーザーは、サイトページを離れることなくフォームに入力し、送信できます。
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: d12d35bf8355d3069071523427a7794b88c09b13

---


# Embed an adaptive form or Interactive Communication in AEM Sites Single Page Application{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概要 {#overview}

AEM Formsを使用すると、フォーム開発者はアダプティブフォームとインタラクティブコミュニケーションをAEM Sites Single Page Application(SPA)にシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームとインタラクティブコミュニケーションは完全に機能し、ユーザーはページを離れることなくフォームに入力して送信できます。 Webページ上の他の要素のコンテキストを維持し、アダプティブフォームやインタラクティブコミュニケーションと同時にやり取りするのに役立ちます。

AEMサイトのシングルページアプリケーションでは、 [AEM Forms SPA Containerコンポーネントを使用してアダプティブフォームまたはインタラクティブ通信を追加できます](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[。](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) これは、サイトページに追加できるAEMサイトSPA用のAEM formsコンポーネントです。

SPA以外のAEMサイトにアダプティブフォームを埋め込む方法について詳しくは、「AEMサイトページにアダプティブフォ [ームまたはインタラクティブな通信を埋め込む」を参照してください](/help/forms/using/embed-adaptive-form-aem-sites.md)。

## 前提条件 {#prerequisites}

AEM Forms SPA Containerコンポーネントを使用してAEMサイトのSPAにアダプティブフォームまたはインタラクティブ通信を埋め込むには、次のファイルがインストールされていることを確認します。

* Java SE開発キット8以降
* Apache Maven 3.3.1以降
* AEM作成者インスタンス
* [オーサーインスタンス上のAEM Forms 6.4.2アドオンパッケージ](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)

## AEM Forms SPA Containerコンポーネントのインストール {#install-aem-forms-spa-container-component}

次の手順を実行して、AEM Forms SPA Containerコンポーネントをインストールします。

1. [SPA用のAEM Formsコンポーネントをコピーまたはダウンロードします](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa)。
1. SPA用のAEM Formsコンポーネントをインストールします。 コンポーネントのインストール手順は、 [README.mdファイルで確認できます](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) 。

   コンポーネントには、SPAコンテ [ナコンポーネントを](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) 、ReactベースのSPAプロジェクトと統合するために使用できるサンプルReactコンポーネントが含まれます。

1. [ReactベースのSPAプロジェクトのコピーまたはダウンロード](https://github.com/adobe/aem-sample-we-retail-journal)。
1. README.md [](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) .

   AEM Forms SPA Containerコンポーネントをインストールし、コンポーネントとReactベースのSPAプロジェクトを統合した後、AEMサイトページにアダプティブフォームとInteractive Communicationsを埋め込むことができます。

## アダプティブフォームまたはインタラクティブ通信を埋め込む {#af-component}

AEM Forms for SPA Containerコンポーネントを使用してアダプティブフォームまたはインタラクティブ通信を埋め込むには：

1. アダプティブフォームまたはインタラクティブ通信を埋め込むAEMサイトページを編集モードで開きます。
1. 次のオプシ **ョンのいずれかを使用して、ページにAEM Form for SPA** (AEM Form)コンポーネントを挿入します。

   * サイトページでレイアウトコンテナをタップし、「 **+」をタッ** プして、SPA用 **AEM Formコンポーネントを選択します** 。

   * From the Component browser panel, drag-drop the **AEM Form for SPA** component on the page.
   * アセットブラウザーでアダプティブフォームまたはインタラクティブコミュニケーションを検索し、サイトページにドラッグ&amp;ドロップします。 AEM Forms for SPAコンポーネントコンテナにフォームを埋め込みます。
   >[!NOTE]
   >
   >ページ上での複数のAEM Forms SPA Containerコンポーネントのレンダリングはサポートされていません。 1つのページに複数のAEM Forms SPAコンテナを設定できますが、一度にレンダリングされるコンポーネントは1つだけです。 不一致を避けるために、1つのページに1つのコンポーネントのみが表示されるようにします。

1. Tap the embedded AEM Forms SPA Container component in the sites page, and then tap ![settings_icon](assets/settings_icon.png) on the action bar. The **Edit AEM Forms SPA Container** dialog opens.
1. In the **Edit AEM Forms Container** dialog, specify the following:

   * **アセットの種類：**&#x200B;埋め込むアセットの種類を選択します。The options are **Adaptive Form** and **Interactive Communication**

   * **Asset Path**:埋め込むアダプティブフォームまたはインタラクティブ通信を参照して選択します。 アダプティブフォームまたはインタラクティブ通信がアセットブラウザーを使用して挿入されると、このフィールドに自動入力されます。
   * **チャネル** （Interactive Communicationのみ）:埋め込むインタラクティブチャネルの種類を選択します。 「 **Webチャネル** 」と「プリ **ントチャネル**」

   * **テーマ**:アダプティブフォームまたはインタラクティブコミュニケーションのコンポーネントのスタイル設定を定義するテーマを選択します。 スタイル設定には、フォントスタイル、背景色、サイズ、配置など、外観のプロパティが含まれます。

1. Tap ![](assets/done_icon.png) to save the settings. これで、アダプティブフォームまたはインタラクティブ通信がページに埋め込まれました。

## 埋め込みアダプティブフォームとインタラクティブ通信の発行 {#publish-embedded-adaptive-form-and-interactive-communication}

AEMサイトページで埋め込みアセット（アダプティブフォームまたはインタラクティブ通信）を発行する場合は、次のシナリオを考慮してください。

* AEMサイトページを初めて発行する場合、そのページにアダプティブフォームやインタラクティブコミュニケーションが埋め込まれている場合は、サイトページと埋め込みアセットを発行します。
* 発行済みサイトページに埋め込まれたアダプティブフォームまたはインタラクティブコミュニケーションのみを変更した場合は、元のアセットを発行し、変更内容は発行済みサイトページに反映されます。 発行済みサイトページにはアセットへの参照が含まれ、ページを再発行する必要はありません。
* サイトページと埋め込まれたアダプティブフォームまたはインタラクティブコミュニケーションを変更した場合は、サイトページと埋め込まれたアセットを再発行します。

## 埋め込まれたアダプティブフォームとインタラクティブ通信の変更 {#modify-embedded-adaptive-form-and-interactive-communication}

AEMサイトページでは、AEM formsコンテナ内のアダプティブフォームとインタラクティブ通信への参照を管理します。 したがって、元のアダプティブフォームとインタラクティブ通信で設定されたテーマ、スタイル、送信アクションなどの設定とプロパティは、埋め込まれたアダプティブフォームとインタラクティブ通信に保持されます。

埋め込まれたアダプティブフォームとインタラクティブ通信の設定またはプロパティを変更するには、次のいずれかの操作を行います。

* 元のフォームをアダプティブフォームまたはインタラクティブコミュニケーションの各エディターで開き、変更します。
* Tap the adaptive form or Interactive Communication from within the Sites page in edit mode and then tap **Edit in a new window**. 元のフォームが編集モードで開きます。

## 注意点とベストプラクティス {#considerations-and-best-practices}

AEM サイトページにアダプティブフォームを埋め込む際は、以下の点に留意してください。

* 元のフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ユーザードラフトと埋め込みフォームの送信はサポートされており、フォームポータル上の「下書き」タブや「送信済みフォーム」タブに表示されます。
* 元のフォームに構築された送信アクションは、埋め込まれたフォームでも保持されます。
* 元のフォームに構築されたのエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたフォームでは動作しません。ただし、サイトページでエクスペリエンスのターゲット設定を使用して、ユーザープロファイルに基づいて異なるフォームを表示することができます。
* 元のフォームに対してAdobe Analyticsが設定されている場合、埋め込まれたフォームの解析データがAdobe Analyticsに取り込まれます。 ただし、フォームの分析レポートでは使用できません。

