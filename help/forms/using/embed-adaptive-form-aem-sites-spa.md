---
title: AEM Sites の単一ページアプリケーションへのアダプティブフォームやインタラクティブコミュニケーションの組み込み
seo-title: Embed adaptive forms or Interactive Communications in AEM Sites pages
description: AEM Sites ページにアダプティブフォームやインタラクティブコミュニケーションを組み込みます。ユーザーは、Sites のページから移動せずにフォームを記入および送信できます。
seo-description: You can embed adaptive forms or Interactive Communication in AEM Sites pages. Users can fill and submit forms without leaving the Sites page.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: Adaptive Forms
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1088'
ht-degree: 100%

---

# AEM Sites の単一ページアプリケーションへのアダプティブフォームやインタラクティブコミュニケーションの組み込み{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概要 {#overview}

AEM Forms を使用すると、フォーム開発者は AEM Sites 単一ページアプリケーション（SPA）ページにアダプティブフォームおよびインタラクティブ通信をシームレスに組み込むことができます。組み込まれたアダプティブフォームおよびインタラクティブ通信ではすべての機能を使用できるため、ユーザーは、ページから移動せずにフォームの記入や送信ができます。これにより、ユーザーは Web ページのその他の要素とのコンテキストを保ったまま、同時にアダプティブフォームやインタラクティブ通信の操作を行うことができます。

