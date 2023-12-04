---
title: SPA およびサーバーサイドレンダリング
description: Adobe Experience ManagerでのSPAとサーバーサイドレンダリングについて説明します。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: a80bc883-e0f6-4714-bd28-108262f96d77
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 85%

---

# SPA およびサーバーサイドレンダリング{#spa-and-server-side-rendering}

>[!NOTE]
>
>SPA Editor は、SPAフレームワークベースのクライアントサイドレンダリング (React やAngularなど ) が必要なプロジェクトで推奨されるソリューションです。

>[!NOTE]
>
>このドキュメントで説明するように、SPAのサーバーサイドレンダリング機能を使用するには、Adobe Experience Manager(AEM)6.5.1.0 以降が必要です。

## 概要 {#overview}

単一ページアプリケーション（SPA）では、使い慣れたネイティブアプリケーションと同様に反応して動作するリッチで動的なエクスペリエンスを提供できます。[これは、コンテンツを事前に読み込こんでからユーザーとのやり取りを処理するという負荷のかかる作業をクライアントにまかせることで](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work)、クライアントとサーバーの間で必要な通信量を最小限に抑え、アプリケーションの反応を良くすることで達成できます。

ただし、SPA のサイズが大きくコンテンツが豊富な場合などは、初期読み込み時間が長くなる可能性があります。読み込み時間を最適化するために、一部のコンテンツをサーバーサイドでレンダリングできます。サーバーサイドレンダリング（SSR）を使用すると、ページの初期読み込みが高速化し、その後、クライアントにさらにレンダリングを渡すことができます。

## SSR を使用するタイミング {#when-to-use-ssr}

SSR が必要なのは一部のプロジェクトだけです。AEM は SPA 向けに JS SSR を完全にサポートしていますが、すべてのプロジェクトに対して体系的に JS SSR を実装することは推奨していません。

SSR を実装することを決定する際には、長期的なメンテナンスを含め、SSR を追加することでプロジェクトにどのような複雑さ、労力、コストをもたらすかをまず評価する必要があります。SSR アーキテクチャは、付加価値が予測コストを明確に上回る場合にのみ選択する必要があります。

次の質問のいずれかへの答えが明確に「はい」である場合、通常、SSR には価値があります。

* **SEO：**&#x200B;トラフィックをもたらす検索エンジンにより、サイトのインデックスを適切に作成するために SSR が実際に必要ですか。メインの検索エンジンクローラーが JS を評価するようになったことに注意してください。
* **ページ速度：** SSR によって実際の環境の速度が大幅に上がり、全体的なユーザーエクスペリエンスが向上しますか。

この 2 つの質問のうち少なくとも 1 つに対して明確に「はい」と答えた場合にのみ、プロジェクトで SSR を実装するようお勧めします。次の節では、Adobe I/O Runtime を使用してこれをおこなう方法について説明します。

## Adobe I/O Runtime {#adobe-i-o-runtime}

