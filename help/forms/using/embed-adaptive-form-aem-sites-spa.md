---
title: AEM Sitesシングルページアプリケーションにアダプティブフォームまたはインタラクティブ通信を埋め込む
seo-title: AEM Sitesページへのアダプティブフォームまたはインタラクティブ通信の埋め込み
description: AEM Sitesページにアダプティブフォームまたはインタラクティブ通信を埋め込む。 ユーザーは、サイトページから離れることなく、フォームに記入して送信できます。
seo-description: アダプティブフォームまたはインタラクティブ通信は、AEM Sitesページに埋め込むことができます。 ユーザーは、サイトページから離れることなく、フォームに記入して送信できます。
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: アダプティブフォーム
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 13%

---

# AEM Sitesシングルページアプリケーションにアダプティブフォームまたはインタラクティブ通信を埋め込む{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概要 {#overview}

AEM Formsを使用すると、フォーム開発者はアダプティブフォームとインタラクティブ通信をAEM Sitesシングルページアプリケーション(SPA)にシームレスに埋め込むことができます。 埋め込まれたアダプティブフォームとインタラクティブ通信は完全に機能し、ユーザーはページを離れることなくフォームに入力して送信できます。 これにより、ユーザーはWebページ上の他の要素のコンテキストを維持し、アダプティブフォームやインタラクティブ通信と同時にやり取りすることができます。

AEM Sitesシングルページアプリケーションでは、[AEM Forms SPAコンテナコンポーネント](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[を使用して、アダプティブフォームまたはインタラクティブ通信を追加できます。](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) AEM Sites SPA用のAEM Formsコンポーネントで、サイトページに追加できます。

SPA AEM Sites以外でのアダプティブフォームの埋め込みについて詳しくは、「 AEM Sitesページにアダプティブフォームまたはインタラクティブ通信を埋め込む」を参照してください。[](/help/forms/using/embed-adaptive-form-aem-sites.md)

## 前提条件 {#prerequisites}

AEM Forms SPAコンテナコンポーネントを使用して、AEMサイトSPAにアダプティブフォームまたはインタラクティブ通信を埋め込むには、以下がインストールされていることを確認します。

* Java SE開発キット8以降
* Apache Maven 3.3.1以降
* AEMオーサーインスタンス
* [AEM Forms 6.4.2アドオンパッケージオーサー](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) インスタンス

## AEM Forms SPA Containerコンポーネント{#install-aem-forms-spa-container-component}のインストール

次の手順を実行して、AEM Forms SPAコンテナコンポーネントをインストールします。

1. [SPA ](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa)用のAEM Formsコンポーネントのクローンを作成するか、ダウンロードします。
1. SPA用のAEM Formsコンポーネントをインストールします。 コンポーネントのインストール手順は、 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component)ファイルに記載されています。

   このコンポーネントには、SPAコンテナコンポーネントをReactベースのSPAプロジェクトと統合するために使用できる、[サンプルのReactコンポーネント](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component)が含まれています。

