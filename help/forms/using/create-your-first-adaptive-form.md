---
title: 「チュートリアル：最初のアダプティブフォームを作成する」
description: ここでは、インタラクティブでレスポンシブな高機能のフォームを作成する方法について説明します。
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 72%

---

# チュートリアル：最初のアダプティブフォームを作成 {#tutorial-create-your-first-adaptive-form}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=ja) |
| AEM 6.5 | この記事 |


![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## はじめに {#introduction}

モバイル対応をお探しですか？ **フォームエクスペリエンス** これにより、登録が簡素化され、エンゲージメントが向上し、ターンアラウンド・タイムが短縮されます。 **アダプティブフォーム** 君にぴったりだ。 アダプティブフォームは、モバイル、自動化、分析に適したフォームエクスペリエンスを提供します。レスポンシブでインタラクティブな特性を持つフォームを簡単に作成することができます。自動化されたプロセスを使用して管理業務や繰り返しの作業を減らし、データ分析機能により、顧客がこのフォームで体験するエクスペリエンスを改善してパーソナライズすることができます。

このチュートリアルでは、アダプティブフォームを作成するためのエンドツーエンドのフレームワークについて説明します。このチュートリアルは、1 つのユースケースと複数のガイドで構成されています。それぞれのガイドでは、このチュートリアルで作成するアダプティブフォームと、このアダプティブフォームに追加する新しい機能について説明します。すべてのガイドが終了した後、使用可能なアダプティブフォームが得られます。アダプティブフォームを作成するためのガイドも用意されています。今後のガイドは近日公開予定です。 このチュートリアルを完了すると、次の操作を実行できるようになります。

* アダプティブフォームとフォームデータモデルを作成する。
* アダプティブフォームのスタイルを設定する。
* アダプティブフォームのルールエディターを使用して、ビジネスルールを作成する。
* アダプティブフォームをテストして公開する。

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

最初に、このチュートリアルで使用するユースケースについて説明します。

Web サイトでは、さまざまな顧客向けに幅広い製品を提供しています。顧客がポータルを参照し、製品を選択して注文します。すべての顧客がアカウントを作成し、配送先と請求先の住所を提供します。既存の顧客である Sara Rose は、Web サイトに配送先住所を追加しようとしています。この web サイトには、配送先住所を追加および更新できるオンラインフォームが用意されています。

この web サイトは Adobe Experience Manager（AEM）上で稼働し、AEM [!DNL Forms] を使用してデータの取得と処理を行います。住所の追加とフォームの更新は、アダプティブフォームを使用して行います。Web サイトでは、顧客の詳細情報をデータベースに保存します。住所の追加と更新を行うフォームを使用して、有効な住所を取得して表示します。また、アダプティブフォームを使用して、更新後の住所と新しい住所を入力します。

### 前提条件 {#prerequisite}

* を設定します。 [AEMオーサーインスタンス](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html#author-and-publish-installs)
* [AEM Forms アドオン](../../forms/using/installing-configuring-aem-forms-osgi.md)をオーサーインスタンスにインストールします。
* JDBC データベースドライバー（JAR ファイル）をデータベースプロバイダーから取得します。このチュートリアルに記載されている例は、[!DNL MySQL] データベースに基づいています。これらの例では、[!DNL Oracle's] [MySQL JDBC データベースドライバー](https://dev.mysql.com/downloads/connector/j/5.1.html)を使用しています。

* 以下に示すフィールドを使用して、顧客データを格納したデータベースを設定します。 アダプティブフォームの作成にデータベースが必須なわけではありません。このチュートリアルではデータベースを使用して、AEM [!DNL Forms] のフォームデータモデルと永続性機能を表示します。

![adaptiveformdata](assets/adaptiveformdata.png)

## 手順 1：アダプティブフォームを作成する {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

アダプティブフォームは、レスポンシブで動的な特性を持つ、柔軟性の高い次世代型の高機能なフォームです。アダプティブフォームを使用すると、パーソナライズされ、ターゲットを絞ったエクスペリエンスを提供できます。AEM [!DNL Forms] には、ドラッグ＆ドロップ操作でアダプティブフォームを作成できる WYSIWYG エディターが用意されています。アダプティブフォームについて詳しくは、「[アダプティブフォームのオーサリングの概要](../../forms/using/introduction-forms-authoring.md)」を参照してください。

ゴール:

* 顧客が配送先住所を追加できるアダプティブフォームを作成します。
* 顧客からの情報を表示および受け入れるためのアダプティブフォームのレイアウトフィールド。
* 送信アクションを作成して、フォームコンテンツを含む電子メールを送信します。
* アダプティブフォームをプレビューして送信します。

[![ガイドを参照してください](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## 手順 2：フォームデータモデルを作成する {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

フォームデータモデルを使用すると、アダプティブフォームを異なるデータソースに接続することができます。 例えば、AEM ユーザープロファイル、RESTful web サービス、SOAP ベースの web サービス、OData サービス、関連データベースなどに接続することができます。フォームデータモデルは、接続されたデータソースで使用可能なビジネスエンティティとサービスの統一されたデータ表現スキーマです。フォームデータモデルをアダプティブフォームとともに使用すると、接続されたデータソースに対して、データの取得、更新、削除、追加を行うことができます。

ゴール:

* Web サイトのデータベースインスタンスを設定します ([!DNL MySQL] データベース ) をデータソースとして使用します。
* を使用してフォームデータモデルを作成する [!DNL MySQL] データベースをデータソースとして使用する。
* データモデルを作成できるように、データモデルオブジェクトを追加します。
* フォームデータモデルの読み取りサービスと書き込みサービスを設定します。
* テストデータを使用して、フォームデータモデルと設定済みのサービスをテストします。

[![ガイドを参照してください](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## 手順 3：アダプティブフォームのフィールドにルールを適用する {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

アダプティブフォームには、アダプティブフォームオブジェクトにルールを書き込むためのエディターが用意されています。これらのルールは、フォームオブジェクト上でトリガーできるアクションを定義します。それらのアクションは、プリセットされた条件、ユーザー入力、およびフォーム上のユーザーアクションに基づいてトリガーされます。これにより、フォーム入力の精度を確保し、スピードを高めることができます。

目標：

* ルールを作成し、アダプティブフォームフィールドに適用する。
* ルールを使用してフォームデータモデルサービスをトリガー化し、データをデータベースに更新します。

[![ガイドを参照してください](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## 手順 4：アダプティブフォームのスタイルを設定する {#step-style-your-adaptive-form}

![adapative-form-styling](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

アダプティブフォームには、アダプティブフォームのテーマを作成するためのテーマと[エディター](../../forms/using/themes.md)が用意されています。テーマには、コンポーネントとパネルの詳細なスタイル設定が含まれています。様々なフォームでテーマを再利用することができます。スタイルには、背景色、状態色、透明度、配置、サイズなどのプロパティが含まれます。テーマをフォームに適用すると、指定したスタイルがフォームの対応コンポーネントに反映されます。アダプティブフォームは、フォームに固有のスタイルのインラインスタイル設定をサポートしています。

ゴール:

* 標準搭載のテーマをアダプティブフォームに適用します。
* テーマエディターを使用してアダプティブフォームのテーマを作成します。
* カスタムWeb Fontsでテーマを使用する。

[![ガイドを参照してください](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 手順 5：アダプティブフォームを公開する {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

アダプティブフォームは、スタンドアロン形式（単一ページのアプリケーション）としてパブリッシュすることも、AEM [Sites ページ](/help/forms/using/embed-adaptive-form-aem-sites.md)に含めることも、[フォームポータル](../../forms/using/introduction-publishing-forms.md)を使用して AEM [!DNL Site] にリスト表示することもできます。

ゴール:

* アダプティブフォームをAEM Page として発行します。
* アダプティブフォームをAEMに埋め込む [!DNL Sites] ページ。
* アダプティブフォームを外部の Web ページ (AEMの外でホストされるAEM以外の Web ページ ) に埋め込みます。

[![ガイドを参照してください](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