[プロジェクトに SSR の実装が必要であると確信できる](/help/sites-developing/spa-ssr.md#when-to-use-ssr)場合、Adobe I/O Runtime を使用したソリューションが推奨されます。

Adobe I/O Runtime について詳しくは、以下を参照してください。

* [https://developer.adobe.com/runtime/](https://developer.adobe.com/runtime/)  — サービスの概要
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs/)  — プラットフォームに関する詳細なドキュメント

次の節では、2 つの異なるモデルで、SPA に SSR を実装する際に Adobe I/O Runtime を使用する方法について詳しく説明します。

* [AEM 主導の通信フロー](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O Runtime 主導の通信フロー](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>アドビでは、環境（ステージング、実稼動、テストなど）ごとに個別の Adobe I/O Runtime ワークスペースを使用することをお勧めします。これにより、異なる環境にデプロイされた単一アプリケーションの異なるバージョンを使用する、一般的なシステム開発ライフサイクル（SDLC）パターンを使用できます。詳しくは、[App Builder アプリケーション用の CI/CD](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) に関するドキュメントを参照してください。
>
>インスタンスタイプごとのランタイム実装に違いがない限り、インスタンス（オーサー、パブリッシュ）ごとに個別のワークスペースは必要ありません。

## リモートレンダラーの設定 {#remote-renderer-configuration}

AEM は、リモートレンダリングされたコンテンツをどこで取得できるかを把握している必要があります。次に関係なく [SSR に実装するモデル](#adobe-i-o-runtime)を使用する場合は、このリモートレンダリングサービスへのアクセス方法をAEMに指定する必要があります。

これは、**RemoteContentRenderer - Configuration Factory OSGi サービス**&#x200B;を介しておこなわれます。`http://<host>:<port>/system/console/configMgr` の Web コンソール設定コンソールで、文字列「RemoteContentRenderer」を検索します。

![レンダラーの設定](assets/rendererconfig.png)

この設定では、次のフィールドを使用できます。

* **コンテンツパスパターン** - 必要に応じて、コンテンツの一部を一致させるための正規表現
* **リモートエンドポイント URL** - コンテンツの生成を担当するエンドポイントの URL。
   * ローカルネットワークにない場合は、保護された HTTPS プロトコルを使用します。
* **追加の要求ヘッダー** - リモートエンドポイントに送信される要求に追加するヘッダー。
   * パターン：`key=value`
* **要求タイムアウト** - リモートホスト要求のタイムアウト（ミリ秒）。

>[!NOTE]
>
>[AEM 駆動の通信フロー](#aem-driven-communication-flow)と [Adobe I/O Runtime 駆動のフロー](#adobe-i-o-runtime-driven-communication-flow)のどちらを実装するかに関係なく、リモートコンテンツレンダラー設定を定義する必要があります。
>
>また、[カスタムの Node.js サーバーを使用する](#using-node-js)場合にも、この設定を定義する必要があります。

>[!NOTE]
>
>この設定では、[リモートコンテンツレンダラー](#remote-content-renderer)を使用します。このレンダラーには、追加の拡張機能とカスタマイズオプションが用意されています。

## AEM 主導の通信フロー {#aem-driven-communication-flow}

SSR を使用する場合、AEM にある SPA の[コンポーネントインタラクションワークフロー](/help/sites-developing/spa-overview.md#workflow)には、Adobe I/O Runtime でアプリの初期コンテンツが生成される段階が含まれます。

1. ブラウザーは AEM から SSR コンテンツを要求します。

1. AEM は、モデルを Adobe I/O Runtime に投稿します。

1. Adobe I/O Runtime は生成されたコンテンツを返します。

1. AEM は、バックエンドページコンポーネントの HTL テンプレートを介して Adobe I/O Runtime から返される HTML を提供します。

![server-side-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime 主導の通信フロー {#adobe-i-o-runtime-driven-communication-flow}

前の節では、AEM がブートストラップとコンテンツの提供を行う場合に、AEM の SPA に関するサーバーサイドレンダリングの標準および推奨される実装について説明しました。

あるいは、SSR を実装して通信フローを効果的に逆転させ、Adobe I/O Runtime がブートストラップをおこなうようにすることもできます。

どちらのモデルも AEM で有効でサポートされています。ただし、特定のモデルを実装する前に、それぞれのメリットとデメリットを考慮する必要があります。

<table>
 <tbody>
  <tr>
   <th><strong>ブートストラップ</strong></th>
   <th><strong>メリット</strong></th>
   <th><strong>デメリット</strong></th>
  </tr>
  <tr>
   <th><strong>AEMを使って</strong><br /> </th>
   <td>
    <ul>
     <li>AEM は必要に応じてライブラリの挿入を管理する</li>
     <li>AEMでのみリソースを管理<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA デベロッパーに馴染みのない場合がある<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>Adobe I/O Runtime 経由<br /> </strong></th>
   <td>
    <ul>
     <li>SPA デベロッパーに馴染みがある<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>CSS や JavaScript などのアプリケーションで必要な Clientlib リソースは、AEMデベロッパーが、 <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> プロパティ<br /> </li>
     <li>リソースは AEM と Adobe I/O Runtime の間で同期する必要がある<br /> </li>
     <li>SPA のオーサリングを可能にするには、Adobe I/O Runtime のプロキシサーバーが必要になる場合がある</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSR の計画 {#planning-for-ssr}

アプリケーションの一部のみがサーバーサイドでレンダリングされる必要があります。 一般的な例として、ページの初回読み込み時に一画面に表示されるコンテンツが、サーバーサイドでレンダリングされます。既にレンダリングされたコンテンツをクライアントに配信することで時間を節約できます。ユーザーが SPA とやり取りすると、追加のコンテンツがクライアントによってレンダリングされます。

SPA にサーバーサイドレンダリングの実装を検討する場合は、アプリのどの部分について必要かを確認してください。

## SSR を使用した SPA の開発 {#developing-an-spa-using-ssr}

SPA コンポーネントは、クライアント（ブラウザー内）またはサーバーサイドでレンダリングできます。サーバーサイドでレンダリングすると、ウィンドウのサイズや位置などのブラウザーのプロパティは存在しません。したがって、SPAのコンポーネントは、レンダリングされる場所を前提としない、同型のものである必要があります。

SSR を使用するには、サーバーサイドレンダリングを担当するAEMとAdobe I/O Runtimeにコードをデプロイします。 ほとんどのコードは同じですが、サーバー固有のタスクは異なります。

## AEM の SPA 向け SSR {#ssr-for-spas-in-aem}

AEM の SPA 向け SSR では、Adobe I/O Runtime が必要です。これは、アプリケーションコンテンツサーバーサイドのレンダリングのために呼び出されます。アプリの HTL 内で、コンテンツをレンダリングするために Adobe I/O Runtime のリソースが呼び出されます。

AEM が標準で Angular および React SPA フレームワークをサポートするのと同様に、Angular および React アプリケーションでもサーバーサイドレンダリングがサポートされています。詳しくは、両方のフレームワークの NPM ドキュメントを参照してください。

* React：[https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular：[https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

単純な例については、 [We.Retail ジャーナルアプリ](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). アプリケーションサーバー側全体をレンダリングします。これは実際の例ではありませんが、SSR の実装に必要な事項を示しています。

>[!CAUTION]
>
>[We.Retail ジャーナルアプリ](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)はデモの目的でのみ使用され、推奨される Adobe I/O Runtime の代わりに、Node.js を単純な例として使用します。この例は、どのプロジェクトの作業にも使用しないでください。

>[!NOTE]
>
>AEM プロジェクトでは、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)を活用します。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を活用します。

## Node.js の使用 {#using-node-js}

Adobe I/O Runtime は、AEM にSPA 用の SSR を実装する場合に推奨されるソリューションです。

オンプレミスの AEM インスタンスの場合は、上記と同じ方法で、カスタム Node.js インスタンスを使用して SSR を実装することもできます。これはアドビでサポートされていますが、お勧めしません。

>[!NOTE]
>
>Node.js は、アドビがホストする AEM インスタンスではサポートされていません。

>[!NOTE]
>
>SSR を Node.js 経由で実装する必要がある場合は、AEM環境（オーサー、パブリッシュ、ステージなど）ごとに個別の Node.js インスタンスを使用することをAdobeにお勧めします。

## リモートコンテンツレンダラー {#remote-content-renderer}

AEM で SSR を SPA と使用するために必要な[リモートコンテンツレンダラー設定](#remote-content-renderer-configuration)は、ニーズに合わせて拡張およびカスタマイズできる、より一般化されたレンダリングサービスです。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` は、Adobe I/O からなど、リモートサーバーでレンダリングされるコンテンツを取得する OSGi サービスです。リモートサーバーに送信されるコンテンツは、渡されたリクエストパラメーターに基づきます。

`RemoteContentRenderingService` は、追加のコンテンツ操作が必要な場合に、カスタム Sling モデルまたはサーブレットに依存関係を反転してインジェクトできます。

このサービスは、[RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet) によって内部的に使用されます。

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

`RemoteContentRendererRequestHandlerServlet` を使用して、要求の設定をプログラムで作成できます。`DefaultRemoteContentRendererRequestHandlerImpl`では、デフォルトのリクエストハンドラーの実装が提供されています。複数の OSGi 設定を作成して、コンテンツ構造内の場所をリモートエンドポイントにマッピングできます。

カスタム要求ハンドラーを追加するには、`RemoteContentRendererRequestHandler` インターフェイスを実装します。`Constants.SERVICE_RANKING` コンポーネントプロパティは、100（`DefaultRemoteContentRendererRequestHandlerImpl` のランク）より大きい整数に設定してください。

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### デフォルトハンドラーの OSGi 設定の作成 {#configure-default-handler}

デフォルトハンドラーの設定は、「[リモートコンテンツレンダラーの設定](#remote-content-renderer-configuration)」の説明に従って作成する必要があります。

### リモートコンテンツレンダラーの使用 {#usage}

サーブレットがページにインジェクト可能なコンテンツを取得して返すには、以下をおこないます。

1. リモートサーバーがアクセス可能であることを確認します。
1. AEM コンポーネントの HTL テンプレートに次のスニペットのいずれかを追加します。
1. 必要に応じて、OSGi 設定を作成または変更します。
1. サイトコンテンツの参照

通常、ページコンポーネントの HTL テンプレートは、この機能のメイン受信者です。

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要件 {#requirements}

このサーブレットでは、Sling モデルエクスポーターを使用してコンポーネントデータをシリアル化します。デフォルトでは、`com.adobe.cq.export.json.ContainerExporter` および `com.adobe.cq.export.json.ComponentExporter` の両方が Sling モデルアダプターとしてサポートされています。必要に応じて、`RemoteContentRendererServlet` を使用して `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses` を実装するように要求を適合させる必要があるクラスを追加できます。追加のクラスは、`ComponentExporter` を拡張する必要があります。
