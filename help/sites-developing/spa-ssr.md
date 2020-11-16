---
title: SPAおよびサーバー側のレンダリング
seo-title: SPAおよびサーバー側のレンダリング
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
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 1%

---


# SPAおよびサーバー側のレンダリング{#spa-and-server-side-rendering}

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

>[!NOTE]
>
>SPAサーバー側のレンダリング機能を使用するには、このドキュメントで説明するようにAEM 6.5.1.0以降が必要です。

## 概要 {#overview}

シングルページアプリ(SPA)では、ユーザーに対して、ネイティブアプリケーションと同様、慣れ親しんだ方法で反応し、動作するリッチで動的なエクスペリエンスをオファーできます。 [これは、クライアントに依存して前もってコンテンツを読み込み、ユーザーの操作を処理する手間が省け](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) 、クライアントとサーバーの間で必要な通信量を最小限に抑えて、アプリケーションをより反応しやすくすることで達成できます。

ただし、SPAのサイズが大きく、コンテンツが豊富な場合など、初期読み込み時間が長くなる可能性があります。 読み込み時間を最適化するために、コンテンツの一部はサーバーサイドでレンダリングできます。 サーバー側レンダリング(SSR)を使用すると、ページの初期読み込みを高速化し、クライアントにさらにレンダリングを渡すことができます。

## SSRを使用するタイミング {#when-to-use-ssr}

SSRは、すべてのプロジェクトで必要ではありません。 AEMはSPA向けにJS SSRを完全にサポートしていますが、Adobeは、すべてのプロジェクトに対して体系的にJS SSRを実装することを推奨しません。

SSRの導入を決定する際は、まず、SSRの追加の複雑さ、取り組み、コストの追加について、長期的なメンテナンスを含め、プロジェクトに対してSSRを現実的に示すものを見積もる必要があります。 SSRアーキテクチャは、付加価値が予測コストを明確に上回る場合にのみ選択する必要があります。

次の質問に対して「はい」と明確な意味を持つ場合、通常、SSRは値を提供します。

* **SEO:** トラフィックをもたらす検索エンジンによって、サイトのインデックスを適切に作成するには、SSRが実際に必要ですか。 メインの検索エンジンクローラーがJSを評価するようになったことに注意してください。
* **ページ速度：** SSRは、実際の環境の速度を測定可能に向上させ、全体的なユーザーエクスペリエンスを増やしますか。

この2つの質問のうち少なくとも1つに対し、明確な「はい」を付けて回答した場合にのみ、プロジェクトでSSRの実装がAdobeに推奨されます。 次の節では、Adobe I/O Runtimeを使ってこれを行う方法について説明します。

## Adobe I/O Runtime {#adobe-i-o-runtime}

プロジェクト [にSSRの実装が必要であると確信でき](/help/sites-developing/spa-ssr.md#when-to-use-ssr)る場合は、Adobeが推奨するソリューションはAdobe I/O Runtimeを使用することです。

Adobe I/O Runtimeについて詳しくは、

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) — サービスの概要
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) — プラットフォームに関する詳細なドキュメント。

次の節では、2つの異なるモデルで、SPAにSSRを実装する際にAdobe I/O Runtimeを使用する方法について詳しく説明します。

