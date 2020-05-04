---
title: SPAとサーバー側のレンダリング
seo-title: SPAとサーバー側のレンダリング
description: 'null'
seo-description: 'null'
uuid: 27e26e3f-65d4-4069-b570-58b8b9e2a1ae
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 844e5c96-2a18-4869-b4c8-2fb9efe0332a
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af

---


# SPAとサーバー側のレンダリング{#spa-and-server-side-rendering}

>[!NOTE]
>
>SPAエディターは、SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトに推奨されるソリューションです。

>[!NOTE]
>
>このドキュメントで説明するように、SPAサーバー側のレンダリング機能を使用するには、AEM 6.5.1.0以降が必要です。

## 概要 {#overview}

単一ページアプリ(SPA)は、ユーザーを、ネイティブアプリケーションと同様、使い慣れた方法で反応し、動作するリッチで動的なエクスペリエンスとオファーできます。 [これは、クライアントに依存して前もってコンテンツを読み込み、ユーザーの操作を処理する手間が省け](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) 、クライアントとサーバーの間で必要な通信量を最小限に抑え、アプリケーションをより反応しやすくすることで達成できます。

ただし、初期読み込み時間が長くなる可能性があります。特に、SPAのサイズが大きく、コンテンツが豊富な場合に、この方法を使用します。 読み込み時間を最適化するために、コンテンツの一部はサーバーサイドでレンダリングできます。 サーバー側レンダリング(SSR)を使用すると、ページの初期読み込みを高速化し、クライアントにさらにレンダリングを渡すことができます。

## SSRを使用するタイミング {#when-to-use-ssr}

SSRは、すべてのプロジェクトで必要ではありません。 AEMはSPAに対してJS SSRを完全にサポートしていますが、アドビでは、すべてのプロジェクトに対して体系的にJS SSRを実装することをお勧めしません。

SSRの導入を決定する際は、まず、SSRの追加の複雑さ、取り組み、コストの追加について、長期的なメンテナンスを含め、プロジェクトに対してSSRを現実的に示すものを見積もる必要があります。 SSRアーキテクチャは、付加価値が予測コストを明確に上回る場合にのみ選択する必要があります。

次の質問に対して「はい」と明確な意味を持つ場合、通常、SSRは値を提供します。

* **SEO:** トラフィックをもたらす検索エンジンによって、サイトのインデックスを適切に作成するには、SSRが実際に必要ですか。 メインの検索エンジンクローラーがJSを評価するようになったことに注意してください。
* **ページ速度：** SSRは、実際の環境の速度を測定可能に向上させ、全体的なユーザーエクスペリエンスを増やしますか。

お客様のプロジェクトに対して、これら2つの質問のうち少なくとも1つに「はい」と明確な回答があった場合にのみ、アドビはSSRの実装をお勧めします。 Adobe I/O Runtimeを使用してこれを行う方法について、以下の節で説明します。

## Adobe I/Oランタイム {#adobe-i-o-runtime}

プロジェクト [にSSRの実装が必要であると確信できる場合](/help/sites-developing/spa-ssr.md#when-to-use-ssr)は、Adobe I/O Runtimeを使用することを推奨します。

Adobe I/O Runtimeについて詳しくは、

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) — サービスの概要
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) — プラットフォームに関する詳細なドキュメント。

次の節では、SPA用のSSRを実装するためにAdobe I/O Runtimeを使用する方法を2つの異なるモデルで説明します。

