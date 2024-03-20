---
title: チュートリアル - 最初のインタラクティブ通信を作成する
description: 最初のインタラクティブ通信の作成方法を説明します。
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
feature: Interactive Communication
exl-id: b20bb719-5686-466e-8dde-279b8471bfe3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 100%

---

# チュートリアル：最初のインタラクティブ通信を作成する {#tutorial-create-your-first-interactive-communication}

最初のインタラクティブ通信の作成方法を説明します。

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

インタラクティブ通信を使用すると、業務上の書簡、ドキュメント、取引明細書、マーケティング用メール、請求書、ウェルカムキットなど、様々な通信記録の作成と配信を、カスタマイズされた安全な方法で一元的に管理することができます。インタラクティブ通信は、印刷チャネルと web チャネルという 2 つのチャネルを使用して配信することができます。印刷チャネルは、PDF や紙ベースの通信手段を作成する場合に使用され、web チャネルは、オンライン情報を配信する場合に使用されます。

このチュートリアルでは、インタラクティブ通信を作成するためのエンドツーエンドのフレームワークについて説明します。このチュートリアルは、1 つのユースケースと複数のガイドで構成されています。各ガイドは、インタラクティブ通信を作成する構築ブロックとして使用される機能の作成に役立ちます。

以下の画像は、インタラクティブ通信を作成するために必要な構築ブロックを表しています。

![ワークフロー](assets/workflow.gif)

このチュートリアルを完了すると、次の操作を実行できるようになります。

* 構築ブロックを作成する（フォームデータモデル、ドキュメントフラグメント、テンプレート）
* インタラクティブ通信の作成
* インタラクティブ通信をテストしてパブリッシュする

## ユースケース {#use-case}

最初に、このチュートリアルで使用するユースケースについて説明します。

通信会社が月々の請求書をお客様にメールで送信します。この請求書がインタラクティブ通信です。メールには以下が含まれます。

* 本チュートリアルで印刷チャネルと呼ばれている、パスワードで保護された PDF。顧客情報、請求書の詳細、請求概要、便利なお支払い方法、使用状況などが含まれます。
* 本チュートリアルで web チャネルと呼ばれている、web 版請求書へのリンク。請求書の Web 版は、PDF 版が網羅している詳細に加えて、使用状況のグラフィック表示と、Adobe Target に基づいてパーソナライズされたオファーを提供します。Web 版にはオンライン支払いフォームも含まれます。フォームを使うと、IC から離れることなくオンライン決済を行えます。
* オンラインストレージ、音楽配信サービス、オンデマンド動画配信サービスなどの付加価値サービスへのリンク。

## 前提条件 {#prerequisites}