* [AEM主導の通信フロー](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O Runtime主導の通信流](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobeでは、AEM環境（作成者、発行、ステージなど）ごとに個別のAdobe I/O Runtimeインスタンスを作成することをお勧めします。

## リモートレンダラーの設定 {#remote-renderer-configuration}

AEMは、リモートレンダリングされたコンテンツをどこで取得できるかを知っている必要があります。 SSRにどのモデル [を実装するかに関係なく](#adobe-i-o-runtime) 、AEMにこのリモートレンダリングサービスへのアクセス方法を指定する必要があります。

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
>AEM駆動の通信フロー [、](#aem-driven-communication-flow) Adobe I/O Runtime駆動のフローのどちらを実装するかに関係なく、リモートコンテンツレンダラー設定を定義する必要があり [](#adobe-i-o-runtime-driven-communication-flow) ます。
>
>また、カスタムNode.jsサーバーを [使用する場合は、この設定も定義する必要があります。](#using-node-js)

>[!NOTE]
>
>この設定では、 [リモートコンテンツレンダラーが利用されます。このレンダラーには](#remote-content-renderer) 、追加の拡張機能とカスタマイズオプションが用意されています。

## AEM主導の通信フロー {#aem-driven-communication-flow}

SSRを使用する場合、AEMのSPAの [コンポーネントインタラクションワークフロー](/help/sites-developing/spa-overview.md#workflow) には、Adobe I/O Runtimeでアプリの初期コンテンツが生成される段階が含まれます。

1. ブラウザはAEMからSSRコンテンツを要求します。

1. AEMは、モデルをAdobe I/O Runtimeに投稿します。

1. Adobe I/O Runtimeは生成されたコンテンツを返します。

1. AEMは、バックエンドページコンポーネントのHTLテンプレートを介してAdobe I/O Runtimeから返されるHTMLを提供します。

![server-side-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime主導の通信流 {#adobe-i-o-runtime-driven-communication-flow}

前の節では、AEMのSPAでAEMがコンテンツのブートストラップと提供を実行する場合に、サーバー側のレンダリングの標準的な実装および推奨される実装について説明します。

あるいは、SSRを実装して、Adobe I/O Runtimeが通信フローを効果的に逆転させ、ブートストラップを行うようにすることもできます。

どちらのモデルも有効で、AEMではサポートされています。 ただし、特定のモデルを実装する前に、それぞれのメリットとデメリットを考慮する必要があります。

<table>
 <tbody>
  <tr>
   <th><strong>ブートストラップ</strong></th>
   <th><strong>メリット</strong></th>
   <th><strong>デメリット</strong></th>
  </tr>
  <tr>
   <th><strong>aem経由</strong><br /> </th>
   <td>
    <ul>
     <li>AEMは、必要に応じてライブラリの挿入を管理</li>
     <li>リソースはAEMでのみ保守する必要がある<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA開発者に馴染みのない<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>adobe i/o runtime経由<br /> </strong></th>
   <td>
    <ul>
     <li>SPA開発者の知り合い<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>CSSやJavaScriptなどのアプリケーションに必要なClientlibリソースは、AEM開発者が <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> プロパティを使用して使用できるようにする必要があります<br /> </li>
     <li>リソースはAEMとAdobe I/O Runtimeの間で同期する必要があります<br /> </li>
     <li>SPAのオーサリングを可能にするには、Adobe I/O Runtimeのプロキシサーバが必要になる場合があります</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSRの計画 {#planning-for-ssr}

通常は、アプリケーションの一部のみをサーバー側でレンダリングする必要があります。 一般的な例として、ページの初回読み込み時に一画面に表示されるコンテンツはサーバー側に表示されます。 これにより、既にレンダリングされたコンテンツをクライアントに配信することで時間を節約できます。 ユーザーがSPAとやり取りすると、追加のコンテンツがクライアントによってレンダリングされます。

SPAに対してサーバー側のレンダリングを実装する場合は、アプリのどの部分が必要かを確認する必要があります。

## SSRを使用したSPAの開発 {#developing-an-spa-using-ssr}

SPAコンポーネントは、クライアント（ブラウザー内）またはサーバー側でレンダリングできます。 サーバー側がレンダリングされる場合、ウィンドウのサイズや場所などのブラウザープロパティは存在しません。 したがって、SPAのコンポーネントは同形的なものであり、レンダリングされる場所を前提としません。

SSRを利用するには、サーバ側のレンダリングを担当するAdobe I/O Runtimeだけでなく、AEMにもコードをデプロイする必要があります。 ほとんどのコードは同じですが、サーバー固有のタスクは異なります。

## AEMのSPA向けSSR {#ssr-for-spas-in-aem}

AEMのSPA向けSSRでは、Adobe I/O Runtimeが必要です。これは、アプリケーションコンテンツサーバー側のレンダリングのために呼び出されます。 アプリのHTL内で、コンテンツをレンダリングするためにAdobe I/O Runtimeのリソースが呼び出されます。

AEMが標準でAngularおよびReact SPAフレームワークをサポートするのと同様に、AngularおよびReactアプリケーションでもサーバー側のレンダリングがサポートされます。 詳しくは、両方のフレームワークのNPMドキュメントを参照してください。

* 反応： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* 角度： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

単純な例については、 [We.Retailジャーナルアプリを参照してください](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)。 アプリケーションサーバー側全体がレンダリングされます。 これは実際の例ではありませんが、SSRの実装に必要なものを示しています。

>[!CAUTION]
>
>[We.Retailジャーナルアプリは、デモ目的でのみ使用され](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 、推奨されるAdobe I/O Runtimeではなく、単純な例としてNode.jsを使用します。 この例は、どのプロジェクト作業にも使用しないでください。

>[!NOTE]
>
>AEMプロジェクトでは、 [AEM Project Archetype](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)（プロジェクトアーキタイプ）を活用する必要があります。このアーキタイプは、ReactまたはAngularを使用するSPAプロジェクトをサポートし、SPA SDKを利用します。

## Node.jsの使用 {#using-node-js}

Adobe I/O Runtimeは、AEMでSPAにSSRを実装する場合に推奨されるソリューションです。

オンプレミスAEMインスタンスの場合は、上記と同様に、カスタムNode.jsインスタンスを使用してSSRを実装することもできます。 これはAdobeでサポートされていますが、お勧めしません。

>[!NOTE]
>
>Node.jsは、AdobeがホストするAEMインスタンスではサポートされていません。

>[!NOTE]
>
>SSRをNode.js経由で実装する必要がある場合、AdobeではAEM環境（作成者、発行、ステージなど）ごとに個別のNode.jsインスタンスを推奨します。

## リモートコンテンツレンダラー {#remote-content-renderer}

AEMでSPAのでSSRを使用するために必要な [リモートコンテンツレンダラー設定](#remote-content-renderer-configuration) （をタップすると、ニーズに合わせて拡張およびカスタマイズできる、より汎用的なレンダリングサービスが提供されます）。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` は、AdobeI/Oからなど、リモートサーバーでレンダリングされるコンテンツを取得するOSGiサービスです。リモートサーバーに送信されるコンテンツは、渡されたリクエストパラメーターに基づきます。

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
1. AEMコンポ追加ーネントのHTLテンプレートに対する次のスニペットの1つです。
1. 必要に応じて、OSGi設定を作成または変更します。
1. サイトのコンテンツを参照する

通常、ページコンポーネントのHTLテンプレートは、この機能のメイン受信者です。

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要件 {#requirements}

このサーブレットでは、Slingモデルエクスポーターを利用してコンポーネントデータをシリアライズします。 デフォルトでは、との両方がSlingモデルアダプタ `com.adobe.cq.export.json.ContainerExporter` としてサポート `com.adobe.cq.export.json.ComponentExporter` されています。 必要に応じて、リクエストを適用してを使用し実装する必要があるクラス `RemoteContentRendererServlet` を追加でき `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`ます。 追加のクラスは、を拡張する必要があり `ComponentExporter`ます。
