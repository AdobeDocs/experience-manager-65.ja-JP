---
title: チュートリアル - 最初のインタラクティブ通信を作成する
description: 最初のインタラクティブ通信の作成方法を説明します。
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
feature: Interactive Communication
exl-id: b20bb719-5686-466e-8dde-279b8471bfe3
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 27%

---

# チュートリアル：最初のインタラクティブ通信を作成する {#tutorial-create-your-first-interactive-communication}

最初のインタラクティブ通信の作成方法を説明します。

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

Interactive Communications は、ビジネス通信、ドキュメント、声明書、マーケティングメール、請求書、ウェルカムキットなど、安全でパーソナライズされたインタラクティブな通信の作成、アセンブリ、配信を一元化および管理します。 インタラクティブ通信は、印刷チャネルと Web チャネルの 2 つのチャネルを使用して配信できます。 印刷チャネルはPDFや紙のコミュニケーションを作成するために使用され、Web チャネルはオンラインエクスペリエンスを提供するために使用されます。

このチュートリアルでは、インタラクティブ通信を作成するためのエンドツーエンドのフレームワークを提供します。 このチュートリアルは、1 つのユースケースと複数のガイドで構成されています。各ガイドでは、インタラクティブ通信を作成するための構築ブロックとして使用される機能を作成する方法について説明します。

次の図は、インタラクティブ通信の作成に必要な構築ブロックを示しています。

![ワークフロー](assets/workflow.gif)

このチュートリアルを完了すると、次の操作を実行できるようになります。

* 構築ブロック（フォームデータモデル、ドキュメントフラグメント、テンプレート）の作成
* インタラクティブ通信の作成
* インタラクティブ通信のテストと公開

## ユースケース {#use-case}

このジャーニーは、まず使用例を学ぶことから始まります。

通信事業者は月々の請求を E メールで顧客に送信します。 請求書はインタラクティブ通信です。 E メールには以下が含まれます。

* パスワードで保護されたPDF（このチュートリアルでは印刷チャネルと呼ばれます）。 顧客の詳細、請求書の詳細、料金の概要、請求書の支払い方法、使用状況の詳細が含まれます。
* Web 版の請求書へのリンク。このチュートリアルでは Web チャネルと呼ばれます。 請求書の Web 版は、PDF 版が網羅している詳細に加えて、使用状況のグラフィック表示と、Adobe Target に基づいてパーソナライズされたオファーを提供します。Web 版にはオンライン支払いフォームも含まれます。IC を離れることなく、オンラインでの支払いを行うのに役立ちます。
* 付加価値のあるサービス（オンラインストレージ、音楽の購読、オンデマンドビデオの購読など）へのリンク。

## 前提条件 {#prerequisites}

