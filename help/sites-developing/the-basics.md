---
title: AEM の中心概念
seo-title: The Basics
description: AEM の構造に関する中心概念と、それを基にした開発方法（JCR、Sling、OSGi、Dispatcher、ワークフロー、MSM の解説を含む）の概要
seo-description: An overview of the core concepts of how AEM is structured and how to develop on top of it including understanding the JCR, Sling, OSGi, the dispatcher, workflows, and MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: ht
source-wordcount: '3324'
ht-degree: 100%

---

# AEM の中心概念 {#aem-core-concepts}

>[!NOTE]
>
>AEM の中心概念の詳細に入る前に、[AEM Sites の開発の手引き](/help/sites-developing/getting-started.md) のドキュメントで WKND チュートリアルを済ませ、AEM の開発プロセスと中心概念の概要を確認しておくことをお勧めします。

## AEM での開発の必要条件 {#prerequisites-for-developing-on-aem}

AEM での開発には、以下のスキルが必要です。

* 以下を含む web アプリケーション技術の基本知識

   * リクエスト - 応答（XMLHttpRequest／XMLHttpResponse）のサイクル
   * HTML
   * CSS
   * JavaScript

* Content Explorer を含む Experience Server（CRX）の実務知識
* クラシック UI で開発する場合は、JSP の簡単な例を理解および変更できる能力を含む、JSP（JavaServer Pages）の基本知識も必要です。

[ガイドラインおよびベストプラクティス](/help/sites-developing/dev-guidelines-bestpractices.md) を読み、手順に従うこともお勧めします。

## Java™ コンテンツリポジトリ {#java-content-repository}

Java™ コンテンツリポジトリ（JCR）の規格である [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html) では、コンテンツリポジトリ内で、任意の精度レベルでコンテンツに双方向アクセスするための、ベンダーにも実装にも依存しない方法が指定されています。

仕様を主導しているのは、Adobe Research（スイス）AG です。

[JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) パッケージ、javax.jcr。「&amp;ast;」は、リポジトリコンテンツの直接アクセスと操作に使用されます。

## Experience Server（CRX）と Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server は、AEM の基でありカスタムアプリケーションの構築に使用できる Experience Services を備えており、Jackrabbit に基づいてコンテンツリポジトリを埋め込みます。

[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) は、オープンソースの、JCR API 2.0 に完全準拠した実装です。

## Sling のリクエスト処理 {#sling-request-processing}

### Sling の概要 {#introduction-to-sling}

