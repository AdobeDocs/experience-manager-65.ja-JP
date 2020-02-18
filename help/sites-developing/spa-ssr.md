---
title: SPAとサーバ側のレンダリング
seo-title: SPAとサーバ側のレンダリング
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
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPAとサーバ側のレンダリング{#spa-and-server-side-rendering}

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

>[!NOTE]
>
>このドキュメントで説明するSPAサーバー側のレンダリング機能を使用するには、AEM 6.5.1.0以降が必要です。

## 概要 {#overview}

シングルページアプリ(SPA)は、ネイティブアプリケーションと同様に、使い慣れた方法で反応し、動作するリッチで動的なエクスペリエンスをユーザーに提供します。 [これは、クライアントを利用して前方にコンテンツを読み込み、ユーザー操作の処理を大幅に短縮し](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) 、クライアントとサーバー間の通信量を最小限に抑えて、アプリの反応性を高めることで達成されます。

ただし、特にSPAが大きく、コンテンツに富む場合は、初期読み込み時間が長くなる可能性があります。 読み込み時間を最適化するために、コンテンツの一部はサーバー側でレンダリングできます。 サーバー側レンダリング(SSR)を使用すると、ページの初期読み込みを高速化し、さらにクライアント上でレンダリングを渡すことができます。

## SSRを使用するタイミング {#when-to-use-ssr}

SSRは、すべてのプロジェクトで必要とされるわけではありません。 AEMはSPAに対してJS SSRを完全にサポートしていますが、アドビでは、すべてのプロジェクトに対して体系的に実装することをお勧めしません。

SSRの導入を決定する際は、まず、SSRの追加的な複雑さ、労力、およびコストの追加が、長期保守を含む、プロジェクトに対してリアルに表現されるものを見積もる必要があります。 SSRアーキテクチャは、加算値が見積もりコストを明確に超える場合にのみ選択する必要があります。

SSRは、次の質問のいずれかに対して明確な「はい」がある場合、通常、ある程度の値を提供します。

* **** SEO:トラフィックをもたらす検索エンジンによってサイトのインデックスが正しく作成されるには、SSRが実際には必要ですか。 メインの検索エンジンクローラーがJSを評価するようになりました。
* **** ページ速度：SSRは、実生活環境における測定可能なスピードの向上を実現し、全体的なユーザーエクスペリエンスに追加しますか。

お客様のプロジェクトに対して、これら2つの質問のうち少なくとも1つが明確な「はい」を使用して回答された場合にのみ、アドビはSSRの実装を推奨します。 以下の節では、Adobe I/O Runtimeを使用してこれを行う方法について説明します。

## Adobe I/Oランタイム {#adobe-i-o-runtime}

プロジェクト [にSSRの実装が必要であることが確実な場合は、アドビの推奨ソリューションは](/help/sites-developing/spa-ssr.md#when-to-use-ssr)、Adobe I/O Runtimeを使用することです。

Adobe I/O Runtimeについて詳しくは、

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) — サービスの概要
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) — プラットフォームに関する詳細なドキュメント

次の節では、Adobe I/O Runtimeを使用してSPAにSSRを実装する方法を2つの異なるモデルについて説明します。

