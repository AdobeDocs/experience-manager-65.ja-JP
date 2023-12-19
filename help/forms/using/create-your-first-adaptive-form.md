---
title: 「チュートリアル：最初のアダプティブフォームを作成する」
description: ここでは、インタラクティブでレスポンシブな高機能のフォームを作成する方法について説明します。
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 100%

---

# チュートリアル：最初のアダプティブフォームを作成 {#tutorial-create-your-first-adaptive-form}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=ja) |
| AEM 6.5 | この記事 |


![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## はじめに {#introduction}

登録を簡素化し、エンゲージメントを高め、作業時間を削減できる、モバイル対応の&#x200B;**フォームエクスペリエンス**&#x200B;をお求めの場合には、**アダプティブフォーム**&#x200B;が最適です。アダプティブフォームは、モバイル、自動化、分析に適したフォームエクスペリエンスを提供します。レスポンシブでインタラクティブな特性を持つフォームを簡単に作成することができます。自動化されたプロセスを使用して管理業務や繰り返しの作業を減らし、データ分析機能により、顧客がこのフォームで体験するエクスペリエンスを改善してパーソナライズすることができます。

このチュートリアルでは、アダプティブフォームを作成するためのエンドツーエンドのフレームワークについて説明します。このチュートリアルは、1 つのユースケースと複数のガイドで構成されています。それぞれのガイドでは、このチュートリアルで作成するアダプティブフォームと、このアダプティブフォームに追加する新しい機能について説明します。すべてのガイドが終了した後、使用可能なアダプティブフォームが得られます。アダプティブフォームを作成するためのガイドも用意されています。続きのガイドは、間もなく公開する予定です。このチュートリアルを完了すると、次の操作を実行できるようになります。

* アダプティブフォームとフォームデータモデルを作成する。
* アダプティブフォームのスタイルを設定する。
* アダプティブフォームのルールエディターを使用して、ビジネスルールを作成する。
* アダプティブフォームをテストして公開する。

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

最初に、このチュートリアルで使用するユースケースについて説明します。

Web サイトでは、さまざまな顧客向けに幅広い製品を提供しています。顧客がポータルを参照し、製品を選択して注文します。すべての顧客がアカウントを作成し、配送先と請求先の住所を提供します。既存の顧客である Sara Rose は、Web サイトに配送先住所を追加しようとしています。この web サイトには、配送先住所を追加および更新できるオンラインフォームが用意されています。

この web サイトは Adobe Experience Manager（AEM）上で稼働し、AEM [!DNL Forms] を使用してデータの取得と処理を行います。住所の追加とフォームの更新は、アダプティブフォームを使用して行います。Web サイトでは、顧客の詳細情報をデータベースに保存します。住所の追加と更新を行うフォームを使用して、有効な住所を取得して表示します。また、アダプティブフォームを使用して、更新後の住所と新しい住所を入力します。

### 前提条件 {#prerequisite}

* [AEM オーサーインスタンス](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=ja#author-and-publish-installs)の設定
* [AEM Forms アドオン](../../forms/using/installing-configuring-aem-forms-osgi.md)をオーサーインスタンスにインストールします。
* JDBC データベースドライバー（JAR ファイル）をデータベースプロバイダーから取得します。このチュートリアルに記載されている例は、[!DNL MySQL] データベースに基づいています。これらの例では、[!DNL Oracle's] [MySQL JDBC データベースドライバー](https://dev.mysql.com/downloads/connector/j/5.1.html)を使用しています。

* 以下に示すフィールドを使用して、顧客データを含むデータベースを設定します。アダプティブフォームの作成にデータベースが必須なわけではありません。このチュートリアルではデータベースを使用して、AEM [!DNL Forms] のフォームデータモデルと永続性機能を表示します。

![adaptiveformdata](assets/adaptiveformdata.png)

## 手順 1：アダプティブフォームを作成する {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

アダプティブフォームは、レスポンシブで動的な特性を持つ、柔軟性の高い次世代型の高機能なフォームです。アダプティブフォームを使用すると、パーソナライズされ、ターゲットを絞ったエクスペリエンスを提供できます。AEM [!DNL Forms] には、ドラッグ＆ドロップ操作でアダプティブフォームを作成できる WYSIWYG エディターが用意されています。アダプティブフォームについて詳しくは、「[アダプティブフォームのオーサリングの概要](../../forms/using/introduction-forms-authoring.md)」を参照してください。

ゴール:

* 顧客が配送先住所を追加するためのアダプティブフォームを作成する
* 顧客の情報を表示して保存するためのアダプティブフォームフィールドのレイアウトを設定する
* フォームコンテンツが記載されたメールを送信するためのアクションを作成する
* アダプティブフォームのプレビューと送信を行う

[![ガイドを参照してください](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## 手順 2：フォームデータモデルを作成する {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

フォームデータモデルを使用すると、アダプティブフォームを複数の異なるデータソースに接続できます。例えば、AEM ユーザープロファイル、RESTful web サービス、SOAP ベースの web サービス、OData サービス、関連データベースなどに接続することができます。フォームデータモデルは、接続されたデータソースで使用可能なビジネスエンティティとサービスの統一されたデータ表現スキーマです。フォームデータモデルをアダプティブフォームとともに使用すると、接続されたデータソースに対して、データの取得、更新、削除、追加を行うことができます。

ゴール:

* データソースとして web サイトのデータベースインスタンス（[!DNL MySQL] データベース）を設定する
* [!DNL MySQL] データベースをデータソースとして使用して、フォームデータモデルを作成する
* データモデルオブジェクトをフォームデータモデルに追加する
* フォームデータモデルの読み取りサービスと書き込みサービスを設定する
* テストデータを使用して、フォームデータモデルと設定済みサービスをテストする

[![ガイドを参照してください](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## 手順 3：アダプティブフォームのフィールドにルールを適用する {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

アダプティブフォームには、アダプティブフォームオブジェクトにルールを書き込むためのエディターが用意されています。これらのルールは、フォームオブジェクト上でトリガーできるアクションを定義します。それらのアクションは、プリセットされた条件、ユーザー入力、およびフォーム上のユーザーアクションに基づいてトリガーされます。ルールを適用することにより、フォームのフィールドに短時間で正確に情報を入力できるようになります。

ゴール:

* ルールを作成してアダプティブフォームフィールドに適用する
* ルールを使用してフォームデータモデルサービスをトリガーし、データベースのデータを更新する

[![ガイドを参照してください](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## 手順 4：アダプティブフォームのスタイルを設定する {#step-style-your-adaptive-form}

![adapative-form-styling](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

アダプティブフォームには、アダプティブフォームのテーマを作成するためのテーマと[エディター](../../forms/using/themes.md)が用意されています。テーマには、コンポーネントとパネルの詳細なスタイル設定が含まれています。様々なフォームでテーマを再利用することができます。スタイルには、背景色、状態色、透明度、配置、サイズなどのプロパティが含まれます。テーマをフォームに適用すると、指定したスタイルがフォームの対応コンポーネントに反映されます。アダプティブフォームは、フォームに固有のスタイルのインラインスタイル設定をサポートしています。

ゴール:

* 標準のテーマをアダプティブフォームに適用
* テーマエディターを使用して、アダプティブフォームのテーマを作成
* カスタムテーマに web フォントを使用する

[![ガイドを参照してください](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 手順 5：アダプティブフォームを公開する {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

アダプティブフォームは、スタンドアロン形式（単一ページのアプリケーション）としてパブリッシュすることも、AEM [Sites ページ](/help/forms/using/embed-adaptive-form-aem-sites.md)に含めることも、[フォームポータル](../../forms/using/introduction-publishing-forms.md)を使用して AEM [!DNL Site] にリスト表示することもできます。

ゴール:

* アダプティブフォームを AEM ページとして公開する
* アダプティブフォームを AEM [!DNL Sites] ページに埋め込む
* アダプティブフォームを外部の web ページ（AEM の外部でホストされる AEM 以外の web ページ）に埋め込む

[![ガイドを参照してください](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
