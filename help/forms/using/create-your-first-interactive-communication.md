---
title: チュートリアル — 最初の対話型コミュニケーションの作成
seo-title: 最初のインタラクティブ通信を作成する
description: 最初のインタラクティブ通信の作成方法を説明します。
seo-description: 最初のインタラクティブ通信の作成方法を説明します。
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 88%

---


# チュートリアル：最初のインタラクティブ通信を作成する {#tutorial-create-your-first-interactive-communication}

最初のインタラクティブ通信の作成方法を説明します。

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

インタラクティブ通信を使用すると、業務上の書簡、ドキュメント、取引明細書、マーケティング用電子メール、請求書、ウェルカムキットなど、さまざまな通信記録の作成と配信を、カスタマイズされた安全な方法で一元的に管理することができます。インタラクティブ通信は、印刷チャネルと Web チャネルという 2 つのチャネルを使用して配信することができます。印刷チャネルは、PDF や紙ベースの通信手段を作成する場合に使用され、Web チャネルは、オンライン情報を配信する場合に使用されます。

このチュートリアルでは、インタラクティブ通信を作成するためのエンドツーエンドのフレームワークについて説明します。このチュートリアルは、1 つのユースケースと複数のガイドから構成されています。各ガイドは、インタラクティブ通信を作成する構築ブロックとして使用される機能の作成に役立ちます。

以下の画像は、インタラクティブ通信を作成するために必要な構築ブロックを表しています。

![ワークフロー](assets/workflow.gif)

このチュートリアルを完了すると、次の操作を実行できるようになります。

* 構築ブロックを作成する（フォームデータモデル、ドキュメントフラグメント、テンプレート）
* インタラクティブ通信の作成
* インタラクティブ通信をテストしてパブリッシュする

## 使用事例{#use-case}


最初に、このチュートリアルで使用するユースケースについて説明します。

通信会社が月々の請求書をお客様に電子メールで送信します。この請求書がインタラクティブ通信です。電子メールには以下が含まれます。

* 本チュートリアルで印刷チャネルと呼ばれている、パスワードで保護された PDF。顧客情報、請求書の詳細、請求概要、便利なお支払い方法、使用状況などが含まれます。
* 本チュートリアルで Web チャネルと呼ばれている、Web 版請求書へのリンク。請求書の Web 版は、PDF 版が網羅している詳細に加えて、使用状況のグラフィック表示と、Adobe Target に基づいてパーソナライズされたオファーを提供します。Webバージョンには、オンライン支払いフォームも含まれています。 フォームを使うと、IC から離れることなくオンライン決済を行えます。
* オンラインストレージ、音楽配信サービス、オンデマンド動画配信サービスなどの付加価値サービスへのリンク。

## 前提条件 {#prerequisites}

* AEM オーサーインスタンスを設定します。
* Install [AEM Forms add-on](/help/forms/using/installing-configuring-aem-forms-osgi.md) on author instance
* MySQL データベースを設定します。
* JDBC データベースドライバー（JAR ファイル）をデータベースプロバイダーから取得します。Examples in the tutorial are based on MySQL database and use Oracle&#39;s [MySQL JDBC database driver](https://dev.mysql.com/downloads/connector/j/5.1.html).

## 手順 1：インタラクティブ通信の計画 {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

インタラクティブ通信の計画の第一歩は、インタラクティブ通信の内容を確定することです。内容が確定したら、内容を分析してインタラクティブ通信の作成に必要な各種アセットタイプを特定する必要があります。

**ゴール:**

次のデータ入力モードを使用して、対話型通信の解剖学を作成する手順は、次のとおりです。

* 静的テキスト
* フォームデータモデル
* エージェント UI
* 条件付きデータ
* 画像

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/planning-interactive-communications.md)

## 手順 2：フォームデータモデルを作成する {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

フォームデータモデルにより、インタラクティブ通信を複数の異なるデータソースに接続することができます。例えば、AEM ユーザープロファイル、RESTful Web サービス、SOAP ベースの Web サービス、OData サービス、関連データベースなどに接続することができます。フォームデータモデルは、接続されたデータソースで使用可能なビジネスエンティティとサービスの統一されたデータ表現スキーマです。フォームデータモデルをインタラクティブ通信とともに使用すると、接続されたデータソースからデータを取得することができます。For more information about form data model, see [AEM Forms Data Integration](/help/forms/using/data-integration.md).

