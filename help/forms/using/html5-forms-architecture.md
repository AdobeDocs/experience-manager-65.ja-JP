---
title: HTML5 フォームのアーキテクチャ
seo-title: Architecture of HTML5 forms
description: HTML5 フォームは、埋め込みAEMインスタンス内のパッケージとしてデプロイされ、RESTful Apache Sling アーキテクチャを使用して、HTTP/S 上での REST エンドポイントとして機能を公開します。
seo-description: HTML5 forms is deployed as a package within the embedded AEM instance and exposes the functionality as REST end point over HTTP/S using RESTful Apache Sling architecture.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
feature: Mobile Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 32%

---

# HTML5 フォームのアーキテクチャ{#architecture-of-html-forms}

## アーキテクチャ {#architecture}

HTML5 フォーム機能は埋め込み AEM インスタンス内のパッケージとしてデプロイされ、RESTful [Apache Sling アーキテクチャ](https://sling.apache.org/)を使用して、HTTP/S 上の REST エンドポイントとして公開されます。

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Sling フレームワークの使用 {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) はリソース中心です。 リクエスト URL を使用して、最初にリソースを解決します。 各リソースには **sling:resourceType** ( または **sling:resourceSuperType**) プロパティを使用します。 このプロパティ、要求メソッドおよび要求 URL のプロパティに基づいて、要求を処理する Sling スクリプトが選択されます。 この Sling スクリプトは、JSP またはサーブレットにすることができます。 HTML5 フォームの場合、**Profile** ノードは Sling リソースとして機能し、**プロファイルレンダラー**&#x200B;はモバイルフォームをレンダリングするために特定のプロファイルで要求を処理する Sling スクリプトとして機能します。**プロファイルレンダラー**&#x200B;は要求からパラメーターを読み取り、Forms OSGi サービスを呼び出す JSP です。

REST エンドポイントとサポートされているリクエストパラメーターについて詳しくは、[フォームテンプレートのレンダリング](/help/forms/using/rendering-form-template.md)を参照してください。

ユーザーがiOSや Android™ブラウザーなどのクライアントデバイスから要求を行うと、Sling はまず要求 URL に基づいてプロファイルノードを解決します。 このプロファイルノードから、 **sling:resourceSuperType** および **sling:resourceType** ：このフォームレンダリング要求を処理できる使用可能なすべてのスクリプトを決定します。 次に、Sling 要求セレクターと要求メソッドを使用して、この要求の処理に最適なスクリプトを識別します。 要求がプロファイルレンダラー JSP に到達すると、JSP はForms OSGi サービスを呼び出します。

Sling スクリプトの解決について詳しくは、 [AEM Sling Cheat Sheet](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja) または [Apache Sling Url の分解](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html).

#### 一般的なフォーム処理呼び出しフロー {#typical-form-processing-call-flow}

HTML5 forms は、最初のリクエスト時にフォームの処理（レンディションまたは送信）に必要なすべての中間オブジェクトをキャッシュします。 データに依存するオブジェクトはキャッシュされません。このようなオブジェクトは変更される可能性が高いからです。

Mobile Forms は、PreRender キャッシュと Render キャッシュの 2 つの異なるレベルのキャッシュを維持します。 preRender キャッシュには、解決されたテンプレートのすべてのフラグメントと画像が含まれ、レンダリングキャッシュには、HTMLなどのレンダリングされたコンテンツが含まれます。

![HTML5 フォームのワークフロー](assets/cacheworkflow.png)

HTML5 フォームのワークフロー

HTML5 フォームは、フラグメントと画像の参照が欠落しているテンプレートをキャッシュしません。 HTML5 フォームの処理に通常より多くの時間がかかる場合は、サーバーログで参照や警告が見つからないかを確認します。 また、オブジェクトの最大サイズに達していないことも確認してください。

Forms OSGi サービスは次の 2 つの手順でリクエストを処理します。

* **レイアウトと初期フォーム状態の生成**：Forms OSGi レンダリングサービスは、フォームキャッシュコンポーネントを呼び出して、このフォームがすでにキャッシュされていて無効化されていないかを調べます。フォームがキャッシュされ、有効な場合は、キャッシュから生成されたHTMLを提供します。 フォームが無効になっている場合、Forms OSGi レンダリングサービスは初期フォームレイアウトとフォーム状態を XML 形式で生成します。 この XML は、Forms OSGi サービスによってHTMLレイアウトと初期 JSON フォーム状態に変換され、以降の要求に対してキャッシュされます。
* **事前入力されたフォーム**：レンダリング中に、データが事前入力されたフォームをユーザーがリクエストした場合、Forms OSGi レンダリングサービスはフォームサービスコンテナを呼び出し、結合されたデータを持つ新しいフォーム状態を生成します。ただし、上記の手順ではレイアウトが既に生成されているので、この呼び出しは最初の呼び出しよりも高速です。 この呼び出しは、データの結合を実行し、データに対してスクリプトを実行するだけです。

フォームまたはフォーム内で使用されているアセットに更新がある場合、フォームキャッシュコンポーネントはその更新を検出し、その特定のフォームのキャッシュは無効化されます。Forms OSGi サービスが処理を完了すると、プロファイルレンダラー JSP はこのフォームに JavaScript ライブラリの参照とスタイルを追加し、応答をクライアントに返します。 のような一般的な Web サーバー [Apache](https://httpd.apache.org/) ここでは、HTML圧縮をオンにして使用できます。 Web サーバーは応答サイズ、ネットワークトラフィックおよびサーバーとクライアントマシンの間でのデータのストリーミングに要する時間を大幅に減らします。

ユーザーがフォームを送信すると、ブラウザーはフォームの状態を JSON 形式で[送信サービスプロキシ](../../forms/using/service-proxy.md)に送信し、送信サービスプロキシは JSON データを使用してデータ XML を生成し、そのデータ XML を送信エンドポイントに送信します。

## コンポーネント {#components}

HTML5 フォームを有効にするには、AEM Formsアドオンパッケージが必要です。 AEM Formsアドオンパッケージのインストールについて詳しくは、 [AEM Formsのインストールと設定](../../forms/using/installing-configuring-aem-forms-osgi.md).

### OSGi コンポーネント (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe XFA フォームレンダラー（com.adobe.livecycle.adobe-lc-forms-core）**&#x200B;は、Felix 管理コンソールのバンドルビュー（https://[host]:[port]/system/console/bundles）に表示される際の HTML5 フォーム OSGi バンドルの表示名です。

このコンポーネントには、レンダリング、キャッシュ管理、および設定用の OSGi コンポーネントが含まれます。

#### Forms OSGi Service {#forms-osgi-service}

この OSGi サービスには、XDP をHTMLとしてレンダリングするロジックが含まれ、フォームの送信を処理してデータ XML を生成します。 このサービスは、Formsサービスコンテナを使用します。 Forms サービスコンテナは処理を実行するネイティブコンポーネント `XMLFormService.exe` を内部的に呼び出します。

レンダラーリクエストが受信された場合は、このコンポーネントが Forms サービスコンテナを呼び出してレイアウトおよび状態情報を生成し、この情報がさらに処理されて HTML および JSON フォーム DOM 状態が生成されます。

また、このコンポーネントは、送信されたフォーム状態の JSON からデータ XML を生成します。

#### キャッシュコンポーネント {#cache-component}

HTML5 フォームでは、スループットと応答時間を最適化するためにキャッシュを使用します。 キャッシュサービスのレベルを設定して、パフォーマンスとスペース使用率のトレードオフを微調整できます。

<table>
 <tbody>
  <tr>
   <th>キャッシュ方法</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>なし</td>
   <td>アーティファクトをキャッシュしない<br /> </td>
  </tr>
  <tr>
   <td>保守的</td>
   <td>インラインフラグメントと画像を含むテンプレートなど、フォームのレンダリング前に生成された中間アーティファクトのみをキャッシュします。</td>
  </tr>
  <tr>
   <td>積極的</td>
   <td>キャッシュレンダリングHTMLコンテンツ<br /> 保守的なレベルでキャッシュされたすべてのアーティファクトをキャッシュします。<br /> <strong>注意</strong>:この方法では最高のパフォーマンスが得られますが、キャッシュされたアーティファクトの保存により多くのメモリを消費します。</td>
  </tr>
 </tbody>
</table>

HTML5 フォームは、LRU 戦略を使用してインメモリキャッシュを実行します。 キャッシュ方法が「なし」に設定されている場合、キャッシュは作成されず、既存のキャッシュデータが存在する場合はクリアされます。 キャッシュ方法に加えて、合計インメモリキャッシュサイズも設定できます。これは、キャッシュサイズの最大バインドを持つのに役立ち、それ以上の場合は LRU モードを使用してキャッシュリソースを解放します。

>[!NOTE]
>
>インメモリキャッシュは、クラスターノード間で共有されません。

#### 設定サービス {#configuration-service}

設定サービスを使用すると、Configuration5 Forms の設定パラメーターとキャッシュ設定をHTMLできます。

これらの設定を更新するには、CQ Felix 管理コンソール（https://&lt;&#39;[server]:[port]&#39;/system/console/configMgr で使用可能）に移動し、「Mobile Forms Configuration」を検索して選択します。

設定サービスを使用して、キャッシュサイズを設定したり、キャッシュを無効にしたりできます。 また、Debug Options パラメーターを使用してデバッグを有効にすることもできます。 フォームのデバッグについて詳しくは、[HTML5 フォームのデバッグ](/help/forms/using/debug.md)を参照してください。

### ランタイムコンポーネント (adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

ランタイムパッケージには、HTMLフォームをレンダリングするために使用されるクライアント側ライブラリが含まれています。

**ランタイムパッケージの一部として使用できる重要なコンポーネント：**

#### スクリプトエンジン {#scripting-engine}

AdobeXFA の実装では、フォーム内でユーザー定義のロジックを実行できるように、2 種類のスクリプティング言語がサポートされています。JavaScript と FormCalc

HTMLFormsのスクリプティングエンジンは、これらの両方の言語で XFA スクリプティング API をサポートするために JavaScript で記述されています。

レンダリング時に、FormCalc スクリプトは、ユーザーやデザイナーに対して透過的なサーバー上で JavaScript に変換（およびキャッシュ）されます。

このスクリプティングエンジンは、Object.defineProperty など、ECMAScript5 の機能の一部を使用します。 エンジン／ライブラリはカテゴリ名 **xfaforms.profile** で CQ クライアントライブラリとして提供されます。また、外部ポータルやアプリがフォームとやりとりできるようにする **FormBridge API** も用意されています。FormBridge を使用すると、外部アプリは特定の要素の非表示、値の取得や設定、属性の変更をプログラムで行うことができます。

詳しくは、 [Form Bridge](/help/forms/using/form-bridge-apis.md) 記事。

#### レイアウトエンジン {#layout-engine}

HTML5 フォームのレイアウトと視覚的側面は、SVG1.1、jQuery、BackBone、CSS3 の機能に基づいています。 フォームの初期の外観が生成され、サーバーでキャッシュされます。 最初のレイアウトの調整と、フォームレイアウトに対するさらなる増分変更は、クライアント上で管理されます。 これを実現するために、ランタイムパッケージには、JavaScript で記述され、jQuery/Backbone に基づくレイアウトエンジンが含まれています。 このエンジンは、繰り返し可能なインスタンスの追加/削除、拡大可能なオブジェクトレイアウトなど、すべての動的動作を処理します。 このレイアウトエンジンは、フォームを 1 ページずつレンダリングします。 最初は、1 ページのみを表示し、水平スクロールバーは最初のページのみを表示します。 ただし、ユーザーが下にスクロールすると、次のページのレンダリングが開始されます。 このページごとのレンダリングにより、ブラウザーで最初のページをレンダリングするのに必要な時間が短縮され、フォームの認識されたパフォーマンスが向上します。 このエンジン/ライブラリは、カテゴリ名を持つ CQ クライアントライブラリの一部です **xfaforms.profile**.

レイアウトエンジンには、ユーザーからフォームフィールドの値を取り込むための一連のウィジェットも含まれています。 これらのウィジェットは、 [jQuery UI ウィジェット](https://api.jqueryui.com/jQuery.widget/) Layout エンジンとシームレスに連携するために、特定の追加の契約を実装する

ウィジェットと対応する契約について詳しくは、 [Widget5 フォームのカスタムHTML](/help/forms/using/introduction-widgets.md).

#### スタイル設定 {#styling}

HTML 要素に関連付けられているスタイルは、インラインで追加されるか、埋め込み CSS ブロックに基づいて追加されます。フォームに依存しないいくつかの一般的なスタイルが、xfaforms.profile というカテゴリ名の CQ クライアントライブラリに含まれています。

デフォルトのスタイル設定プロパティに加えて、各フォーム要素には、要素のタイプ、名前、その他のプロパティに基づく特定の CSS クラスも含まれています。 これらのクラスを使用して、独自の CSS を指定することで要素のスタイルを変更できます。

デフォルトのスタイル設定とクラスについて詳しくは、 [スタイルの概要](/help/forms/using/css-styles.md).

#### サーバーサイドスクリプトと Web サービス {#server-side-script-and-web-services}

Web サービスを呼び出すようにマークされた、または実行するようにマークされたスクリプトは、常にサーバー上で実行されます（実行するようにマークされている場所に関係なく）。

クライアントスクリプトエンジン：

1. 現在の Form 状態を JSON 形式で渡して、サーバーへの同期呼び出しをおこないます
1. サーバー上でスクリプトまたは Web サービスを実行します
1. 新しい JSON 状態を生成します
1. 応答が返された場合に、クライアント上の新しい JSON 状態を結合します。

#### ローカリゼーションリソースバンドル {#localization-resource-bundles}

HTML5 フォームはイタリア語（it）、スペイン語（es）、ポルトガル語（ブラジル）（pt_BR）、簡体字中国語（zh_CN）、繁体字中国語（サポート制限有り）（zh_TW）、韓国語（ko_KR）、英語（en_US）、フランス語（fr_FR）、ドイツ語（de_DE）、日本語（ja）をサポートしています。要求ヘッダーで受信されるロケールに基づいて、それに対応するリソースバンドルがクライアントに送信されます。このリソースバンドルはカテゴリ名が **xfaforms.I18N** の CQ クライアントライブラリとして、プロファイル JSP に追加されます。プロファイルでロケールパッケージを取得するロジックを上書きします。

### Sling コンポーネント (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Sling パッケージには、プロファイルとプロファイルレンダラーに関連するコンテンツが含まれています。

#### プロファイル {#profiles}

プロファイルは、フォームまたはFormsファミリーを表す Sling のリソースノードです。 CQ レベルでは、これらのプロファイルは JCR ノードです。 ノードは、 **/content** JCR リポジトリ内のフォルダーと、 **/content** フォルダー。

#### プロファイルレンダラー {#profile-renderers}

Profile ノードにはプロパティがあります **sling:resourceSuperType** 値と共に **xfaforms/profile**. このプロパティは転送リクエストを、**/libs/xfaforms/profile** フォルダーにあるプロファイルノードの Sling スクリプトに内部的に送信します。これらのスクリプトは JSP ページで、HTMLフォームと必要な JS/CSS アーティファクトを組み合わせるためのコンテナです。 ページには、次への参照が含まれます。

* **xfaforms.I18N.&lt;locale>**:このライブラリには、ローカライズされたデータが含まれています。
* **xfaforms.profile**:このライブラリには、XFA スクリプティングおよびレイアウトエンジンの実装が含まれています。

これらのライブラリは、CQ フレームワーク JavaScript ライブラリの自動連結、縮小、圧縮機能の利点を利用する CQ クライアントライブラリとしてモデル化されています。
CQ クライアントライブラリについて詳しくは、「[CQ Clientlib Documentation](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)」を参照してください。

上記のとおり、プロファイルレンダラー JSP は Sling include をとおして Forms サービスをを呼び出します。また、この JSP は、管理設定または要求パラメーターに基づいて様々なデバッグオプションを設定します。

HTML5 フォームを使用することで、開発者はプロファイルとプロファイルレンダラーを作成してフォームの外観をカスタマイズできるようになります。例えば、HTML5 フォームでは、開発者はフォームをパネル内または既存の HTML ポータルの &lt;div> セクションに統合できます。
カスタムプロファイルの作成について詳しくは、「[カスタムプロファイルの作成](/help/forms/using/custom-profile.md)」を参照してください。