* AEM オーサーインスタンスを設定します。
* [AEM Forms アドオン](/help/forms/using/installing-configuring-aem-forms-osgi.md)をオーサーインスタンスにインストールします。
* MySQL データベースを設定します。
* JDBC データベースドライバー（JAR ファイル）をデータベースプロバイダーから取得します。このチュートリアルに記載されている例は、MySQL データベースに基づいています。これらの例では、Oracle の [MySQL JDBC データベースドライバー](https://dev.mysql.com/downloads/connector/j/5.1.html)を使用しています。

## 手順 1：インタラクティブ通信の計画 {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

インタラクティブ通信を計画する際の最初の手順は、インタラクティブ通信のコンテンツを最終化することです。 コンテンツが確定したら、そのコンテンツを分析して、インタラクティブ通信の作成に必要な様々なアセットタイプを特定する必要があります。

**ゴール：**

以下のデータ入力モードでインタラクティブ通信の分析を作成します。

* 静的テキスト
* フォームデータモデル
* エージェント UI
* 条件付きデータ
* 画像

[](/help/forms/using/planning-interactive-communications.md)

## 手順 2：フォームデータモデルを作成する {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

フォームデータモデルを使用すると、インタラクティブ通信を複数の異なるデータソースに接続することができます。 例えば、AEMユーザープロファイル、RESTful Web サービス、SOAP ベースの Web サービス、OData サービス、リレーショナルデータベースなどです。 フォームデータモデルは、接続されたデータソースで使用できるビジネスエンティティとサービスの統合データ表現スキーマです。 フォームデータモデルをインタラクティブ通信と共に使用して、接続されたデータソースからデータを取得することができます。 フォームデータモデルの詳細情報については、「[AEM Forms のデータ統合機能](/help/forms/using/data-integration.md)」を参照してください。

**ゴール：**

* データベースインスタンス（MySQL データベース）をデータソースとして設定する
* MySQL データベースをデータソースとして使用してフォームデータモデルを作成する
* データモデルオブジェクトをフォームデータモデルに追加する
* フォームデータモデルの読み取りサービスと書き込みサービスを設定する
* データモデルオブジェクト間の関連付けの作成
* 自動生成されたサンプルデータを表示
* サンプルデータを編集する
* テストデータを使用して、フォームデータモデルと設定済みサービスをテストする

[](/help/forms/using/create-form-data-model0.md)

## 手順 3：ドキュメントフラグメントの作成 {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

ドキュメントフラグメントは、インタラクティブ通信の作成に使用される通信の再利用可能なコンポーネントです。 ドキュメントフラグメントのタイプは、テキスト、リスト、条件です。

**ゴール：**

* ドキュメントフラグメントの作成
* 変数の作成
* ルールの作成と適用

[](/help/forms/using/create-document-fragments.md)

## 手順 4：テンプレートを作成する {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

インタラクティブ通信を作成するには、AEMサーバー上で印刷チャネルと Web チャネル用のテンプレートを使用できる必要があります。

印刷チャネルのテンプレートは、AdobeForms Designer で作成され、AEMサーバーにアップロードされます。 その後、これらのテンプレートは、インタラクティブ通信の作成時に使用できます。

Web チャネルのテンプレートは、AEMで作成されます。 テンプレートの作成者と管理者は、Web テンプレートの作成、編集、有効化をおこなうことができます。 作成して有効にすると、インタラクティブ通信の作成時にこれらのテンプレートを使用できるようになります。

**ゴール：**

* AdobeForms Designer を使用した印刷チャネル用の XDP テンプレートの作成
* XDP テンプレートのAEM Forms Server へのアップロード
* Web チャネル用のテンプレートの作成と有効化

[](/help/forms/using/create-templates-print-web.md)

## 手順 5：インタラクティブ通信を作成する {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Web 版のフォームデータモデル、ドキュメントフラグメント、テンプレートなど、すべての構築ブロックを作成したら、インタラクティブ通信の作成を開始できます。

インタラクティブ通信は、印刷チャネルと Web チャネルの 2 つのチャネルを通じて配信できます。 印刷チャネルをマスターとして使用してインタラクティブ通信を作成することもできます。 Web チャネルのマスターとして印刷オプションを使用すると、Web チャネルのコンテンツ、継承、データ連結が印刷チャネルから派生するようになります。

**ゴール：**

* 印刷チャネル用のインタラクティブ通信の作成
* Web チャネル用のインタラクティブ通信の作成
* 印刷と Web のインタラクティブ通信を作成し、印刷をマスター
* Web 版のインタラクティブ通信で動的テーブルを作成する
* Web 版のインタラクティブ通信でグラフを作成する
* Web 版インタラクティブ通信でハイパーリンクを作成する

[](/help/forms/using/create-interactive-communication0.md)

## 手順 6：インタラクティブ通信を公開する {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

印刷チャネルと Web チャネルを使用してインタラクティブ通信を作成およびテストした後、これらのアセットを公開できます。 このチュートリアルで説明する使用例では、これらのアセットを電子メールクライアントに統合する方法に焦点を当てています。 電子メールクライアントは、複数の電子メールアドレスにインタラクティブ通信を送信するためのブリッジとして機能します。

**ゴール：**

* インタラクティブ通信を電子メールクライアントと統合して、顧客に通信を送信できるようにする
* PDFドキュメントを添付ファイルとして含める（印刷チャネルで作成されたインタラクティブ通信）
* インタラクティブ通信の Web バージョンへのリンクを含める
