---
title: カスタムポータルにおける通信を作成の UI の統合
description: 通信の作成 UI をカスタムポータルに統合する方法を説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 37%

---

# 通信作成用 UI のカスタムポータルへの統合{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概要 {#overview}

この記事では、通信を作成ソリューションを環境に統合する方法について詳しく説明します。

## URL ベースの呼び出し {#url-based-invocation}

カスタムポータルから通信を作成アプリケーションを呼び出す方法の 1 つは、次の要求パラメーターを使用して URL を準備することです。

* 文字テンプレートの識別子（cmLetterId パラメーターを使用）。

* 目的のデータソースから取得した XML データの URL（cmDataUrl パラメーターを使用）。

例えば、カスタムポータルは、次のような URL を準備します\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`（ポータル上のリンクからの href にすることができます）。

>[!NOTE]
>
>このような呼び出し方法では、必要なパラメーターが URL で同じ（明確に表示される）を公開することで、GETリクエストとして渡されるので、安全ではありません。

>[!NOTE]
>
>通信を作成アプリケーションを呼び出す前に、データを保存してアップロードし、指定された dataURL で通信を作成 UI を呼び出します。 これは、カスタムポータル自体から実行することも、別のバックエンドプロセスを通じて実行することもできます。

## インラインデータベースの呼び出し {#inline-data-based-invocation}

通信作成用アプリケーションを呼び出す別の（そしてより安全な）方法は、https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html の URL をシンプルにヒットしながら、通信作成用アプリケーションを呼び出すパラメーターとデータを POST リクエストとして送信（エンドユーザーからはそれらを隠して）すること、が考えられます。つまり、以前のアプローチでは不可能で、理想的ではなかった、同じリクエストの一環として、通信を作成アプリケーションの XML データをインラインで渡すことができます。

### レターを指定するためのパラメーター {#parameters-for-specifying-letter}

| **名前** | **タイプ** | **説明** |
|---|---|---|
| cmLetterInstanceId | 文字列 | レターインスタンスの ID です。 |
| cmLetterId | 文字列 | レターテンプレートの名前。 |

テーブル内のパラメーターの順序は、レターの読み込みに使用するパラメーターの優先順位を指定します。

### XML データソースを指定するためのパラメーター {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td> 
   <td><strong>種類</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>cq、ftp、http、file などの基本的なプロトコルを使用したソースファイルからの XML データ。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>文字列</td> 
   <td>レターインスタンスで使用可能な xml データを使用します。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>ブール値</td> 
   <td>データディクショナリに添付されたテストデータを再利用する。</td> 
  </tr>
 </tbody>
</table>

テーブル内のパラメーターの順序は、XML データの読み込みに使用するパラメーターのプリファレンスを指定します。

### その他のパラメーター {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td> 
   <td><strong>種類</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>ブール値</td> 
   <td>True に設定すると、レターがプレビューモードで開きます<br /> </td> 
  </tr>
  <tr>
   <td>ランダム</td> 
   <td>Timestamp</td> 
   <td>ブラウザーのキャッシュの問題を解決するには、以下を実行します。</td> 
  </tr>
 </tbody>
</table>

cmDataURL に http または cq プロトコルを使用している場合、http または cq の URL には匿名でアクセスできます。