AEM Sites 単一ページアプリケーションでは、[AEM Forms SPA Container コンポーネント](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[を使用してアダプティブフォームやインタラクティブ通信を追加できます。](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)これは AEM Sites SPA 用の AEM Forms コンポーネントで、Sites ページに追加できます。

SPA AEM Sites 以外でのアダプティブフォームの組み込みについて詳しくは、[AEM Sites ページへのアダプティブフォームまたはインタラクティブ通信の組み込み](/help/forms/using/embed-adaptive-form-aem-sites.md)を参照してください。

## 前提条件 {#prerequisites}

AEM Forms SPA コンテナコンポーネントを使用して、アダプティブフォームやインタラクティブ通信を AEM Sites SPA に組み込むには、以下がインストールされていることを確認します。

* Java SE Development Kit 8 以降
* Apache Maven 3.3.1 以降
* AEM オーサーインスタンス
* オーサーインスタンスの [AEM Forms 6.4.2 アドオンパッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)

## AEM Forms SPA Container コンポーネントのインストール {#install-aem-forms-spa-container-component}

次の手順を実行して、AEM Forms SPA コンテナコンポーネントをインストールします。

1. [SPA 用の AEM Forms コンポーネントを複製またはダウンロード](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa)します。
1. SPA 用の AEM Forms コンポーネントをインストールします。 コンポーネントのインストール手順は、[README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) ファイルで説明しています。

   このコンポーネントには[サンプル React コンポーネント](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component)が含まれており、SPA コンテナコンポーネントを React ベースの SPA プロジェクトと統合するために使用できます。

1. [React ベースの SPA プロジェクトをクローンまたはダウンロード](https://github.com/adobe/aem-sample-we-retail-journal)します。
1. [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) ファイルにある説明に従って、SPA コンテナコンポーネントと React ベースの SPA プロジェクトを統合します。

   AEM Forms SPA コンテナコンポーネントをインストールし、そのコンポーネントを React ベースの SPA プロジェクトに統合した後、AEM Sites ページにアダプティブフォームとインタラクティブ通信を組み込むことができます。

## アダプティブフォームまたはインタラクティブ通信を組み込む {#af-component}

AEM Forms コンテナコンポーネントを使用してアダプティブフォームやインタラクティブ通信を組み込むには：

1. アダプティブフォームやインタラクティブ通信を組み込む AEM Sites ページを、編集モードで開きます。
1. 次のいずれかのオプションを使用して、ページ上で **AEM Form for SPA** コンポーネントを挿入します。

   * Sites ページのレイアウトコンテナをタップし、**+** をタップして、**AEM form for SPA** コンポーネントを選択します。

   * コンポーネントブラウザーパネルから、**AEM Form for SPA** コンポーネントをページ上にドラッグアンドドロップします。
   * または、アセットブラウザーでアダプティブフォームまたはインタラクティブ通信を検索して、Sites ページにドラッグアンドドロップします。これにより、AEM Formsにフォームが組み込まれ、SPA コンポーネントコンテナに格納されます。

   >[!NOTE]
   >
   >1 つのページでの複数の AEM Forms SPA コンテナコンポーネントのレンダリングはサポートされていません。1 つのページに複数の AEM Forms SPA コンテナを追加することができますが、一度にレンダリングされるコンポーネントは 1 つだけです。 不一致を避けるために、1 つのページに 1 つのコンポーネントのみが表示されるようにします。

1. Sites ページに埋め込まれた AEM Forms SPA コンテナコンポーネントをタップし、アクションバーの ![settings_icon](assets/settings_icon.png) をタップします。**AEM Forms SPA コンテナを編集**&#x200B;ダイアログが開きます。
1. **AEM Forms コンテナを編集**&#x200B;ダイアログで、次の設定を行います。

   * **アセットのタイプ：**&#x200B;埋め込むアセットのタイプを選択します。オプションには「**アダプティブフォーム**」と「**インタラクティブ通信**」があります。

   * **アセットパス：**&#x200B;埋め込むアダプティブフォームまたはインタラクティブ通信を参照して選択します。アダプティブフォームまたはインタラクティブ通信がアセットブラウザーから挿入されると、このフィールドは自動入力されます。
   * **チャネル**（インタラクティブ通信のみ）：埋め込むインタラクティブチャネルのタイプを選択します。 オプションには「**web チャネル**」と「**印刷チャネル**」があります。

   * **テーマ**：アダプティブフォームまたはインタラクティブ通信のコンポーネントのスタイルを定義するテーマを選択します。スタイル設定には、フォントスタイル、背景色、サイズ、配置など、外観のプロパティが含まれます。

1. 「![done_icon](assets/done_icon.png)」をタップして、変更内容を保存します。これで、アダプティブフォームまたはインタラクティブ通信がページに埋め込まれました。

## 埋め込まれたアダプティブフォームとインタラクティブ通信を公開する {#publish-embedded-adaptive-form-and-interactive-communication}

ここでは、AEM Sites ページに埋め込まれたアセット（アダプティブフォームまたはインタラクティブ通信）を公開する際における、次のようなシナリオを考えてみます。

* 初めて AEM Sites ページを公開する場合で、かつアダプティブフォームやインタラクティブ通信が埋め込まれている場合は、Sites ページに加え、埋め込みアセットも公開します。
* 公開済み Sites ページに埋め込まれたアダプティブフォームまたはインタラクティブ通信のみを変更した場合は、元のアセットを公開します。変更内容は、公開された Sites ページに反映されます。公開された Sites ページにはアセットへの参照情報が含まれているため、ページを再公開する必要はありません。
* Sites ページに加え、埋め込まれたアダプティブフォームやインタラクティブ通信を変更した場合は、Sites ページと埋め込みアセットを再公開します。

## 埋め込まれたアダプティブフォームとインタラクティブ通信を変更する {#modify-embedded-adaptive-form-and-interactive-communication}

AEM Sites ページには、AEM Forms コンテナ内のアダプティブフォームおよびインタラクティブ通信への参照情報が保持されます。したがって、元のアダプティブフォームおよびインタラクティブ通信で設定されているすべての構成や特性（テーマ、スタイル、送信アクションなど）は、埋め込まれた形で保持されます。

埋め込まれたアダプティブフォームおよびインタラクティブ通信の構成やプロパティを変更するには、次のいずれかの操作を行います。

* アダプティブフォームまたはインタラクティブ通信の元のフォームをそれぞれエディターで開き、修正します。
* 編集モードで開いた Sites ページ内からアダプティブフォームまたはインタラクティブ通信をタップし、続けて「**新しいウィンドウで編集**」をタップします。元のフォームが編集モードで開きます。

## 注意点とベストプラクティス {#considerations-and-best-practices}

AEM サイトページにアダプティブフォームを埋め込む際は、以下の点に留意してください。

* 元のフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ユーザードラフトと埋め込みフォームの送信はサポートされており、フォームポータル上の「下書き」タブや「送信済みフォーム」タブに表示されます。
* 元のフォームに構築された送信アクションは、埋め込まれたフォームでも保持されます。
* 元のフォームに構築されたのエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたフォームでは動作しません。ただし、ユーザープロファイルに基づいて異なるフォームを表示するよう、Sites ページ上でエクスペリエンスのターゲット設定を使用することはできます。
* 元のフォームに Adobe Analytics が設定されている場合、埋め込まれたフォームの分析データは Adobe Analytics でキャプチャされます。ただし、フォームの分析レポートでは使用できません。
