---
title: AEM Forms用語集
description: AEM Forms用語集は、Adobe Experience Manager Forms（AEM Forms）で使用される主要な用語、定義および概念の包括的な一覧で、アダプティブフォームと関連機能を理解し、操作するのに役立ちます。
feature: Adaptive Forms
role: Admin, User, Developer
hidefromtoc: true
hide: true
source-git-commit: 37f471e09c13b7ab036ab1043d11dfed98da1d97
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 2%

---

# AEM Forms用語集

## [アダプティブフォーム](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form)

ユーザーのデバイスと入力に基づいてレイアウトと表示を調整する動的なレスポンシブフォームにより、様々なプラットフォームでのユーザーエクスペリエンスが向上します。 条件付きロジック、動的データ連結、ルールベースの動作が含まれます。

## [ アダプティブフォームのバージョン管理 ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/adaptive-forms-core-components/add-versioning-reviews-comments)

JCR ノードのバージョン管理を使用して、リポジトリ内のフォームの複数のバージョンを管理する機能。 アダプティブフォームの監査証跡と簡単なロールバックを確保します。

## [Adobe Analytics Formsの統合 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation)

Adobe Analyticsを使用してユーザーのインタラクション（フィールドのドロップオフ、セクションあたりの滞在時間など）に関する詳細なインサイトを提供し、フォームデザインのデータ駆動型の最適化を可能にします。

## [AEM Forms アドオンパッケージ ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)

Adobe Experience Manager（AEM）にパッケージとしてデプロイされるアプリケーションです。これには、AEM Sling フレームワークによって管理されるサービス（API プロバイダー）およびサーブレットや JSP が含まれます。

## [JEE でのAEM Forms](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)

Java Enterprise Edition （JEE）サーバーを活用するAEM Formsのデプロイメントオプションで、エンタープライズレベルのスケーラビリティ、トランザクション管理、複雑なエンタープライズワークフローのサポートを提供します。

## [OSGi のAEM Forms](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/deploying/introduction/technical-requirements)

OSGi 環境上のAEM Formsは、AEM Forms パッケージがデプロイされた標準のAEM オーサーまたはAEM Publishです。 OSGi 上のAEM Formsは、1 つのサーバー環境、ファーム設定、クラスター設定で実行できます。 クラスターを設定できるのは、AEM オーサーインスタンスの場合だけです。

## [AEM FormsのAdobe Sign](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms)

安全でシームレスなデジタル署名ワークフローを実現する RESTful サービス。 OAuth ベースの認証を使用してAEM Formsと統合され、自動署名コレクションとリアルタイムトラッキングが可能になります。

## [AEM Forms ドキュメントサービス 6.5](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services)

AEM Formsの web レイヤーで提供される、HTTP ベースのクライアント（フォームモバイル SDKなど）によるリモートでの利用向けの API です。AEM Forms内の各機能により、PDFドキュメントの作成、組み立て、配布、アーカイブ、デジタル署名の追加、Barcoded Formsのデコードを行うことができます。