* [AEM主導型通信フロー](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/Oランタイム主導型通信フロー](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>アドビでは、AEM環境（作成者、発行、ステージなど）ごとに別々のAdobe I/Oランタイムインスタンスを使用することをお勧めします。

## AEM主導型通信フロー {#aem-driven-communication-flow}

SSRを使用する場合、AEMの [SPAのコンポーネントインタラクションワークフローに](/help/sites-developing/spa-overview.md#workflow) 、Adobe I/O Runtimeでアプリの初期コンテンツが生成される段階が含まれます。

1. ブラウザーがAEMからSSRコンテンツを要求します。

1. AEMは、モデルをAdobe I/O Runtimeに投稿します。

1. Adobe I/O Runtimeは、生成されたコンテンツを返します。

1. AEMは、Adobe I/O RuntimeがバックエンドページコンポーネントのHTLテンプレートを介して返すHTMLを提供します。

![server-side-rendering-cms-drivenamenode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/Oランタイム主導型通信フロー {#adobe-i-o-runtime-driven-communication-flow}

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
     <li>AEMは必要な場所でライブラリの挿入を管理</li>
     <li>リソースはAEMでのみ維持する必要があります<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA開発者に馴染みのない可能性がある<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>adobe I/O Runtimeを使用<br /> </strong></th>
   <td>
    <ul>
     <li>SPA開発者にとってより親しみのある方法<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>CSSやJavaScriptなどのアプリケーションに必要なClientlibリソースは、AEM開発者がプロパティを介して使用できるようにする必要があり <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> ます<br /> </li>
     <li>リソースはAEMとAdobe I/O Runtimeの間で同期する必要があります<br /> </li>
     <li>SPAのオーサリングを有効にするには、Adobe I/O Runtimeのプロキシサーバーが必要な場合があります</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSRの計画 {#planning-for-ssr}

通常、サーバー側でレンダリングする必要があるのはアプリケーションの一部のみです。 一般的な例は、ページの初回読み込み時に一画面に表示されるコンテンツがサーバー側にレンダリングされることです。 これにより、既にレンダリングされたコンテンツをクライアントに配信することで、時間を節約できます。 ユーザーがSPAを操作すると、追加のコンテンツがクライアントによってレンダリングされます。

SPAに対してサーバー側のレンダリングを実装する場合は、アプリケーションのどの部分が必要かを確認する必要があります。

## SSRを使用したSPAの開発 {#developing-an-spa-using-ssr}

SPAコンポーネントは、クライアント（ブラウザー内）またはサーバー側でレンダリングできます。 サーバー側でレンダリングする場合、ウィンドウサイズや場所などのブラウザープロパティは存在しません。 したがって、SPAコンポーネントは同形的で、レンダリングされる場所を前提としません。

SSRを利用するには、コードをAEMにデプロイするだけでなく、サーバー側のレンダリングを担当するAdobe I/O Runtimeにデプロイする必要があります。 ほとんどのコードは同じですが、サーバー固有のタスクは異なります。

## AEMのSPA用SSR {#ssr-for-spas-in-aem}

AEMのSPA用SSRにはAdobe I/O Runtimeが必要です。これは、アプリケーションコンテンツサーバー側のレンダリングに呼び出されます。 アプリケーションのHTL内で、Adobe I/O Runtime上のリソースが呼び出され、コンテンツがレンダリングされます。

AEMがAngularおよびReact SPAフレームワークをサポートするのと同様に、AngularおよびReactアプリでもサーバー側のレンダリングがサポートされます。 詳しくは、両方のフレームワークに関するNPMのドキュメントを参照してください。

* 反応：https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component [](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* 角度：https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component [](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

簡単な例については、 [We.Retail Journalアプリを参照してください](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)。 アプリケーションサーバー側全体がレンダリングされます。 これは実際の例ではありませんが、SSRの実装に必要なものを示しています。

>[!CAUTION]
>
>We.Retail Journalア [プリはデモ用にのみ使用されるので](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 、推奨されるAdobe I/O Runtimeの代わりにNode.jsを単純な例として使用します。 この例は、どのプロジェクト作業にも使用しないでください。

>[!NOTE]
>
>AEM上のすべてのSPAプロジェクトは、SPAスターターキットの [Mavenアーキタイプに基づく必要があります](https://github.com/adobe/aem-spa-project-archetype)。

## Node.jsの使用 {#using-node-js}

AEMでSPAにSSRを実装する場合は、Adobe I/O Runtimeが推奨されるソリューションです。

オンプレミスAEMインスタンスの場合は、上記と同じ方法で、カスタムNode.jsインスタンスを使用してSSRを実装することもできます。 これはアドビでサポートされていますが、お勧めしません。

>[!NOTE]
>
>Node.jsは、アドビがホストするAEMインスタンスに対してはサポートされていません。

>[!NOTE]
>
>SSRをNode.js経由で実装する必要がある場合、アドビでは各AEM環境（作成者、発行、ステージなど）に対して個別のNode.jsインスタンスを使用することをお勧めします。
