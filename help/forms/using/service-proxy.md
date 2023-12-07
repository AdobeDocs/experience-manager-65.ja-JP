---
title: HTML5 forms サービスプロキシ
description: HTML5 Forms サービスプロキシは、送信サービスのプロキシを登録する設定です。 サービスプロキシを設定するには、リクエストパラメータ submissionServiceProxy を使用して送信サービスの URL を指定します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 8f9b10ae-1600-49c2-a061-153a2a89c67e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 29%

---

# HTML5 forms サービスプロキシ{#html-forms-service-proxy}

HTML5 Forms サービスプロキシは、送信サービスのプロキシを登録する設定です。 サービスプロキシを設定するには、リクエストパラメーターを使用して送信サービスの URL を指定します *submissionServiceProxy*.

## サービスプロキシの利点 {#benefits-of-service-proxy-br}

サービスプロキシは次の問題点を解消します。

* HTML5 Forms ワークフローでは、HTML5 Forms ユーザーの送信サービス「/content/xfaforms/submission/default」を開く必要があります。 これにより、AEMサーバーが意図しない閲覧者にさらに公開されます。
* サービス URL は、フォームのランタイムモデルに埋め込まれます。 サービス URL パスを変更することはできません。
* 送信は 2 段階のプロセスです。 フォームデータを送信するには、サーバーに少なくとも 2 つのジャーニーが必要です。 したがって、サーバーの負荷が増加します。
* HTML5 forms は、PDF リクエストの代わりに POST リクエストでデータを送信します。PDF と HTML5 forms の両方が関与するワークフローの場合、2 つの異なる方法による送信処理が必要となります。

### トポロジー {#topologies-br}

HTML5 フォームは、次のトポロジを使用してAEMサーバーに接続できます。

* AEM Server またはHTML5 forms がサーバーにPOSTを介してデータを送信するトポロジー。
* プロキシサーバーが POST データをサーバーに送信するトポロジー。

![HTML5 forms サービスプロキシのトポロジー](assets/topology.png)

HTML5 forms サービスプロキシのトポロジー

HTML5 Forms はAEMサーバーに接続して、サーバー側スクリプト、Web サービス、送信を実行します。 HTML5 forms の XFA ランタイムは、「/bin/xfaforms/submitaction」エンドポイントで Ajax 呼び出しを使用し、AEMサーバーに接続するための様々なパラメーターを指定します。 HTML5 forms はAEMサーバーに接続し、次の操作を実行します。

#### サーバー側スクリプトと Web サービスの実行 {#execute-server-sided-scripts-and-web-services}

サーバー上で実行するようにマークされたスクリプトは、サーバー側スクリプトと呼ばれます。 サーバーサイドスクリプトと web サービスで使用されるすべてのパラメーターを下表に示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>パラメーター</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>アクティビティ</p> </td>
   <td><p>「アクティビティ」には、リクエストをトリガーするイベントが含まれます。 例：クリック、終了、変更</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom には、イベントが実行されるオブジェクトの SOM 式が含まれます。</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>Template は、フォームをレンダリングするために使用するテンプレートを指定します。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot は、フォームのレンダリングに使用するテンプレートルートディレクトリを指定します。</p> </td>
  </tr>
  <tr>
   <td><p>データ</p> </td>
   <td><p>Data は、フォームのレンダリングに使用されるデータバイトを含みます。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom は、JSON 形式のHTML5 の DOM を含みます。</p> </td>
  </tr>
  <tr>
   <td><p>パケット</p> </td>
   <td><p>パケットはフォームとして指定されます。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir は、フォームをレンダリングするために使用するデバッグディレクトリを指定します。</p> </td>
  </tr>
 </tbody>
</table>

#### データを送信 {#submit-data}

送信ボタンをクリックすると、HTML5 forms はデータをサーバーに送信します。 次の表に、Server5 Forms がサーバーに送信するすべてのHTMLを示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>パラメーター</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>フォームのレンダリングに使用するテンプレート。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>フォームのレンダリングに使用するテンプレートルートディレクトリ。</p> </td>
  </tr>
  <tr>
   <td><p>データ</p> </td>
   <td><p>フォームのレンダリングに使用するデータバイト。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>JSON 形式のHTML5 の DOM。</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>データ XML が投稿される URL。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>フォームのレンダリングに使用する debug ディレクトリ。</p> </td>
  </tr>
 </tbody>
</table>

#### 送信プロキシの仕組み {#how-nbsp-the-nbsp-submit-proxy-works}

submiturl がリクエストパラメーターに存在しない場合、送信サービスプロキシはパススルーとして機能します。 これはパススルーとして機能します。 これはリクエストを /bin/xfaforms/submitaction エンドポイントに送信し、応答を XFA ランタイムに送信します。

送信サービスプロキシは、submiturl がリクエストパラメーターに存在する場合に、トポロジを選択します。

* AEMサーバーがデータを投稿する場合、プロキシサービスはパススルーとして機能します。 これはリクエストを /bin/xfaforms/submitaction エンドポイントに送信し、応答を XFA ランタイムに送信します。
* プロキシがデータを送信すると、プロキシサービスは、submitUrl を除くすべてのパラメーターを */bin/xfaforms/submitaction* エンドポイントに渡し、応答ストリームで xml バイトを受け取ります。次に、プロキシサービスはデータ xml バイトを submitUrl に投稿して処理します。

* データ (POSTリクエスト ) をサーバーに送信する前に、HTML5 forms はサーバーの接続と可用性を確認します。 接続性と可用性を検証するために、HTMLフォームは空の head リクエストをサーバーに送信します。 サーバーが使用可能な場合、HTML5 フォームはデータ (POSTリクエスト ) をサーバーに送信します。 サーバーが使用できない場合は、エラーメッセージ「*サーバーに接続できませんでした*」が表示されます。この事前の検出により、ユーザーがフォームに再記入するなどの問題を回避できます。プロキシサーブレットがヘッドリクエストを処理し、例外をスローしません。
