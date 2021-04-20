---
title: アダプティブフォームまたはインタラクティブコミュニケーションをAEM Sitesのシングルページアプリに埋め込む
seo-title: アダプティブフォームまたはインタラクティブコミュニケーションをAEM Sitesページに埋め込む
description: アダプティブフォームまたはインタラクティブコミュニケーションをAEM Sitesページに埋め込みます。 ユーザーは、サイトページを離れることなく、フォームに入力して送信できます。
seo-description: アダプティブフォームやインタラクティブコミュニケーションは、AEM Sitesのページに埋め込むことができます。 ユーザーは、サイトページを離れることなく、フォームに入力して送信できます。
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 11%

---


# アダプティブフォームまたはインタラクティブコミュニケーションをAEM Sitesシングルページアプリに埋め込む{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概要 {#overview}

AEM Formsでは、フォーム開発者がAEM Sitesのシングルページアプリ(SPA)にアダプティブフォームとインタラクティブコミュニケーションをシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームとインタラクティブ通信は完全に機能し、ユーザーはページを離れることなくフォームに入力して送信できます。 Webページ上の他の要素のコンテキストを維持し、アダプティブフォームやインタラクティブコミュニケーションと同時にやり取りするのに役立ちます。

AEM Sitesシングルページアプリでは、[AEM FormsSPAコンテナコンポーネント](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[を使用して、アダプティブフォームまたはインタラクティブコミュニケーションを追加できます。](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) これは、サイトページに追加できるAEM SitesSPAのAEM Formsコンポーネントです。

SPA以外のAEM Sitesにアダプティブフォームを埋め込む方法について詳しくは、[AEM Sitesページにアダプティブフォームまたはインタラクティブな通信を埋め込む](/help/forms/using/embed-adaptive-form-aem-sites.md)を参照してください。

## 前提条件 {#prerequisites}

AEM FormsSPAコンテナコンポーネントを使用してAEMサイトSPAにアダプティブフォームまたはインタラクティブ通信を埋め込むには、次のをインストール済みであることを確認します。

* Java SE開発キット8以降
* Apache Maven 3.3.1以降
* AEM作成者インスタンス
* [AEM Forms6.4.2アドオン](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) パッケージオン作成者インスタンス

## AEM FormsSPAコンテナコンポーネントのインストール{#install-aem-forms-spa-container-component}

次の手順を実行して、AEM FormsSPAコンテナコンポーネントをインストールします。

1. [SPA用のAEM Formsコンポーネントをコピーまたはダウンロードします](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa)。
1. SPA用のAEM Formsコンポーネントをインストールします。 コンポーネントのインストール手順は、[README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component)ファイルに記載されています。

   コンポーネントは、SPAコンテナコンポーネントをReactベースのSPAプロジェクトと統合するために使用できる[サンプルのReactコンポーネント](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component)を含む。

1. [リアクトベースのSPAプロジェクトのコピーまたはダウンロード](https://github.com/adobe/aem-sample-we-retail-journal)。
1. [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor)ファイルの説明に従って、SPAコンテナコンポーネントをReactベースのSPAプロジェクトに統合します。

   AEM FormsSPAコンテナコンポーネントをインストールし、コンポーネントとReactベースのSPAプロジェクトを統合した後、AEM SitesページにアダプティブフォームとInteractive Communicationsを埋め込むことができます。

## アダプティブフォームまたはインタラクティブ通信を埋め込む{#af-component}

SPAコンテナコンポーネントにAEM Formsを使用してアダプティブフォームまたはインタラクティブコミュニケーションを埋め込むには：

1. アダプティブフォームやインタラクティブコミュニケーションを埋め込むAEMサイトページを編集モードで開きます。
1. 次のいずれかのオプションを使用して、**SPA**&#x200B;用AEMフォームコンポーネントをページに挿入します。

   * サイトページのレイアウトコンテナをタップし、**+**&#x200B;をタップして、SPA **コンポーネント用の** AEMフォームを選択します。

   * コンポーネントブラウザパネルから、**SPA**&#x200B;用AEMフォームコンポーネントをページにドラッグ&amp;ドロップします。
   * アセットブラウザーでアダプティブフォームまたはインタラクティブコミュニケーションを検索し、サイトページにドラッグ&amp;ドロップします。 SPAコンポーネントコンテナ用にAEM Formsにフォームを埋め込みます。

   >[!NOTE]
   >
   >ページ上での複数のAEM FormsSPAコンテナコンポーネントのレンダリングはサポートされていません。 1つのページに複数のAEM FormsSPAコンテナを設定できますが、一度にレンダリングされるコンポーネントは1つだけです。 不一致を避けるために、1つのページに1つのコンポーネントのみが表示されていることを確認します。

1. サイトページに埋め込まれたAEM FormsSPAコンテナコンポーネントをタップし、アクションバーの![settings_icon](assets/settings_icon.png)をタップします。 [**AEM FormsSPAの編集**]ダイアログが開きます。
1. **AEM Formsコンテナ**&#x200B;を編集ダイアログで、次の設定を指定します。

   * **アセットの種類：**&#x200B;埋め込むアセットの種類を選択します。オプションは、**アダプティブフォーム**&#x200B;と&#x200B;**インタラクティブコミュニケーション**&#x200B;です

   * **Asset Path**:埋め込むアダプティブフォームまたはインタラクティブコミュニケーションを参照して選択します。アダプティブフォームまたはインタラクティブ通信がアセットブラウザーを使用して挿入された場合、このフィールドには自動入力されます。
   * **チャネル** （対話型通信のみ）:埋め込むインタラクティブチャネルの種類を選択します。オプションは&#x200B;**Webチャネル**&#x200B;と&#x200B;**印刷チャネル**&#x200B;です。

   * **テーマ**:アダプティブフォームまたはインタラクティブコミュニケーションのコンポーネントのスタイル設定を定義するテーマを選択します。スタイル設定には、フォントスタイル、背景色、サイズ、配置など、外観のプロパティが含まれます。

1. ![done_icon](assets/done_icon.png)をタップして設定を保存します。 これで、アダプティブフォームまたはインタラクティブ通信がページに埋め込まれます。

## 埋め込まれたアダプティブフォームとインタラクティブ通信を発行{#publish-embedded-adaptive-form-and-interactive-communication}

埋め込みアセット（アダプティブフォームまたはインタラクティブコミュニケーション）をAEM Sitesページに発行する場合は、次のシナリオを考慮してください。

* 初めてAEM Sitesページを発行する場合で、埋め込みのアダプティブフォームまたはインタラクティブコミュニケーションが含まれている場合は、サイトページと埋め込みアセットを発行します。
* 発行済みサイトページに埋め込まれたアダプティブフォームまたはインタラクティブコミュニケーションのみを変更した場合は、元のアセットを発行し、変更内容は発行済みサイトページに反映されます。 発行済みサイトページにはアセットへの参照が含まれており、ページを再発行する必要はありません。
* サイトページと、埋め込まれたアダプティブフォームまたはインタラクティブコミュニケーションを変更した場合は、サイトページと埋め込まれたアセットを再発行します。

## 埋め込まれたアダプティブフォームとインタラクティブ通信の変更{#modify-embedded-adaptive-form-and-interactive-communication}

AEMサイトのページには、AEM Formsコンテナのアダプティブフォームとインタラクティブコミュニケーションへの参照が保持されています。 したがって、元のアダプティブフォームとインタラクティブコミュニケーションで設定されたテーマ、スタイル、送信アクションなどの設定とプロパティは、埋め込まれたアダプティブフォームとインタラクティブコミュニケーションでも保持されます。

埋め込まれたアダプティブフォームおよびインタラクティブ通信の設定やプロパティを変更するには、次のいずれかを実行します。

* 各エディターでアダプティブフォームまたはインタラクティブコミュニケーションでオリジナルフォームを開き、変更します。
* 編集モードでサイトページ内からアダプティブフォームまたはインタラクティブコミュニケーションをタップし、**新しいウィンドウで編集**&#x200B;をタップします。 元のフォームが編集モードで開きます。

## 注意点とベストプラクティス {#considerations-and-best-practices}

AEM サイトページにアダプティブフォームを埋め込む際は、以下の点に留意してください。

* 元のフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ユーザードラフトと埋め込みフォームの送信はサポートされており、フォームポータル上の「下書き」タブや「送信済みフォーム」タブに表示されます。
* 元のフォームに構築された送信アクションは、埋め込まれたフォームでも保持されます。
* 元のフォームに構築されたのエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたフォームでは動作しません。ただし、サイトページのエクスペリエンスのターゲット設定を使用して、ユーザーのプロファイルに基づいて異なるフォームを表示することができます。
* 元のフォームに対してAdobe Analyticsが設定している場合、埋め込まれたフォームの分析データはAdobe Analyticsで取得されます。 ただし、フォームの分析レポートでは使用できません。

