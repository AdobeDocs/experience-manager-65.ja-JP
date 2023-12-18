---
title: Document Security の機能
description: AEM Document Security のさまざまなツールや機能について説明します。
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
source-git-commit: 65c5a4442f17e6bc52deaa1588f535a05698083f
workflow-type: ht
source-wordcount: '1216'
ht-degree: 100%

---

# Document Security の機能{#document-security-offerings}

Adobe Experience Manager Forms の Document Security を使用して、許可されたユーザーだけがドキュメントを使用するように指定できます。Document Security を使用すると、サポートされている形式で保存した情報を安全に配布できます。Adobe Portable Document Format（PDF）、Microsoft Word、Excel および PowerPoint を含むファイル形式に対応しています。

ドキュメントを保護するには、ポリシーを使用します。ポリシーを適用したドキュメントを受信者がどのように使用できるかは、ポリシーで指定した機密性設定によって決まります。例えば、テキストの印刷やコピー、テキストの編集、保護されたドキュメントへの署名やコメントの追加を受信者が実行できるかどうかを指定できます。

ポリシーは Document Security に保存されます。クライアントアプリケーションを使用してそのポリシーをドキュメントに適用します。ドキュメントにポリシーを適用すると、ポリシーで指定された機密性設定によって、ドキュメントに含まれる情報が保護されます。ポリシーで保護されたドキュメントを、ポリシーで許可されている受信者に配布できます。

次の図は、AEM Forms Document Security の一般的なアーキテクチャを示しています。

![Document Security - 推奨されるアーキテクチャ](do-not-localize/document_security_architecture.png)

## Document Security クライアント {#document-security-clients}

Document Security では、ドキュメントの保護や、保護されたドキュメントを表示および編集するための、さまざまなクライアントが提供されています。また、保護されたドキュメント上での全文検索を有効にするためのインデクサーも提供されています。ニーズに合ったクライアント、およびそのクライアントの機能を選ぶことができます。

Document Security サーバーは、ユーザー認証、ポリシーのリアルタイム管理、機密性の適用などのトランザクションをサーバーから実行する、中心となるコンポーネントです。サーバーは、ポリシー、監査記録およびその他の関連情報の中央リポジトリとしての役割も果たします。

Document Security サーバーでは、ポリシーの作成、ポリシーで保護されたドキュメントの管理、およびポリシーで保護されたドキュメントに関連するイベントの監視を行うための、web ベースのインターフェイス（web ページ）が提供されています。管理者は、ユーザー認証、監査、招待ユーザーへのメッセージなどのグローバルオプションを設定したり、招待ユーザーのアカウントを管理したりすることもできます。