| **サービス名** | **説明** | **ドキュメントリンク** |
|------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Forms サービス** | テンプレートおよび XML を使用してPDF formsをレンダリングし、インポート/エクスポート用にフォームデータを統合し、フラグメントベースのレンダリングをサポートします。 | [Forms サービスのドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Output サービス** | PDF、PCL、PostScriptなどの形式のテンプレートとデータを結合してドキュメントを生成します。 | [Output サービスのドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Assembler サービス** | PDFドキュメントと XDP ドキュメントの結合、並べ替え、検証および拡張を行います。 | [Assembler サービスのドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/use-document-services/assembler-service) |
| **ConvertPDF サービス** | PDFドキュメントをPostScriptまたは PNG、JPEG、TIFFなどの画像形式に変換します。 | [ConvertPDF サービスのドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/use-document-services/using-convertpdf-service) |
| **Barcoded Forms サービス** | TIFFファイルおよびPDFファイルのバーコードからデータを抽出し、データ取得プロセスを自動化します。 | [Barcoded Forms サービスのドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/use-document-services/using-barcoded-forms-service) |
| **DocAssurance サービス** | ドキュメント セキュリティ ポリシーの暗号化、復号化、デジタル署名、およびPDFへの適用を行います。 | [DocAssurance サービスのドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services#doc-assurance-service) |
| **PDF Generatorサービス** | ネイティブファイル形式（Microsoft Word、Excel など）をPDF文書に変換します。 | [PDF Generatorサービスドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/use-document-services/aem-document-services-programmatically#pdfgeneratorservice) |

## [Formsas a Cloud Service通信 API](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction)

AEM Formsas a Cloud Serviceは、フォームとコミュニケーションワークフローを管理するための高度なツールを提供し、シームレスなデジタルフォームの作成、データの取得、パーソナライズされたコミュニケーションをサポートします。 クラウド通信 API は、安全なオンデマンドおよびバッチでのドキュメント生成、操作、検証および HTTP を介した外部システムとの統合を提供し、効率的で安全な操作を確保します。

| **サービス名** | **説明** | **ドキュメントリンク** |
|-------------------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **ドキュメントの生成** | テンプレート（XFA またはPDF）と XML データを組み合わせて、PS、PCL、DPL、IPL、ZPL 形式などのPDF形式および印刷形式でドキュメントを生成します。 | [ ドキュメント生成ドキュメント ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=ja#document-generation) |
| **ドキュメントの操作** | PDF文書を結合、並べ替えます。 | [ ドキュメント操作ドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation) |
| **ドキュメントの変換** | PDFをPDF/A に変換し、PDF/A 準拠を確認します。 | [ ドキュメント変換ドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-conversion) |
| **ドキュメントAssurance** | 署名フィールドの追加または削除、署名、認証、暗号化、復号化、PDFドキュメントへの使用権限の適用を行います。 | [Document Assuranceのドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#doc-assurance) |
| **電子署名** | Adobe Signを統合して、フォームやドキュメントの安全な電子サインを行います。 | [ 電子署名のドキュメント ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=ja#digital-signatures) |


## [AEM Forms Workbench](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/install-workbench)

ワークフローの作成、編集、デプロイ、およびフォーム中心のビジネスプロセスの管理を行うためのデスクトップアプリケーションです。 バックエンドのサービスやシステムとの統合を実現します。

## [ アーキタイプ ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/developing/archetype/overview)

構造が事前に定義された新しいプロジェクトを生成するために使用されるAEMのテンプレートまたはパターンです。これにより、標準化、クイックセットアップ、AEM開発のベストプラクティスへの準拠が促進されます。

## [ オーサーインスタンス ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

コンテンツ作成者および管理者がコンテンツを公開する前に設計、作成および管理する環境。 バージョン管理、プレビュー、テストをサポートします。

## [ オーサリングのフロントエンド ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

AEM Forms内でフォームを作成および管理するためのユーザーインターフェイスです。

## [ アダプティブフォームブロック ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-references/form-components)

関連するコンポーネントとメタデータを論理的にグループ化し、動的なデータ処理と複数手順のフォームでの簡単なスケーラビリティを可能にするカプセル化ユニット。

## [コアコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/introduction)

フォームフィールド、レイアウトコンテナ、ボタン、その他のインタラクティブ要素など、すぐに使用できる再利用可能な構築ブロックで、フォームを作成します。

## [Correspondence Management](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/letters-correspondences/cm-overview)

企業が事前定義済みのテンプレート、ルール、データソースを使用して、パーソナライズされた通信を作成、管理および配信できるようにするモジュール。 レターテンプレート、カスタマーコミュニケーション、バッチ生成が含まれます。

## [CRX（Content repository extreme） ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/use-aem-forms-workspace/html-workspace-architecture)

AEMに組み込まれた JCR （Java Content Repository）は、構造化データと非構造化データを格納し、コンテンツ、テンプレート、設定の階層ストレージを可能にします。

## [ カスタムコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/customize-adaptive-forms-core-components)

Sling モデル、Sightly （HTL）および Java を使用して開発された、AEM Forms機能を拡張するカスタムコンポーネント。 通常、一意のビジネスロジックまたは高度なクライアントサイドのインタラクティビティに使用されます。

## [ カスタム XCI （XML 設定情報） ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/administrator-help/configure-forms/specifying-xci-configuration-options)

Adobe Experience Manager（AEM）Formsでは、カスタム XCI （XML Configuration Information）ファイルを使用することで、管理者はフォームおよびドキュメントに固有のレンダリングプロパティを定義できます。 管理コンソールで XCI 設定を指定すると、カスタムオプションでシステムのデフォルトを上書きし、カスタマイズされた処理やフォームの表示を行うことができます。

## [データ統合](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/form-data-model/data-integration)

データベース、web サービス、REST API などの外部データソースをフォームやワークフローにシームレスに統合して、動的でパーソナライズされたユーザーエクスペリエンスを実現します。

## [ データソース ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/form-data-model/configure-data-sources)

外部データをフォームに統合するためのインターフェイス（リレーショナルデータベース用の JDBC、web サービス用の REST エンドポイント、SAP システム用の OData など）。 AEM Forms Data Integration フレームワークを介して管理されます。

## [ ドキュメントフラグメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/letters-correspondences/lists)

ヘッダー、フッター、免責事項、条項など、ドキュメントの再利用可能なコンポーネント。フォームや通信に動的に含めて、一貫性を確保できます。

## [ レコードのドキュメント（DoR） ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms)

AEM Formsで、送信されたフォームの編集不可のアーカイブバージョン（通常はPDF形式）を生成する機能。トランザクションのレコードとして正確なコンテンツとレイアウトが保持されます。

## [Edge Delivery Services](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/overview)

AEM Forms用に最適化されたコンテンツ配信により、作成者がコンテンツをすばやく更新して公開できる、フォーム、テーマ、クライアントライブラリなどのアセットの待ち時間が短縮されます。

## [Formsの統合 ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/form-data-model/data-integration)

OSGi バンドルおよびコネクタを使用してAEM Formsをエンタープライズシステム（SAP、Salesforceなど）に接続し、双方向のデータフローとリアルタイムの更新をサポートする必要があります。

## [ フォームのレビュー ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms)

関係者が公開前にアダプティブフォームを確認、注釈を追加、変更を承認できる、ワークフロー駆動型の機能。 AEM インボックスとタスク管理を使用します。

## [フォームデータモデル（FDM）](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model)

アダプティブフォームをバックエンドデータソースに接続し、RESTful web サービス、SOAP サービスおよび OData との統合を可能にする表現レイヤー。 FDM を使用すると、フォーム作成者はフォームフィールドをバックエンドデータ構造に直接マッピングし、ユーザー入力を外部システムとシームレスに同期できます。

## [ フォームのローカリゼーション ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization)

アダプティブフォームのプロセスにより、複数の言語と地域の設定をサポートし、様々なオーディエンスからフォームにアクセスでき、使いやすいものになるようにします。

## [ フォームポータル ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/use-forms-portal/creating-form-portal-page)

Forms ポータルコンポーネントは、Adobe Experience Manager（AEM）を使用して作成された web サイトにForms ポータルを作成してカスタマイズするためのコンポーネントを web 開発者に提供します。 これにより、ユーザーは、web やモバイルのプラットフォームをまたいで、効率的にフォームを検出、アクセス、送信できます。

## [ フォームレンディションと送信フロントエンド ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Web ブラウザーを使用してフォームを表示および送信できる、AEM Formsのエンドユーザーインターフェイス。

## [ フォームセット ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/html5-forms/formset-in-aem-forms)

グループ化されて単一のエンティティとしてユーザーに表示される関連フォームのコレクションで、複雑なデータ収集プロセスを管理可能なセクションに分類できます。

## [Forms Designer](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/using-communications/installing-configuring-designer)

XDP フォームでフォームテンプレートをデザインし、AEM Formsでそれを使用してレコードのドキュメントを生成するために使用されるスタンドアロンアプリケーション。

## [Forms中心のワークフロー ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow)

ドキュメント承認、コンテンツ公開、ユーザー通知などのビジネスプロセスを管理する、AEM Formsの自動または手動の一連の手順です。

## [インタラクティブ通信](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/getting-started/interactive-communications-overview)

高度にパーソナライズされたマルチチャネル通信を管理するためのカスタム実装。 CRM や ERP システムなど、様々なソースのデータを組み合わせて、web、モバイル、メール、印刷など、様々な形式のコミュニケーションを提供します。

## [JCR （Java コンテンツリポジトリ） ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr)

コンテンツ、構成、メタデータをAEMに保存するための階層型の標準ベースのリポジトリであり、構造化されたデータ・ストレージと非構造化データ・ストレージをサポートします。

## [レター](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/letters-correspondences/create-letter#create-a-letter-template)

AEM Forms Document Services を活用してカスタマーコミュニケーションを生成する。 レターは、XDP テンプレート、データモデル、再利用可能なフラグメントを組み合わせて作成されるので、大量のシナリオでもスケーラビリティが確保されます。

## [AEM Formsのメタデータ ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/manage-administer-aem-forms/manage-form-metadata)

メタデータを使用すると、アセットの分類と取得を効率的に行えます。 AEM Formsには、各アセットタイプの定義済みメタデータが含まれており、カスタマイズできます。 また、メタデータをシームレスに作成、管理および交換するためのツールも提供します。

## [PDF Generator](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/forms/document-services/using-pdfg-in-aem-forms)

様々なファイル形式（Word、Excel、PowerPoint など）をPDF文書に変換し、暗号化、透かし、結合などの機能を提供する、AEM Formsのツール。

## [パブリッシュインスタンス](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

エンドユーザーにライブコンテンツを提供するAEM内の環境。 最適化されたパフォーマンスでフォーム、ページ、その他のデジタルエクスペリエンスを提供します。

## [ルールエディター](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components)

コーディングの専門知識を必要とせずに、表示、検証、データの事前入力など、フォームフィールドのカスタムルールとロジックを作成者が定義できる、アダプティブFormsのビジュアルツール。

## [ 手書き署名 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble)

マウスまたはタッチ操作対応デバイスを使用してフォームに直接署名することによって、フォームに電子サインを描画できるAEM Formsの機能。

## [AEM Formsでの送信アクション ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/configuring-submit-actions)

フォームの送信時に実行されるサーバーサイドまたはクライアントサイドのアクション。 例としては、REST API 呼び出し、ワークフローの呼び出し、JCR （Java コンテンツリポジトリ）へのデータの書き込みなどがあります。

## [ テーマ ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components)

プリプロセッサーに LESS/SASS を利用して、アダプティブフォームに適用される、CSS ベースのスタイルフレームワーク。 テーマを使用すると、ブランディングガイドラインやアクセシビリティ標準に準拠し、テーマをカスタマイズしたり、デザイン要素、レイアウト、カラー、タイポグラフィーや、場合によっては基になるコードを変更したりできます。

## [テンプレート](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components)

アダプティブフォームのブループリントは、構造要素（フィールド、レイアウト）と事前設定済みのスクリプトで構成され、新しいテンプレートを作成してカスタマイズしたり、既存の標準テンプレートを使用したりできます。

## [Web レイヤー ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

共通のサービスおよびフォームサービス上に構築された JSP またはサーブレットで構成され、フロントエンドのオーサリング、フォームレンディションと送信フロントエンド、REST API などの機能を提供します。

## [XDP （XML データパッケージ） ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/manage-administer-aem-forms/get-xdp-pdf-documents-aem)

AEM Formsで使用されるファイル形式で、フォームのデザインと構造化に使用され、動的コンテンツとインタラクティブ機能をサポートしながら、PDFやHTMLとしてレンダリングできます。

## [XFA （XML Forms アーキテクチャ） ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-an-xfa-form-template)

インタラクティブなアセットと動的なPDF formsを作成するための従来のテクノロジー。 XFA フォームを使用すると、動的なレイアウト調整、スクリプト作成、バックエンドシステムとのシームレスな統合など、高度な機能を利用できます。

## [XML または JSON スキーマ ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-xml-or-json-schema)

フォームおよびワークフローで XML または JSON データの形式および編成を定義するために使用される標準化された構造。 これらのスキーマは、一貫したデータ処理を保証し、外部システムとの相互運用性を可能にします。

<!--

## **Custom Properties**  

Developer-defined metadata attributes added to components or forms for advanced behaviors, accessed via Sling APIs or Groovy scripts for dynamic processing.

## **Embedding** 

Integrating adaptive forms into AEM Sites or external web pages using `<iframe>` or SPA (Single Page Application) models. Embedding supports seamless session handling and cross-origin resource sharing (CORS).

## **CDN (Content Delivery Network)**  

Distributed networks (e.g., Akamai) used for caching and delivering forms-related resources, ensuring high availability and faster load times for geographically distributed users.


## **Dispatcher**  

An AEM caching and load balancing tool configured to optimize delivery of adaptive forms. Its filter rules ensure secure access control while caching frequently accessed forms and assets.

## **Editors**  

Tools like the Adaptive Forms Editor, Theme Editor, and Rule Editor, enabling developers and content authors to customize forms and their behavior without extensive coding.

## **Responsive UI**  

An implementation of media queries and flexible grids, ensuring adaptive forms render seamlessly across various screen sizes and devices.

## **Custom Functions**  

JavaScript-based utilities or REST microservices that provide additional logic (e.g., complex field validation or data pre-population), extending the out-of-the-box capabilities of AEM Forms.

## **Package Manager**  

AEM's CRX Package Manager facilitates importing/exporting adaptive forms, data schemas, or configurations as .zip files, enabling modular deployment in distributed environments.

## **UE (User Experience)**  

Design principles and optimizations applied in AEM Forms to enhance usability, including accessibility features (ARIA roles, tab navigation) and intuitive layouts.

## **Forms Submission Services**

Back-end services for handling form submissions, integrating with the AEM Workflow engine, third-party APIs, or direct JCR persistence.


Foundation components
e-signing
adobe sign
letters
submit action
data sources
adaptive form block
edge delivery services
forms integration
custom component 
themes
template 
custom properties
embedding
CDN
Dispatcher
editors
responsive UI
custom functions
package manager
communication APIs
UE
Forms submission services
Form review
Forms Versioning
Adobe analytics forms integration specific

## **AEM Forms Foundation Components**  
Core reusable elements within AEM Forms, built on Granite UI, enabling developers to create complex forms. They provide robust features like data bindings, field validations, and support for multilingual content.


## **e-Signing**  
An implementation of digital signature standards (e.g., PKCS #7) within AEM Forms, integrated with Adobe Sign APIs to ensure secure and legally binding electronic signatures.

## Workspace

A browser-based interface for users to interact with AEM Forms workflows, tasks, and approvals.

## Sling

A REST-based web framework used in AEM to map request URLs to content resources, enabling efficient content rendering and delivery.

-->