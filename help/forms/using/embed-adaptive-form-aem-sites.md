---
title: AEM サイトページへのアダプティブフォームまたはインタラクティブ通信の埋め込み
seo-title: AEM サイトページへのアダプティブフォームまたはインタラクティブ通信の埋め込み
description: アダプティブフォームを AEM サイトページに埋め込むことができます。ユーザーは、サイトのページから移動することなくフォームを記入および送信できます。
seo-description: アダプティブフォームを AEM サイトページに埋め込むことができます。ユーザーは、サイトのページから移動することなくフォームを記入および送信できます。
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 71%

---


# AEM サイトページへのアダプティブフォームまたはインタラクティブ通信の埋め込み {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## 概要 {#overview}

AEM Forms を使用すると、フォーム開発者は AEM サイトページまたは AEM の外側にホストされた Web ページにアダプティブフォームおよびインタラクティブ通信をシームレスに埋め込むことができます。埋め込まれたアダプティブフォームおよびインタラクティブ通信ではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームの記入および送信を行えます。これにより、ユーザーは Web ページのその他のエレメントとのコンテキストを保ったまま、同時にフォームまたはインタラクティブ通信の操作を行うことができます。

For information about embedding an adaptive form in an external web page, see [Embed adaptive form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md).

AEM Sitesページでは、次を使用して、アダプティブフォームまたはインタラクティブな通信を追加できます。

* **[AEM Form コンテナコンポーネント](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)** AEM Forms では、サイトページに追加できるコンポーネントを提供します。AEM Form コンテナコンポーネントを使用することで、アダプティブフォームやインタラクティブ通信を埋め込むことが可能になります。

* **[アセットブラウザー](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)** 作成したフォームやインタラクティブ通信は、すべて「アセット」の下に表示されます。フォームは、アセットとしてページ上にドラッグ＆ドロップすることができます。

## 前提条件 {#prerequisites}

編集可能なテンプレートを使用するAEMサイトページにアダプティブフォームやインタラクティブな通信を埋め込むには、AEM Formコンポーネントが関連付けられたテンプレートで許可コンポーネントとして設定されていることを確認します。 For more information, see **Policy &amp; Properties (Layout Container)** section in [Creating Page Templates](/help/sites-authoring/templates.md).

サイトページがスタティックテンプレートを使用している場合は、それをサイトページの段落システムから設定する必要があります。詳しくは、[デザインモードでのコンポーネントの設定](/help/sites-authoring/default-components-designmode.md)を参照してください。

## Embedding an adaptive form or interactive communication {#af-component}

AEM Forms コンテナコンポーネントを使用してアダプティブフォームやインタラクティブ通信を埋め込むには：

1. アダプティブフォームやインタラクティブ通信を埋め込む AEM サイトページを、編集モードで開きます。
1. コンポーネントブラウザーパネルからそのページ上に AEM Forms コンテナコンポーネントをドラッグアンドドロップします。

   または、アセットブラウザーでアダプティブフォームまたはインタラクティブ通信を検索して、AEM サイトページにドラッグアンドドロップします。これにより、AEM Forms コンテナにフォームが埋め込まれます。

   >[!NOTE]
   >
   >1 つのページ上の複数の AEM Form コンテナコンポーネントはサポートされていません。