1. [ReactベースのSPAプロジェクトのクローンまたはダウンロード](https://github.com/adobe/aem-sample-we-retail-journal)を行います。
1. [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor)ファイルの手順を使用して、SPAコンテナコンポーネントをReactベースのSPAプロジェクトに統合します。

   AEM Forms SPA Containerコンポーネントをインストールし、そのコンポーネントをReactベースのSPAプロジェクトに統合した後、AEM Sitesページにアダプティブフォームとインタラクティブ通信を埋め込むことができます。

## アダプティブフォームまたはインタラクティブ通信を埋め込む{#af-component}

AEM Forms for SPA Containerコンポーネントを使用してアダプティブフォームまたはインタラクティブ通信を埋め込むには：

1. アダプティブフォームまたはインタラクティブ通信を埋め込むAEMサイトページを編集モードで開きます。
1. 次のいずれかのオプションを使用して、**SPA用AEM Form**&#x200B;コンポーネントをページに挿入します。

   * Sitesページのレイアウトコンテナをタップし、**+**&#x200B;をタップして、**SPA用AEMフォーム**&#x200B;コンポーネントを選択します。

   * コンポーネントブラウザーパネルから、**AEM Form for SPA**&#x200B;コンポーネントをページにドラッグ&amp;ドロップします。
   * アセットブラウザーでアダプティブフォームまたはインタラクティブ通信を検索し、サイトページにドラッグ&amp;ドロップします。 これにより、フォームがSPA用AEM Formsコンポーネントコンテナに埋め込まれます。

   >[!NOTE]
   >
   >1つのページでの複数のAEM Forms SPA Containerコンポーネントのレンダリングはサポートされていません。 1つのページに複数のAEM Forms SPAコンテナを設定できますが、一度にレンダリングされるコンポーネントは1つだけです。 不一致を避けるために、1つのページに1つのコンポーネントのみが表示されるようにします。

1. サイトページに埋め込まれたAEM Forms SPAコンテナコンポーネントをタップし、アクションバーの![settings_icon](assets/settings_icon.png)をタップします。 **AEM Forms SPAコンテナを編集**&#x200B;ダイアログが開きます。
1. **AEM Formsコンテナを編集**&#x200B;ダイアログで、次の情報を指定します。

   * **アセットのタイプ：**&#x200B;埋め込むアセットのタイプを選択します。オプションは&#x200B;**アダプティブフォーム**&#x200B;と&#x200B;**インタラクティブ通信**&#x200B;です。

   * **アセットパス**:埋め込むアダプティブフォームまたはインタラクティブ通信を参照して選択します。アダプティブフォームまたはインタラクティブ通信がアセットブラウザーを使用して挿入されると、このフィールドに値が自動入力されます。
   * **チャネル** （インタラクティブ通信のみ）:埋め込むインタラクティブチャネルのタイプを選択します。オプションは&#x200B;**Webチャネル**&#x200B;と&#x200B;**印刷チャネル**&#x200B;です。

   * **テーマ**:アダプティブフォームまたはインタラクティブ通信のコンポーネントのスタイルを定義するテーマを選択します。スタイル設定には、フォントスタイル、背景色、サイズ、配置など、外観のプロパティが含まれます。

1. ![done_icon](assets/done_icon.png)をタップして設定を保存します。 アダプティブフォームまたはインタラクティブ通信がページに埋め込まれます。

## 埋め込まれたアダプティブフォームとインタラクティブ通信を発行する{#publish-embedded-adaptive-form-and-interactive-communication}

AEM Sitesページで埋め込みアセット（アダプティブフォームまたはインタラクティブ通信）を発行する場合、以下のシナリオを考えてみます。

* AEM Sitesページを初めて発行する場合で、アダプティブフォームやインタラクティブ通信が埋め込まれている場合は、 Sitesページと埋め込みアセットを発行します。
* 発行済みサイトページに埋め込まれたアダプティブフォームまたはインタラクティブ通信のみを変更した場合は、元のアセットを発行し、変更内容が発行済みサイトページに反映されます。 公開済みのサイトページにはアセットへの参照が含まれており、ページを再公開する必要はありません。
* サイトページと、埋め込まれたアダプティブフォームまたはインタラクティブ通信を変更した場合は、サイトページと埋め込まれたアセットを再発行します。

## 埋め込まれたアダプティブフォームとインタラクティブ通信の変更{#modify-embedded-adaptive-form-and-interactive-communication}

AEMのサイトページには、AEM Formsコンテナ内のアダプティブフォームとインタラクティブ通信への参照情報が保持されます。 したがって、元のアダプティブフォームとインタラクティブ通信で設定されているテーマ、スタイル、送信アクションなどの設定とプロパティは、埋め込まれたアダプティブフォームとインタラクティブ通信ですべて保持されます。

埋め込まれたアダプティブフォームとインタラクティブ通信の設定またはプロパティを変更するには、次のいずれかの操作を行います。

* 元のフォームをアダプティブフォームまたはインタラクティブ通信の各エディターで開き、変更します。
* 編集モードでサイトページ内からアダプティブフォームまたはインタラクティブ通信をタップし、新しいウィンドウで「**編集**」をタップします。 元のフォームが編集モードで開きます。

## 注意点とベストプラクティス {#considerations-and-best-practices}

AEM サイトページにアダプティブフォームを埋め込む際は、以下の点に留意してください。

* 元のフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ユーザードラフトと埋め込みフォームの送信はサポートされており、フォームポータル上の「下書き」タブや「送信済みフォーム」タブに表示されます。
* 元のフォームに構築された送信アクションは、埋め込まれたフォームでも保持されます。
* 元のフォームに構築されたのエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたフォームでは動作しません。ただし、サイトページでエクスペリエンスのターゲット設定を使用して、ユーザープロファイルに基づいて異なるフォームを表示できます。
* 元のフォームに Adobe Analytics が設定されている場合、埋め込まれたフォームの分析データは Adobe Analytics でキャプチャされます。ただし、フォームの分析レポートでは使用できません。
