---
title: カスタムポータルにおける通信を作成の UI の統合
seo-title: Integrating Create Correspondence UI with your custom portal
description: 通信の作成 UI とカスタムポータルを統合する方法について説明します。
seo-description: Learn how to integrate create correspondence UI with your custom portal
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '413'
ht-degree: 100%

---

# 通信作成用 UI のカスタムポータルへの統合{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概要 {#overview}

ここでは、通信を作成のソリューションをお使いの環境に統合する方法の詳細を説明します。

## URL ベースの呼び出し {#url-based-invocation}

通信を作成アプリケーションをカスタムポータルから呼び出す 1 つの方法として、次の要求パラメーターを持つ URL を準備する方法が挙げられます。

* 文字テンプレートの識別子（cmLetterId パラメーターを使用）。

* 目的のデータソースから取得した XML データの URL（cmDataUrl パラメーターを使用）。

例えば、カスタムポータルは、次のような URL を準備します\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`（ポータル上のリンクからの href にすることができます）。

>[!NOTE]
>
>この呼び出し方法は安全ではありません。必要なパラメーターが URL に明示される GET 要求として渡されるからです。

>[!NOTE]
>
>通信を作成アプリケーションを呼び出す前に、データを保存、アップロードして、指定された dataURL で通信を作成の UI を呼び出します。この処理は、カスタムポータル自体で実行されるか、または異なるバックエンドプロセスで実行される可能性があります。

## インラインデータベースの呼び出し {#inline-data-based-invocation}

通信作成用アプリケーションを呼び出す別の（そしてより安全な）方法は、https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html の URL をシンプルにヒットしながら、通信作成用アプリケーションを呼び出すパラメーターとデータを POST リクエストとして送信（エンドユーザーからはそれらを隠して）すること、が考えられます。つまり、通信を作成アプリケーションの XML データを（cmData パラメーターを使用して、同じ要求の一部として）インラインで渡すことができることも意味します。これは、前述のアプローチでは、不可能で、理想的ではありませんでした。

### レターを指定するパラメーター {#parameters-for-specifying-letter}

| **名前** | **タイプ** | **説明** |
|---|---|---|
| cmLetterInstanceId | 文字列 | レターインスタンスの ID です。 |
| cmLetterId | 文字列 | レターテンプレートの名前です。 |

テーブル中のパラメーターの順序が、レターの読み込みに使用されるパラメーターの優先順位を指定します。

### XML データソースを指定するパラメーター {#parameters-for-specifying-the-xml-data-source}

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
   <td>cq、ftp、http、file などの基本的なプロトコルを使用してソースファイルから取得する XML データです。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>文字列</td> 
   <td>レターインスタンスで使用可能な xml データを使用します。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>ブール値</td> 
   <td>データディクショナリに添付されたテストデータを再利用します。</td> 
  </tr>
 </tbody>
</table>

テーブル中のパラメーターの順序が、XML データの読み込みに使用されるパラメーターの優先順位を指定します。

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
   <td>「True」に設定されている場合、レターをプレビューモードで開きます<br /> </td> 
  </tr>
  <tr>
   <td>ランダム</td> 
   <td>Timestamp</td> 
   <td>ブラウザーのキャッシュに関する問題を解決します。</td> 
  </tr>
 </tbody>
</table>

cmDataURL に http または cq プロトコルを使用している場合、http または cq の URL には匿名でアクセスできます。