* [AEM駆動の通信フロー](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/Oランタイム主導の通信フロー](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>各AEM環境（作成者、発行、ステージなど）に対して、個別のAdobe I/Oランタイムインスタンスを使用することをお勧めします。

## リモートレンダラーの設定 {#remote-renderer-configuration}

AEMは、リモートレンダリングされたコンテンツを取得できる場所を知る必要があります。 SSR [にどのモデルを実装するかに関係なく](#adobe-i-o-runtime) 、AEMに対して、このリモートレンダリングサービスへのアクセス方法を指定する必要があります。

これは、RemoteContentRenderer - Configuration Factory OSGiサー **ビスを介して行われます**。 のWebコンソール設定コンソールで、文字列「RemoteContentRenderer」を検索し `http://<host>:<port>/system/console/configMgr`ます。

![レンダラーの設定](assets/rendererconfig.png)

この設定では、次のフィールドを使用できます。

* **コンテンツパスパターン** — 必要に応じて、コンテンツの一部を一致させるための正規式。
* **リモートエンドポイントURL** — コンテンツの生成を担当するエンドポイントのURL。
   * ローカルネットワークにない場合は、保護されたHTTPSプロトコルを使用します。
* **追加の要求ヘッダー** — リモートエンドポイントに送信される要求に追加するヘッダー
   * パターン: `key=value`
* **要求タイムアウト** — リモートホスト要求のタイムアウト（ミリ秒）

>[!NOTE]
>
>[AEM駆動の通信フロー](#aem-driven-communication-flow) 、または [](#adobe-i-o-runtime-driven-communication-flow) Adobe I/Oランタイム駆動フローを実装する場合には、リモートコンテンツレンダラーの設定を定義する必要があります。
>
>また、カスタムNode.jsサーバーを [使用する場合は、この設定も定義する必要があります。](#using-node-js)

>[!NOTE]
>
>この設定では、 [リモートコンテンツレンダラーが利用されます。このレンダラーには](#remote-content-renderer) 、追加の拡張機能とカスタマイズオプションが用意されています。

## AEM駆動の通信フロー {#aem-driven-communication-flow}

SSRを使用する場合、AEMのSPAの [コンポーネント対話ワークフロー](/help/sites-developing/spa-overview.md#workflow) には、Adobe I/O Runtimeでアプリの初期コンテンツが生成される段階が含まれます。

1. ブラウザーがAEMからSSRコンテンツを要求します。

1. AEMは、モデルをAdobe I/O Runtimeに投稿します。

1. Adobe I/O Runtimeは、生成されたコンテンツを返します。

1. AEMは、Adobe I/O RuntimeがバックエンドページコンポーネントのHTLテンプレートを介して返すHTMLを提供します。

![server-side-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/Oランタイム主導の通信フロー {#adobe-i-o-runtime-driven-communication-flow}

前の節では、AEMでSPAに関するサーバー側レンダリングの標準実装および推奨実装について説明します。AEMでは、コンテンツのブートストラップと提供を実行します。

または、Adobe I/O Runtimeがブートストラップを行い、通信フローを効果的に逆にするようにSSRを実装することもできます。

両方のモデルが有効で、AEMでサポートされています。 ただし、特定のモデルを実装する前に、それぞれのメリットとデメリットを考慮する必要があります。

<table>
 <tbody>
  <tr>
   <th><strong>ブートストラップ</strong></th>
   <th><strong>メリット</strong></th>
   <th><strong>デメリット</strong></th>
  </tr>
  <tr>
   <th><strong>AEM経由</strong><br /> </th>
   <td>
    <ul>
     <li>必要に応じてAEMが注入ライブラリを管理</li>
     <li>リソースはAEMでのみ維持する必要があります<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA開発者に馴染みのないものと思われる<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>（Adobe I/O Runtimeを使用）<br /> </strong></th>
   <td>
    <ul>
     <li>SPA開発者に詳しい<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>CSSやJavaScriptなどのアプリケーションに必要なClientlibリソースは、AEM開発者が <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> プロパティを使用して利用できるようにする必要があります<br /> </li>
     <li>AEMとAdobe I/O Runtimeの間でリソースを同期する必要がある<br /> </li>
     <li>SPAのオーサリングを有効にするには、Adobe I/O Runtimeのプロキシサーバーが必要な場合があります</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSRの計画 {#planning-for-ssr}

通常は、アプリケーションの一部のみをサーバー側でレンダリングする必要があります。 一般的な例として、ページの初回読み込み時に一画面に表示されるコンテンツはサーバー側に表示されます。 これにより、既にレンダリングされたコンテンツをクライアントに配信することで時間を節約できます。 ユーザーがSPAとやり取りすると、追加のコンテンツがクライアントによってレンダリングされます。

SPAに対してサーバー側のレンダリングを実装する場合は、アプリのどの部分が必要かを確認する必要があります。

## SSRを使用したSPAの開発 {#developing-an-spa-using-ssr}

SPAコンポーネントは、クライアント（ブラウザー内）またはサーバー側でレンダリングできます。 サーバー側がレンダリングされる場合、ウィンドウのサイズや場所などのブラウザープロパティは存在しません。 したがって、SPAコンポーネントは同形的である必要があり、レンダリングされる場所を前提としません。

SSRを利用するには、コードをAEMにデプロイするほか、サーバー側のレンダリングを担当するAdobe I/O Runtimeにデプロイする必要があります。 ほとんどのコードは同じですが、サーバー固有のタスクは異なります。

## AEMのSPA用SSR {#ssr-for-spas-in-aem}

AEMのSPA用SSRにはAdobe I/O Runtimeが必要です。これは、アプリケーションコンテンツサーバー側のレンダリングに対して呼び出されます。 アプリケーションのHTL内で、Adobe I/O Runtimeのリソースが呼び出され、コンテンツがレンダリングされます。

AEMがAngularおよびReact SPAフレームワークをサポートするように、AngularおよびReactアプリでもサーバー側のレンダリングがサポートされます。 詳しくは、両方のフレームワークのNPMドキュメントを参照してください。

* 反応： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* 角度： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

単純な例については、 [We.Retailジャーナルアプリを参照してください](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)。 アプリケーションサーバー側全体がレンダリングされます。 これは実際の例ではありませんが、SSRの実装に必要なものを示しています。

>[!CAUTION]
>
>We. [Retailジャーナルアプリはデモ目的でのみ使用され](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 、推奨されるAdobe I/Oランタイムの代わりに、Node.jsを単純な例として使用します。 この例は、どのプロジェクト作業にも使用しないでください。

>[!NOTE]
>
>AEMプロジェクトは、ReactまたはAngularを使用してSPAプロジェクトをサポートし、SPA SDKを利用する [AEMプロジェクトアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)を活用する必要があります。

## Node.jsの使用 {#using-node-js}

AEMでSPAにSSRを実装する場合、Adobe I/O Runtimeが推奨されるソリューションです。

オンプレミスAEMインスタンスの場合は、上記と同様に、カスタムNode.jsインスタンスを使用してSSRを実装することもできます。 これはアドビでサポートされていますが、お勧めしません。

>[!NOTE]
>
>Node.jsは、アドビがホストするAEMインスタンスではサポートされていません。

>[!NOTE]
>
>SSRをNode.js経由で実装する必要がある場合、アドビでは各AEM環境（作成者、発行、ステージなど）に個別のNode.jsインスタンスを割り当てることをお勧めします。

## リモートコンテンツレンダラー {#remote-content-renderer}

AEMでSSRをSPAと共に使用するために必要な [リモートコンテンツレンダラー設定](#remote-content-renderer-configuration) （SSRをSPAと共に使用する場合）は、ニーズに合わせて拡張およびカスタマイズできる、より汎用的なレンダリングサービスにタップします。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` は、Adobe I/Oなどのリモートサーバーでレンダリングされるコンテンツを取得するOSGiサービスです。 リモートサーバーに送信されるコンテンツは、渡されたリクエストパラメーターに基づきます。

`RemoteContentRenderingService` は、追加のコンテンツ操作が必要な場合に、カスタムSlingモデルまたはサーブレットに依存関係を反転して挿入できます。

このサービスは、RemoteContentRendererRequestHandlerServletによって内部的に使用され [ます](#remotecontentrendererrequesthandlerservlet)。

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

を使用 `RemoteContentRendererRequestHandlerServlet` して、リクエストの設定をプログラムで設定できます。 `DefaultRemoteContentRendererRequestHandlerImpl`では、デフォルトのリクエストハンドラーの実装が提供されており、コンテンツ構造内の場所をリモートエンドポイントにマップするために、複数のOSGi設定を作成できます。

カスタム要求ハンドラーを追加するには、インター `RemoteContentRendererRequestHandler` フェイスを実装します。 コンポーネントのプロパティは、100より大きい整数（ランク）に設定して `Constants.SERVICE_RANKING` く `DefaultRemoteContentRendererRequestHandlerImpl`ださい。

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### デフォルトハンドラのOSGi設定の設定 {#configure-default-handler}

デフォルトハンドラーの設定は、「 [リモートコンテンツレンダラーの設定](#remote-content-renderer-configuration)」の説明に従って設定する必要があります。

### リモートコンテンツレンダラーの使用 {#usage}

サーブレットがページに挿入可能なコンテンツを取得して返すには：

1. リモートサーバーがアクセス可能であることを確認します。
1. AEMコンポ追加ーネントのHTLテンプレートに関する以下のスニペットの1つです。
1. 必要に応じて、OSGi設定を作成または変更します。
1. サイトのコンテンツを参照する

通常、ページコンポーネントのHTLテンプレートは、この機能のメイン受信者です。

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要件 {#requirements}

このサーブレットでは、Slingモデルエクスポーターを利用してコンポーネントデータをシリアライズします。 デフォルトでは、との両方がSlingモデルアダプタ `com.adobe.cq.export.json.ContainerExporter` としてサポート `com.adobe.cq.export.json.ComponentExporter` されています。 必要に応じて、リクエストを適用してを使用し実装する必要があるクラス `RemoteContentRendererServlet` を追加でき `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`ます。 追加のクラスは、を拡張する必要があり `ComponentExporter`ます。