**ゴール:**

* データベースインスタンス（MySQL データベース）をデータソースとして設定する
* MySQL データベースをデータソースとして使用して、フォームデータモデルを作成する
* データモデルオブジェクトをフォームデータモデルに追加する
* フォームデータモデルの読み取りサービスと書き込みサービスを設定する
* データモデルオブジェクトの間で関連性を作成する
* 自動生成されたサンプルデータを表示する
* サンプルデータを編集する
* テストデータを使用して、フォームデータモデルと設定済みサービスをテストする

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-form-data-model0.md)

## 手順 3：ドキュメントフラグメントの作成 {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

ドキュメントフラグメントとは再利用可能な通信のコンポーネントを指し、インタラクティブ通信の作成に使用されます。ドキュメントフラグメントのタイプとして、テキスト、リスト、および条件があります。

**ゴール:**

* ドキュメントフラグメントの作成
* 変数の作成
* ルールを作成して適用

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-document-fragments.md)

## 手順 4：テンプレートの作成 {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

インタラクティブ通信を作成するには、AEM サーバーに用意されている印刷チャネルと Web チャネル用のテンプレートを入手する必要があります。

印刷チャネルのテンプレートは Adobe Forms Designer で作成されて、AEM サーバーにアップロードされます。これらのテンプレートはインタラクティブ通信を作成する際に使用できるようになります。

Web チャネル用のテンプレートは AEM で作成されます。テンプレートの作成者と管理者は、Web テンプレートの作成、編集、有効化を行うことができます。作成して有効化されたテンプレートは、インタラクティブ通信を作成する際に使用できるようになります。

**ゴール:**

* Adobe Forms Designer を使用して印刷チャネル用の XDP テンプレートを作成する
* XDP テンプレートを AEM Forms サーバーにアップロードする
* Web チャネル用のテンプレートを作成し有効化する

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-templates-print-web.md)

## 手順 5：インタラクティブ通信の作成 {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

フォームデータモデル、ドキュメントフラグメント、Web 版用のテンプレートなどのすべての構築ブロックの作成が終わったら、インタラクティブ通信の作成を開始できます。

インタラクティブ通信は、印刷チャネルと Web チャネルという 2 つのチャネルを使用して配信することができます。また、印刷チャネルをマスターとしてインタラクティブ通信を作成することも可能です。印刷チャネルを Web チャネルのマスターとして使用すると、Web チャネルに連結されたコンテンツ、継承設定、データが印刷チャネルから取得されます。

**ゴール:**

* 印刷チャネル用のインタラクティブ通信の作成
* Web チャネル用のインタラクティブ通信の作成
* 印刷をマスターとする印刷版および Web 版インタラクティブ通信の作成
* Web 版インタラクティブ通信で動的テーブルを作成する
* Web 版インタラクティブ通信でグラフを作成する
* Interactive CommunicationのWebバージョンでハイパーリンクを作成する

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-interactive-communication0.md)

## 手順 6：インタラクティブ通信をテストする {#step-test-your-interactive-communication}

![アダプティブフォームの11テスト](assets/11-test-your-adaptive-form.png)

インタラクティブ通信を作成したら、自分が行ったすべての変更をテストすることが重要です。対話型通信のすべてのフィールドをテストするのは退屈です。 AEM Formsは、WebブラウザーでのInteractive Communicationsのテストを自動化するSDK(Calvin SDK)を提供しています。

**ゴール:**

* テストスイートの作成
* テストケースの作成
* テストケースの実行

## 手順 7：インタラクティブ通信をパブリッシュする {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

印刷チャネルおよび Web チャネルでインタラクティブ通信を作成しテストし終えたら、これらのアセットをパブリッシュすることができます。チュートリアルで紹介されているユースケースは、これらのアセットと電子メールクライアントの統合にフォーカスしています。電子メールクライアントは、インタラクティブ通信を複数のメールアドレスに送信する橋の役割を果たします。

**ゴール:**

* インタラクティブ通信を電子メールクライアントと統合し、通信をお客様に送信できるようになる
* PDF 文書を添付ファイルとして含める（印刷チャネルで作成したインタラクティブ通信）
* Web 版インタラクティブ通信へのリンクを含める