1. Tap the embedded AEM Forms Container component in the sites page, and then tap ![settings_icon](assets/settings_icon.png) on the action bar. The **[!UICONTROL Edit AEM Forms Container]** dialog opens.
1. AEM Forms コンテナを編集ダイアログで、次の設定を行います。

   * **アセットの種類：**&#x200B;埋め込むアセットの種類を選択します。選択肢はアダプティブフォームとインタラクティブ通信です。
   * **Asset Path**:埋め込むアダプティブフォームまたはインタラクティブな通信を参照して選択します。 また、アセットブラウザーからドロップすると、自動的に入力されます。
   * (Adaptive form only) **Post Submission**: Select the action to trigger on form submission. お礼のメッセージを表示するため、「ありがとうございます」ページを設けることができます。

      * **ありがとうございますメッセージ**:フォーム送信時に表示するメッセージをリッチテキストエディターを使用して作成します。 このオプションは、「ありがとうございます」メッセージの表示を選択した場合にのみ使用できます。
      * **「ありがとうございます」ページ**:フォームの送信時に表示するページを参照して選択します。 このオプションは、「ありがとうございます」ページの表示を選択した場合にのみ使用できます。
      * **送信時にページを更新**：アダプティブフォームが埋め込まれたページを更新して「ありがとうございます」ページを表示します。この機能が無効な場合は、AEM Forms コンテナ内のアダプティブフォームの代わりに「ありがとうございます」ページが（ページの更新を待たずに）表示されます。このオプションは、「ありがとうございます」ページの表示を選択した場合にのみ使用できます。
   * **テーマ：**&#x200B;アダプティブフォームまたはインタラクティブ通信のコンポーネントのスタイルを定義するテーマを選択します。スタイル設定には、フォントスタイル、背景色、サイズ、配置など、外観のプロパティが含まれます。
   * **高さ**：コンテナの高さを指定します。自動でコンテナのサイズを調整するには、空白のままにします。
   * **CSS クライアントライブラリ**：CSS クライアントライブラリへのパスを指定します。


1. 設定を保存します。これで、アダプティブフォームまたはインタラクティブな通信がページに埋め込まれます。

## Publishing embedded adaptive form and interactive communication {#publishing-embedded-adaptive-form-and-interactive-communication}

ここでは、AEM サイトページに埋め込まれたアセット（アダプティブフォームまたはインタラクティブ通信）を発行する際における、次のようなシナリオを考えてみます。

* 初めて AEM サイトページを発行する場合で、かつアダプティブフォームやインタラクティブ通信が埋め込まれている場合は、サイトページに加え、埋め込みアセットも発行します。
* 発行済みサイトページに埋め込まれたアダプティブフォームまたはインタラクティブな通信のみを変更した場合は、元のアセットを発行し、変更内容は発行済みサイトページに反映されます。 発行されたサイトページにはアセットへの参照情報が含まれているため、ページを再発行する必要はありません。
* サイトページに加え、埋め込まれたアダプティブフォームやインタラクティブ通信を変更した場合は、サイトページと埋め込みアセットを再発行します。

## Modifying embedded adaptive form and interactive communication {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM サイトページには、AEM Forms コンテナ内のアダプティブフォームおよびインタラクティブ通信への参照情報が保存されます。したがって、元のアダプティブフォームおよびインタラクティブ通信で構成されているすべての構成や特性（テーマ、スタイル、送信アクションなど）は、埋め込まれた形で保持されます。

埋め込まれたアダプティブフォームおよびインタラクティブ通信の構成やプロパティを変更するには、次のいずれかの操作を行います。

* アダプティブフォームまたはインタラクティブ通信の元のフォームをそれぞれエディターで開き、修正します。
* Tap the adaptive form or interactive communication from within the site page in edit mode and then tap **[!UICONTROL Edit in a new window]**. 元のフォームは、修正可能な編集モードで開きます。

>[!NOTE]
>
>元のアダプティブフォームまたはインタラクティブ通信に加えた変更は、埋め込まれたフォームに自動的に反映されます。ただし、発行済みページに変更内容を反映するには、アダプティブフォーム、インタラクティブ通信またはサイトページを再発行する必要があります。

## 注意点とベストプラクティス {#considerations-and-best-practices}

AEM サイトページにアダプティブフォームを埋め込む際は、以下の点に留意してください。

* 元のフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ユーザードラフトと埋め込みフォームの送信はサポートされており、フォームポータル上の「下書き」タブや「送信済みフォーム」タブに表示されます。
* 元のフォームに構築された送信アクションは、埋め込まれたフォームでも保持されます。
* 元のフォームに構築されたのエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたフォームでは動作しません。ただし、ユーザープロファイルに基づいて異なるフォームを表示するよう、サイトページ上でエクスペリエンスのターゲット設定を使用することはできます。
* 元のフォームに対してAdobe Analyticsが設定している場合、埋め込まれたフォームの分析データはAdobe Analyticsで取得されます。 ただし、フォームの分析レポートでは使用できません。

