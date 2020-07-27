---
title: HTML5 forms 用のフォームテンプレートのレンダリング
seo-title: HTML5 forms 用のフォームテンプレートのレンダリング
description: HTML5 forms のプロファイルは、プロファイルレンダリングに関連付けられています。プロファイルレンダラーは Forms OSGi サービスを呼び出すことでフォームの HTML 表現を生成する役割を持つ JSP ページです。
seo-description: HTML5 forms のプロファイルは、プロファイルレンダリングに関連付けられています。プロファイルレンダラーは Forms OSGi サービスを呼び出すことでフォームの HTML 表現を生成する役割を持つ JSP ページです。
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 79%

---


# HTML5 forms 用のフォームテンプレートのレンダリング {#rendering-form-template-for-html-forms}

## レンダリングエンドポイント {#render-endpoint}

HTML5 forms have the notion of **Profiles** which are exposed as REST Endpoints to enable Mobile Rendering of Form Templates. These Profiles have associated **Profile Renderer**. これらは、Forms OSGiサービスを呼び出してフォームのHTML表現を生成する役割を持つJSPページです。 Profile ノードの JCR パスがレンダリングエンドポイントの URL を決定します。「default」プロファイルを指す、フォームのデフォルトのレンダリングエンドポイントは次のようになります。

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*path of the folder containg form xdp*>&amp;template=&lt;*name of the xdp*>

例：`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

カスタムプロファイルでは、それに応じてエンドポイントが変わります。たとえば、hrforms の名前を持つカスタムプロファイルのエンドポイントは：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

テンプレートが FormSubmission と呼ばれるアプリケーションの AEM リポジトリにある場合、URI は次のとおりです。

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## レンダリングパラメーター {#render-parameters}

次に、HTML 形式でフォームをレンダリングする場合にサポートされるリクエストパラメーターを示します。

<table>
 <tbody>
  <tr>
   <th><strong>パラメーター </strong></th>
   <th><strong>説明</strong></th>
  </tr>
  <tr>
   <td>テンプレート<br /> </td>
   <td>このパラメーターはテンプレートファイルの名前を指定します。<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>このパラメーターはテンプレートとそれに関連するリソースが存在するパスを指定します。このパスにはサーバーのファイルシステムパス、リポジトリパス、http または ftp パスを使用できます。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>このパラメーターはフォームのデータ XML がポストされる URL を指定します。<br /> </td>
  </tr>
 </tbody>
</table>

### フォームテンプレートとのデータの結合 {#merge-data-with-form-template}

| パラメーター | 説明 |
|---|---|
| dataRef | このパラメーターはテンプレートと結合されるデータファイルの&#x200B;**絶対パス**&#x200B;を指定します。このパラメーターには、xml形式でデータを返すRESTサービスへのURLを指定できます。 |
| data | このパラメーターはテンプレートと結合される UTF-8 エンコードされたデータバイトを指定します。このパラメーターが指定されている場合、HTML5 form は dataRef パラメーターを無視します。 |

### レンダリングパラメーターの送信 {#passing-the-render-parameter}

HTML5 forms は 3 つの方法によるレンダリングパラメーターの送信をサポートしています。URL、キー値ペア、およびプロファイルノードを使用してパラメーターを渡すことができます。レンダリングパラメーターでは、キー値ペアは最高の優先度を持ち、プロファイルノードがその次に高い優先度を持ちます。URLリクエストパラメーターは最も優先度が低いパラメーターです。

* **URL リクエストパラメーター**: レンダリングパラメーターを URL で指定できます。 URL リクエストパラメーターでは、パラメーターはエンドユーザーに対して表示されます。For example, the following submit URL contains template parameter in the URL: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute リクエストパラメーター**: レンダリングパラメーターをキー値ペアとして指定できます。 SetAttribute リクエストパラメーターでは、パラメーターはエンドユーザーに対して表示されません。リクエストを他の JSP から HTML5 form のプロファイルレンダラ― JSP に転送し、リクエストオブジェクトで *setAttribute* を使用してすべてのレンダリングパラメーターを渡すことができます。この方法は最高の優先度を持ちます。

* **プロファイルノードリクエストパラメーター：** レンダリングパラメータは、プロファイルノードのノードプロパティとして指定できます。 プロファイルノードリクエストパラメーターでは、パラメーターはエンドユーザーに対して表示されません。プロファイルノードは、リクエストが送信されるノードです。パラメーターをノードプロパティとして指定するには、CRXDE lite を使用します。

### 送信パラメーター {#submit-parameters}

HTML5 forms はデータを送信し、サーバー側スクリプトおよび Web サービスを AEM サーバーで実行します。サーバー側スクリプトと Web サービスを AEM サーバーで実行するために使用するパラメーターについて詳しくは、[HTML5 フォームサービスプロキシ](/help/forms/using/service-proxy.md)を参照してください。