このサーバーには、AEM Forms Document Security アドオンの機能が含まれています。Document Security アドオンのご購入については、AEM Forms の[セールスチーム](https://www.adobe.com/jp/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG)にお問い合わせください。

### ドキュメントを保護 {#protect-documents}

AEM Forms Document Security には、セキュリティポリシーに適用できる様々なツールが用意されています。ニーズや仕様に応じて、ツールを選ぶことができます。

![document-security-offerings](assets/document-security-offerings.png)

Document Security SDK、Adobe Acrobat、Document Security Extension for Microsoft® Office、またはポータブル保護ライブラリを使用して、セキュリティポリシーを適用、トラッキングすることができます。

* **Document Security SDK**：この SDK は、豊富な機能を持つクライアントです。ドキュメントセキュリティ SDK を使用して Document Server の機能にアクセスしたり、ポリシーで保護されたドキュメントを開いたり、カスタム拡張機能やプラグイン、またはアプリケーションを開発したりすることができます。例えば、カスタムのファイル形式を保護する拡張機能を開発したり、SDK とデータ損失防止（DLP）ソリューションを統合したりすることができます。Document Security SDK を使用して開発された拡張機能、アプリケーション、およびプラグインは、指定された AEM Forms サーバーにドキュメントを送信し、ポリシーはサーバー上で適用されます。AEM Forms Document Security クライアント SDK（CSDK）で、ポータブル保護ライブラリ（PPL）を使用して保護されているドキュメントの保護を解除することはできません（その逆の動作もできません）。

  Document Security SDK は Java と C++ の両方で利用することができます。Java™ SDK は、AEM Forms Document Security に付属しています。JEE 上に AEM Forms をデプロイする際に、Java SDK がインストールされます。C++ SDK を入手するには、[AEM カスタマーサポート](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja&amp;support-tab=home#support)にお問い合わせください。C++ SDK は、Microsoft® Visual Studio 2013 を使用してコンパイルすることができます。SDK の機能とその使用方法については、[Document Security API のドキュメント](https://help.adobe.com/ja_JP/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html)のサイトを参照してください。

* **Adobe Acrobat**：Adobe Acrobat を使用して、Microsoft® Office、web ブラウザー、またはその他の PDF 形式の印刷に対応しているアプリケーションなど、一般的なデスクトップアプリケーションで作成された PDF ドキュメントにセキュリティポリシーを適用できます。

  Adobe Acrobat は、[アドビの Web サイト](https://www.adobe.com/jp/acrobat/free-trial-download.html)で購入、ダウンロードできます。Adobe Acrobat の [PDF のセキュリティポリシーの設定](https://helpx.adobe.com/jp/acrobat/using/setting-security-policies-pdfs.html)の記事には、Adobe Acrobat を使用したポリシーの作成や適用についての詳細が掲載されています。

* **Document Security Extension for Microsoft® Office**：Document Security Extension for Microsoft® Office を使用して、Microsoft® Office プログラム内から、事前に定義されたポリシーを Microsoft® Office ファイルに適用できます。この拡張機能を使用することで、許可されたユーザーだけがポリシーで保護された Microsoft® Word、Excel、PowerPoint ファイルを使用できるようになります。このプラグインをインストールした、権限を持つユーザーのみが、ポリシーで保護されたファイルを使用できます。

  この Document Security の拡張機能は Microsoft® Office プラグインとして使用できます。C++ SDK を入手する場合は、[AEM カスタマーサポート](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html)にお問い合わせください。その後、[Document Security Extension for Microsoft® Office](https://experienceleague.adobe.com/docs/experience-manager-document-security/using/download-installer.html?lang=ja)のヘルプを参照することで、インストール方法、設定方法、拡張機能の使用方法を確認できます。

* **ポータブル保護ライブラリ（PPL）：** PPL は、ドキュメントを AEM Forms サーバーに送ることなく、ローカルにドキュメントを保護します。ネットワークに送信されるのは、セキュリティの証明書とポリシーの詳細のみです。PPL を使用して、ログインしているユーザーに対してのみ、ポリシーへのアクセスとポリシーの取得を許可することができます。AEM にログインしているユーザーについて、ポリシーを取得することができます。

  上記に加えて、PPL には Document Security SDK のすべての機能が搭載されています。ドキュメントセキュリティ SDK を使用して Document Server の機能にアクセスしたり、ポリシーで保護されたドキュメントを開いたり、カスタム拡張機能やプラグイン、またはアプリケーションを開発したりすることができます。PPL で、AEM Forms Document Security クライアント SDK（CSDK）を使用して保護されたドキュメントの保護を解除することはできません（その逆の動作もできません）。

  PPL は、32 ビットおよび 64 ビットバージョンの Java、または C++ 言語で使用できます。また、OSGi 上の AEM Forms に対する OSGi バンドルとして使用することもできます。C++ PPL は、Microsoft® Visual Studio 2013 を使用してコンパイルすることができます。AEM Forms Document Security アドオンのライセンスを持っている場合は、[AEM Forms Document Security](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja&amp;support-tab=home#support) サポートチームに問い合わせて、PPL を入手することができます。後から、PPL ヘルプ（ライブラリに付属）を参照することで、PPL のセットアップ方法および使用方法を確認できます。

### 保護されたドキュメントの表示または編集 {#view-or-edit-protected-documents}

* **PDF ドキュメント**&#x200B;の場合、Adobe Acrobat DC、Acrobat Reader、およびモバイル版 Acrobat Reader を使用して、保護された PDF ドキュメントを表示できます。ほとんどのユーザーはすでにデバイスに Acrobat Reader がインストールされているため、保護されたドキュメントを表示するために追加のソフトウェアを入手もしくは使用方法を学習する必要はありません。Acrobat Reader は、[Acrobat Reader ダウンロード Web サイト](https://get.adobe.com/jp/reader/)からダウンロードすることもできます。

* **Microsoft® Office ドキュメント**&#x200B;の場合、Microsoft® Office と AEM Forms Document Security extension for Microsoft® Office が必要となります。この Document Security の拡張機能は Microsoft® Office プラグインとして使用できます。この拡張機能は、アドビの Web サイトからダウンロードすることができます。

### 保護済みドキュメントのインデックス作成 {#index-protected-documents}

Microsoft® Windows の全文検索エンジン（SharePoint インデックスサーバー）や Adobe Experience Manager（AEM）は、プレーンテキストファイル、Microsoft® Office ドキュメント、PDF ドキュメントなど、広く使用されている様々なドキュメント形式において、全文検索を実行できます。ドキュメントセキュリティインデクサーを使用して全文検索エンジンを有効にし、保護された PDF ドキュメントを検索できます。

* **iFilter インデクサー：** Filter インデクサーを使用することで、保護された PDF ドキュメントのインデックスを作成し、Microsoft® Windows の全文検索エンジン（デスクトップインデックスサービスと SharePoint インデックスサーバー）を有効にします。これにより、保護された PDF ドキュメントを検索することができます。詳しくは、[保護済みドキュメントに対する AEM SharePoint IFilter の使用](assets/sharepoint-ifilter-doc-security.pdf)を参照してください。

* **AEM Forms ドキュメントセキュリティインデクサー：** AEM Forms ドキュメントセキュリティインデクサーを使用することで、保護された PDF ドキュメントのインデックスを作成し、Adobe Experience Manager での保護された PDF ドキュメントの検索を有効にします。このインデクサーは、AEM Forms ドキュメントセキュリティのサービスの一部です。これらは、JEE 上の AEM Forms インストーラーに含まれています。