AEM の構築には [Sling](https://sling.apache.org/index.html) が使用されています。これは、REST の原則に基づき、コンテンツ指向のアプリケーションを簡単に開発できる、web アプリケーションのフレームワークです。Sling はデータストアとして、Apache Jackrabbit のような JCR リポジトリ、または、AEM の場合は CRX コンテンツリポジトリを使用します。Sling は Apache Software Foundation に寄贈されました。詳しくは、Apache でご確認ください。

Sling を使用する場合、レンダリングされるコンテンツのタイプは、処理に関する第一の考慮事項ではありません。主な考慮事項は、URL を解決して得られるコンテンツオブジェクト用に、レンダリングを実行するためのスクリプトが見つかるかどうかです。このことは、要件に合わせて簡単にカスタマイズ可能なページを Web コンテンツ作成者が構築する際に非常に役立ちます。

この柔軟性の利点は、様々なコンテンツ要素を持つアプリ、または容易にカスタマイズできるページが必要な場合に明らかです。特に、WCM のような web コンテンツ管理システムを AEM ソリューションに実装する場合です。

Sling を使用した開発の概要について詳しくは、『[15 分間でわかる Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html)』を参照してください。

次の図は、Sling のスクリプト解決の説明です。HTTP リクエストからコンテンツノード、コンテンツノードからリソースタイプ、リソースタイプからスクリプトを得る方法と、使用可能なスクリプト変数を示しています。

![Apache Sling スクリプトの解決について](assets/sling-cheatsheet-01.png)

次の図は、SlingPostServlet を扱う際に使用できる、非表示ながらも強力なリクエストパラメータをすべて説明しています。これは、すべての POST リクエストのデフォルトハンドラで、リポジトリー内のノードの作成、変更、削除、コピー、移動に無限のオプションを提供します。

![SlingPostServlet の使用](assets/sling-cheatsheet-02.png)

### Sling はコンテンツ中心型 {#sling-is-content-centric}

Sling は *コンテンツ中心型* です。これは、各（HTTP）リクエストが JCR リソース（リポジトリーノード）の形でコンテンツにマッピングされるため、コンテンツに焦点を当てた処理が行われることを意味します。

* 最初のターゲットは、コンテンツを保持しているリソース（JCR ノード）です。
* 次に、表示域またはスクリプトが、リソースプロパティから、リクエストの特定の部分（セレクターや拡張子など）と組み合わせて配置されます。

### RESTful Sling {#restful-sling}

コンテンツ中心型の原理により、Sling は REST 指向のサーバーを実装するので、web アプリケーションフレームワークの新しい概念を特徴としています。メリットは次のとおりです。

* 表面上だけでなく、非常に RESTful であり、リソースや表示域をサーバー内で正しくモデリング
* 1 つ以上のデータモデルを削除

   * 以前に必要だったもの：URL 構造、ビジネスオブジェクト、DB スキーマ
   * これは現在、次のように短縮されています：URL = リソース = JCR 構造

### URL の分解 {#url-decomposition}

Sling では、処理はユーザーリクエストの URL によって駆動されます。これにより、適切なスクリプトによって表示されるコンテンツが定義されます。これを行うために、URL から情報が抽出されます。

次の URL を分析する場合：

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

次のような複合部品に分割できます。

| プロトコル | ホスト | コンテンツのパス | セレクター | 拡張子 |  | 接尾辞 |  | パラメーター |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | tools/spy | .printable.a4. | html | / | a/b | ? | x=12 |

**プロトコル** - HTTP

**ホスト** - web サイトの名前。

**コンテンツのパス** - レンダリングされるコンテンツを指定するパス。拡張機能と組み合わせて使用します。この例では、tools/spy.html に変換します。

**セレクター** - コンテンツをレンダリングする方法を選ぶために使用します。この例では、A4 形式のプリンターに対応したバージョンを選択しています。

**拡張子** - コンテンツの形式。これも、レンダリングに使用するスクリプトを指定します。

**サフィックス** - 追加情報を指定するために使用できます。

**パラメーター** - 動的コンテンツで必要なパラメーターです。

#### URL からコンテンツおよびスクリプトへ {#from-url-to-content-and-scripts}

これらの原則を使用すると、次のようになります。

* マッピングでは、リクエストから抽出されたコンテンツパスを使用してリソースを見つけます。
* 適切なリソースが見つかると、Sling リソースタイプが抽出され、コンテンツのレンダリング用のスクリプトを見つけるために使用されます。

次の図は、使用されるメカニズムを示しています。これについては、次の各セクションで詳しく説明します。

![chlimage_1-86](assets/chlimage_1-86a.png)

Sling を使用して、特定のエンティティをレンダリングするスクリプトを指定します（JCR ノードで `sling:resourceType` プロパティを設定します）。このメカニズムは、リソースが複数のレンディションを持つことができるため、スクリプトがデータエンティティにアクセスするメカニズム（PHP スクリプトの SQL 文のように）よりも自由度が高くなります。

#### リソースへのリクエストのマッピング {#mapping-requests-to-resources}

リクエストを分解し、必要な情報を抽出します。リポジトリーで、リクエストされたリソース（コンテンツノード）を検索します。

* 最初の Sling では、リクエストで指定された場所（例：`../content/corporate/jobs/developer.html`）にノードが存在するかどうかを確認します。
* ノードが見つからない場合、拡張子なしで検索を繰り返します（例：`../content/corporate/jobs/developer`）。
* それでもノードが見つからない場合、Sling は HTTP コード 404（Not Found）を返します。

Sling では JCR 以外のノードもリソースとして扱えますが、これは詳細な機能です。

### スクリプトの検索 {#locating-the-script}

適切なリソース（コンテンツノード）が見つかると、**sling リソースタイプ**&#x200B;が抽出されます。これは、コンテンツのレンダリングに使用するスクリプトを見つけるパスです。

`sling:resourceType` によって指定されるパスは、次のいずれかです。

* 絶対パス
* 設定パラメーターに対する相対パス

   移植性を高めるため、アドビでは相対パスを推奨しています。

Sling のスクリプトはすべて、`/apps` または `/libs` のサブフォルダーに格納され、この順序で検索されます（[コンポーネントおよびその他の要素のカスタマイズ](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)を参照）。

その他の注意点は次のとおりです。

* メソッド（GET、POST）が必要な場合は、HTTP の仕様に従って、jobs.POST.esp のように大文字で指定します（以下を参照）。
* 次のような様々なスクリプトエンジンがサポートされています。

   * HTL（HTML テンプレート言語 - Adobe Experience Manager で優先および推奨される HTML 用のサーバーサイドのテンプレートシステム）：`.html`
   * ECMAScript（JavaScript）ページ（サーバーサイド実行）：`.esp, .ecma`
   * Java™ サーバーページ（サーバーサイド実行）：`.jsp`
   * Java™ サーブレットコンパイラー（サーバーサイド実行）：`.java`
   * JavaScript テンプレート（クライアント側実行）：`.jst`

AEM の特定のインスタンスでサポートされているスクリプトエンジンのリストは、Felix Management Console（`http://<host>:<port>/system/console/slingscripting`）にあります。

また、Apache Sling では、他の一般的なスクリプトエンジン（Groovy、JRuby、Freemarker など）との統合がサポートされており、新しいスクリプトエンジンと統合する方法も提供されています。

前述の例を使用すると、`sling:resourceType` が `hr/jobs` の場合は、次のようになります。

* GET/HEAD リクエストおよび .html で終わる URL（デフォルトのリクエストタイプ、デフォルトの形式）

   スクリプトは /apps/hr/jobs/jobs.esp です。sling:resourceType の最後のセクションがファイル名となります。

* POST リクエスト（GET／HEAD を除くすべてのリクエストタイプ。メソッド名は大文字にする必要があります）

   スクリプト名には POST が使用されます。

   スクリプトは `/apps/hr/jobs/jobs.POST.esp` です。

* .html で終わらない、他の形式の URL です。

   例：`../content/corporate/jobs/developer.pdf`

   スクリプトは `/apps/hr/jobs/jobs.pdf.esp` です。スクリプト名にサフィックスが追加されます。

* セレクターを含む URL

   セレクターを使用して、同じコンテンツを別の形式で表示できます。例：プリンターに適したバージョン、rss フィード、概要など。

   プリンターに適したバージョンでは、セレクターが *print* である可能性がります。例：`../content/corporate/jobs/developer.print.html`

   スクリプトは `/apps/hr/jobs/jobs.print.esp` です。セレクターがスクリプト名に追加されます。

* sling:resourceType が定義されていない場合は、次のようになります。

   * コンテンツパスは、適切なスクリプトを検索するために使用されます（パスに基づいた ResourceTypeProvider がアクティブな場合）。

      例えば、`../content/corporate/jobs/developer.html` のスクリプトは、`/apps/content/corporate/jobs/` で検索を生成します。

   * プライマリノードタイプが使用されます。

* スクリプトがまったく見つからない場合は、デフォルトのスクリプトが使用されます。

   デフォルトのレンディションは現在、プレーンテキスト（.txt）、HTML（.html）、JSON（.json）としてサポートされています。これらのレンディションでは、ノードのプロパティが（適切にフォーマットされて）リストされます。拡張子 .res のデフォルトのレンディション、またはリクエスト拡張子のない要求は、（可能な場合は）リソースをスプールします。
* HTTP エラー処理（コード 403 または 404）の場合、Sling は以下のいずれかの場所でスクリプトを検索します。

   * それぞれ、[カスタマイズされたスクリプト](/help/sites-developing/customizing-errorhandler-pages.md)の場所 /apps/sling/servlet/errorhandler 
   * または標準スクリプト /libs/sling/servlet/errorhandler/403.esp または 404.esp の場所です。

特定のリクエストに複数のスクリプトが該当する場合は、一致率が最も高いスクリプトが選択されます。一致は具体的であるほど良くなります。つまり、リクエスト拡張子であれ、メソッド名の一致であれ、セレクターの一致が多いほど良くなります。

例えば、次のリソースにアクセスするためのリクエストについて考えます。
`/content/corporate/jobs/developer.print.a4.html`リソースのタイプは次のとおりとします。`sling:resourceType="hr/jobs"`

また、次のリストのスクリプトが正しい場所にあると仮定します。

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

この場合、優先順位は (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1) となります。

リソースタイプ（主に `sling:resourceType` プロパティで定義）に加えて、リソーススーパータイプもあります。これは通常、`sling:resourceSuperType` プロパティで示されます。これらのスーパータイプは、スクリプトを検索する際にも検討されます。リソーススーパータイプの利点は、（デフォルトのサーブレットで使用される）デフォルトのリソースタイプ `sling/servlet/default` が事実上のルートになるリソースの階層を形成できる点です。

リソースのリソーススーパータイプは次の 2 つの方法で定義できます。

* リソースの `sling:resourceSuperType` プロパティを使用。
* `sling:resourceSuperType` が示すノードの `sling:resourceType` プロパティを使用。

次に例を示します。

* ／

   * a
   * b

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




タイプの階層は

* `/x`
   * `[ c, b, a, <default>]` です
* 一方、`/y` では
   * 階層は `[ c, a, <default>]` です

これは、`/y` には `sling:resourceSuperType` プロパティがあるのに対して、`/x` にはなく、スーパータイプがリソースタイプから継承されているからです。

#### Sling スクリプトを直接呼び出しできない {#sling-scripts-cannot-be-called-directly}

Sling 内では、スクリプトを直接呼び出しできません。REST サーバーの厳格な概念に違反して、リソースと表現を混在させることになるからです。

表現（スクリプト）を直接呼び出す場合、リソースがスクリプト内に隠蔽されるので、フレームワーク（Sling）では認識できなくなります。これにより、次のような機能が失われます。

* GET 以外の HTTP メソッドの自動処理。これには以下が含まれます。

   * Sling のデフォルトの実装で扱う POST、PUT、DELETE
   * sling:resourceType の場所にある `POST.jsp` スクリプト

* コードアーキテクチャに必要なクリーン性や明確な構造が失われます。これは大規模な開発では最も重要です。

### Sling API {#sling-api}

これは、Sling API パッケージ、org.apache.sling.&amp;ast;、およびタグライブラリを使用します。

### sling:include を使用した既存の要素の参照 {#referencing-existing-elements-using-sling-include}

最後の考慮事項は、スクリプト内にある既存の要素の参照の必要性です。

より複雑なスクリプト（集計スクリプト）は、複数のリソース（ナビゲーション、サイドバー、フッター、リストの要素など）へのアクセスが必要になる場合があり、そのために&#x200B;*リソース*&#x200B;を含めます。

これは、sling:include(&quot;/&lt;path>/&lt;resource>&quot;) コマンドを使用して行えます。これにより、参照されるリソースの定義を効率的に含めることができます。例えば、次のステートメントでは、画像をレンダリングするために既存の定義を参照しています。

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGi {#osgi}

OSGi は、モジュール式アプリケーションおよびライブラリを開発およびデプロイするためのアーキテクチャを定義します（Dynamic Module System for Java とも呼ばれる）。OSGi コンテナを使用すると、アプリケーションを個々のモジュール（追加のメタ情報を含む jar ファイルで、OSGi 用語でバンドルと呼ばれます）に分割し、それらの間の相互依存関係を次の機能で管理できます。

* コンテナ内に実装されているサービス
* コンテナとアプリケーションの間の契約

これらのサービスおよび契約によって提供されるアーキテクチャでは、コラボレーションのために個々の要素が相互に動的に検出し合うことができます。

その後、OSGi フレームワークによって、これらのバンドルの動的読み込み／読み込み解除、設定および制御が可能になります。再起動は不要です。

>[!NOTE]
>
>OSGi テクノロジーについて詳しくは、[OSGi Web サイト](https://www.osgi.org)を参照してください。
>
>特に、基礎教育に関するページには、プレゼンテーションやチュートリアルのコレクションが収められています。

このアーキテクチャにより、Sling をアプリケーション固有のモジュールで拡張できます。Sling、したがって CQ5 は、OSGI（Open Services Gateway initiative）の [Apache Felix](https://felix.apache.org/documentation/index.html) 実装を使用しており、OSGi Service Platform Release 4 バージョン 4.2 の仕様に基づいています。どちらも、OSGi フレームワーク内で実行される OSGi バンドルの集まりです。

これにより、インストール内のどのパッケージでも、以下のアクションを実行できます。

* インストール
* 開始
* 停止
* 更新
* アンインストール
* 現在のステータスの確認
* 特定のバンドルに関する詳細情報（記号名、バージョン、場所など）へのアクセス

詳しくは、[Web コンソール](/help/sites-deploying/web-console.md)、[OSGI 設定](/help/sites-deploying/configuring-osgi.md)、および [OSGi 設定の指定](/help/sites-deploying/osgi-configuration-settings.md)を参照してください。

## AEM 環境の開発オブジェクト {#development-objects-in-the-aem-environment}

開発の際に関心事となるものを以下に示します。

**項目** - ノードまたはプロパティのアイテム。

項目オブジェクトの操作方法について詳しくは、Interface javax.jcr Item の [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) を参照してください。

**ノード（およびそのプロパティ）** - ノードとそのプロパティは、JCR API 2.0 仕様（JSR 283）で定義されています。コンテンツ、オブジェクト定義、レンダリングスクリプトおよびその他のデータを格納します。

ノードがコンテンツ構造を定義し、ノードのプロパティに実際のコンテンツおよびメタデータが格納されます。

コンテンツノードがレンダリングを制御します。Sling は、受信リクエストからコンテンツノードを取得します。このノードの sling:resourceType プロパティは、使用する Sling レンダリングコンポーネントを指しています。

ノードは JCR 名であり、Sling 環境ではリソースとも呼ばれます。

例えば、現在のノードのプロパティを取得するには、スクリプトで次のコードを使用できます。

`PropertyIterator properties = currentNode.getProperties();`

currentNode は現在のノードオブジェクトです。

ノードオブジェクトの操作方法について詳しくは、[Javadocs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) を参照してください。

**Widget** - AEMでは、すべてのユーザー入力はウィジェットで管理されます。多くの場合、コンテンツの一部の編集を制御するために使用されます。

ダイアログは、ウィジェットを組み合わせて作成されます。

AEM は、ExtJS ウィジェットライブラリを使用して開発されました。

**ダイアログ** - ダイアログは特殊なタイプのウィジェットです。

AEM では、コンテンツを編集するには、アプリケーション開発者が定義したダイアログを使用します。ダイアログでは一連のウィジェットを組み合わせて、関連するコンテンツの編集に必要なフィールドとアクションをすべてユーザーに提供します。

ダイアログは、メタデータの編集や、様々な管理ツールでも使用されます。

**コンポーネント** - ソフトウェアコンポーネントは、事前に定義されたサービスやイベントを提供するシステム要素であり、他のコンポーネントと通信できます。

AEM 内では、多くの場合、コンポーネントを使用してリソースのコンテンツをレンダリングします。リソースがページである場合、それをレンダリングするコンポーネントは、トップレベルコンポーネントまたはページコンポーネントと呼ばれます。ただし、コンポーネントは必ずしもコンテンツのレンダリングや特定のリソースへのリンクに使用されるわけではありません。例えば、ナビゲーションコンポーネントを使用すると、複数のリソースに関する情報を表示できます。

コンポーネントの定義には以下が含まれます。

* コンテンツのレンダリングに使用するコード
* ユーザー入力および結果コンテンツの設定のためのダイアログ

**テンプレート** - テンプレートは特定のタイプのページのベースとなります。「Web サイト」タブでページを作成する際は、ユーザーはテンプレートを選択する必要があります。このテンプレートをコピーして新しいページが作成されます。

テンプレートは、そこから作成されるページと同じ構造を持つノードの階層ですが、実際のコンテンツは含みません。

ページのレンダリングに使用するページコンポーネントと、デフォルトのコンテンツ（プライマリトップレベルコンテンツ）を定義します。AEM はコンテンツ中心型なので、コンテンツによってレンダリング方法が定義されます。

**ページコンポーネント（トップレベルコンポーネント）** - ページのレンダリングに使用するコンポーネント。

**ページ** - ページはテンプレートの「インスタンス」です。

ページには、cq:Page タイプの階層ノードと cq:PageContent タイプのコンテンツノードが含まれています。コンテンツノードの sling:resourceType プロパティは、ページのレンダリングに使用されるページコンポーネントを指しています。

例えば、現在のページの名前を取得するには、スクリプトで次のコードを使用します。

S`tring pageName = currentPage.getName();`

currentPage は現在のページオブジェクトです。ページオブジェクトの操作方法について詳しくは、[Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html) を参照してください。

**ページマネージャー** - ページマネージャーは、ページレベルの操作方法を提供するインターフェイスです。

例えば、リソースを含んだページを取得するには、スクリプトで次のコードを使用します。

Page myPage = pageManager.getContainingPage(myResource);

pageManager はページマネージャーオブジェクト、myResource はリソースオブジェクトです。ページマネージャーで提供される方法について詳しくは、[Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html) を参照してください。

## リポジトリ内の構造 {#structure-within-the-repository}

以下のリストは、リポジトリ内で見られる構造の概要を示しています。

>[!CAUTION]
>
>この構造、またはその中のファイルの変更は、注意して行う必要があります。
>
>開発時には変更が必要ですが、その変更が及ぼす影響を十分に理解しておく必要があります。

>[!CAUTION]
>
>`/libs` パス内は一切変更しないでください。設定やその他の変更の場合は、項目を `/libs` から `/apps` にコピーし、`/apps` 内で変更を行います。

* `/apps`

   関連するアプリケーション。Web サイトに固有のコンポーネント定義を含めます。コンポーネントは、`/libs/foundation/components` で利用可能な標準搭載のコンポーネントに基づいて開発することができます。

* `/content`

   Web サイト用に作成したコンテンツ。

* `/etc`

* `/home`

   ユーザーおよびグループの情報。

* `/libs`

   AEM のコアに属するライブラリと定義。`/libs` のサブフォルダーは、検索やレプリケーションなどの標準搭載の AEM 機能を表します。AEM の動作に影響するため、`/libs` のコンテンツは変更しないでください。Web サイトに固有の機能は `/apps` の下で開発する必要があります（[コンポーネントおよびその他の要素のカスタマイズ](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)を参照）。

* `/tmp`

   一時作業領域。

* `/var`

   監査ログ、統計、イベント処理など、変化し、システムによって更新されるファイル。

## 環境 {#environments}

AEM では、実稼働環境は多くの場合、[オーサーインスタンスとパブリッシュインスタンス](/help/sites-deploying/deploy.md#author-and-publish-installs)という 2 種類のインスタンスで構成されます。

## Dispatcher {#the-dispatcher}

Dispatcher は、キャッシュとロードバランシングの両方を管理するアドビのツールです。詳しくは、[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) を参照してください。

## FileVault（ソースリビジョンシステム） {#filevault-source-revision-system}

FileVault は、JCR リポジトリにファイルシステムマッピングとバージョン管理の機能を提供します。FileVault を使用すると、標準のバージョン管理システム（Subversion など）で、プロジェクトコード、コンテンツ、設定などの格納やバージョン管理を完全にサポートして、AEM 開発プロジェクトを管理できます。

詳しくは、[FileVault ツール](/help/sites-developing/ht-vlttool.md)のドキュメントを参照してください。

## ワークフロー {#workflows}

コンテンツは、多くの場合、様々な参加者による承認やサインオフなどの組織的なプロセスの対象となります。これらのプロセスはワークフローとして表現し、[AEM 内で定義および開発](/help/sites-developing/workflows-models.md)したあと、必要に応じて[適切なコンテンツページ](/help/sites-administering/workflows.md)や[デジタルアセット](/help/assets/assets-workflow.md)に適用することができます。

ワークフローエンジンを使用して、ワークフローの実装と、その後のコンテンツへの適用を管理します。

## マルチサイト管理 {#multi-site-management}

マルチサイトマネージャー（MSM）を使用すると、同じコンテンツを共有する複数の web サイトを簡単に管理できます。MSM を使用すると、あるサイトでのコンテンツの変更が他のサイトに自動的にレプリケートされるように、サイト間の関係を定義できます。

例えば、web サイトは多くの場合、世界中のオーディエンスに向けて複数の言語で提供されています。同じ言語のサイト数が少ない場合（3～5 個）は、手動プロセスによってサイト間でコンテンツを同期することも可能です。しかし、サイト数が増えた場合や、複数の言語が関係する場合は、プロセスを自動化する方が効率的です。

* Web サイトの様々な言語バージョンを効率的に管理します。
* ソースサイトに基づいて 1 つ以上のサイトを自動的に更新します。

   * 基本構造を共通化し、複数のサイトで共通のコンテンツを使用します。
   * 利用可能なリソースを最大限に活用します。
   * 共通のルックアンドフィールを維持します。
   * サイト間で異なるコンテンツの管理に労力を集中させます。

詳しくは、[マルチサイトマネージャー](/help/sites-administering/msm.md)を参照してください。