* AEM オーサーインスタンスを設定します。
* [AEM Forms アドオン](/help/forms/using/installing-configuring-aem-forms-osgi.md)をオーサーインスタンスにインストールします。
* MySQL データベースを設定します。
* JDBC データベースドライバー（JAR ファイル）をデータベースプロバイダーから取得します。このチュートリアルに記載されている例は、MySQL データベースに基づいています。これらの例では、Oracle の [MySQL JDBC データベースドライバー](https://dev.mysql.com/downloads/connector/j/5.1.html)を使用しています。

## 手順 1：インタラクティブ通信の計画 {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

インタラクティブ通信の計画の第一歩は、インタラクティブ通信の内容を確定することです。内容が確定したら、内容を分析してインタラクティブ通信の作成に必要な各種アセットタイプを特定する必要があります。

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

フォームデータモデルにより、インタラクティブ通信を複数の異なるデータソースに接続することができます。例えば、AEM ユーザープロファイル、RESTful web サービス、SOAP ベースの web サービス、OData サービス、関連データベースなどに接続することができます。フォームデータモデルは、接続されたデータソースで使用可能なビジネスエンティティとサービスの統一されたデータ表現スキーマです。フォームデータモデルをインタラクティブ通信とともに使用すると、接続されたデータソースからデータを取得することができます。フォームデータモデルの詳細情報については、「[AEM Forms のデータ統合機能](/help/forms/using/data-integration.md)」を参照してください。

**ゴール：**

* データベースインスタンス（MySQL データベース）をデータソースとして設定する
* MySQL データベースをデータソースとして使用して、フォームデータモデルを作成
* データモデルオブジェクトをフォームデータモデルに追加する
* フォームデータモデルの読み取りサービスと書き込みサービスを設定する
* データモデルオブジェクトの間で関連性を作成
* 自動生成されたサンプルデータを表示
* サンプルデータを編集する
* テストデータを使用して、フォームデータモデルと設定済みサービスをテストする

[](/help/forms/using/create-form-data-model0.md)

## 手順 3：ドキュメントフラグメントの作成 {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

ドキュメントフラグメントとは再利用可能な通信のコンポーネントを指し、インタラクティブ通信の作成に使用されます。ドキュメントフラグメントのタイプとして、テキスト、リスト、および条件があります。

**ゴール：**

* ドキュメントフラグメントを作成
* 変数の作成
* ルールの作成と適用

[](/help/forms/using/create-document-fragments.md)

## 手順 4：テンプレートを作成する {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

インタラクティブ通信を作成するには、AEM サーバーに用意されている印刷チャネルと web チャネル用のテンプレートを入手する必要があります。

印刷チャネルのテンプレートは Adobe Forms Designer で作成されて、AEM サーバーにアップロードされます。これらのテンプレートはインタラクティブ通信を作成する際に使用できるようになります。

Web チャネル用のテンプレートは AEM で作成されます。テンプレートの作成者と管理者は、web テンプレートの作成、編集、有効化を行うことができます。作成して有効化されたテンプレートは、インタラクティブ通信を作成する際に使用できるようになります。

**ゴール：**

* Adobe Forms Designer を使用して印刷チャネル用の XDP テンプレートを作成
* AEM Forms サーバーに XDP テンプレートをアップロード
* Web チャネル用のテンプレートを作成し有効にする

[](/help/forms/using/create-templates-print-web.md)

## 手順 5：インタラクティブ通信を作成する {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

フォームデータモデル、ドキュメントフラグメント、web 版用のテンプレートなどのすべての構築ブロックの作成が終わったら、インタラクティブ通信の作成を開始できます。

インタラクティブ通信は、印刷チャネルと web チャネルという 2 つのチャネルを使用して配信することができます。また、印刷チャネルをメインとしてインタラクティブ通信を作成することも可能です。印刷チャネルを web チャネルのメインとして使用すると、web チャネルに連結されたコンテンツ、継承設定、データが印刷チャネルから取得されます。

**ゴール：**

* 印刷チャネル用のインタラクティブ通信を作成
* Web チャネル用のインタラクティブ通信を作成
* 印刷をメインとする印刷版および web 版インタラクティブ通信を作成
* Web 版インタラクティブ通信で動的テーブルを作成
* Web 版インタラクティブ通信でグラフを作成
* Web 版インタラクティブ通信でハイパーリンクを作成する

[](/help/forms/using/create-interactive-communication0.md)

## 手順 6：インタラクティブ通信を公開する {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

印刷チャネルおよび Web チャネルでインタラクティブ通信を作成しテストし終えたら、これらのアセットをパブリッシュすることができます。チュートリアルで紹介されているユースケースは、これらのアセットとメールクライアントの統合にフォーカスしています。メールクライアントは、インタラクティブ通信を複数のメールアドレスに送信する橋の役割を果たします。

**ゴール：**

* インタラクティブ通信をメールクライアントと統合し、通信をお客様に送信できるようにする
* PDF ドキュメントを添付ファイルとして含める（印刷チャネルで作成したインタラクティブ通信）
* Web 版インタラクティブ通信へのリンクを含める
