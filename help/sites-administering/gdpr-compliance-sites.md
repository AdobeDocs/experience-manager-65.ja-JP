---
title: AEM Sites - GDPR 対応
description: AEM Sites で GDPR リクエストを処理する手順とその使用方法について説明します。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Architect, Developer, Leader, User, Data Architect, Data Engineer
source-git-commit: 5c1eda486e31be01f614a3a7ada71563fd996656
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 93%

---

# AEM Sites - GDPR 対応{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制（GDPR、CCPA など）に適用できます。

データのプライバシー権に関する EU 一般データ保護規則（GDPR）が 2018 年 5 月に発効します。

AEM Sites は、GDPR コンプライアンスに関する義務をお客様が果たすのを支援する準備が整っています。このページでは、AEM Sites での GDPR 要求の処理手順について詳しく説明します。プライベートデータの格納場所や、それらのデータを手動で、またはコードを使用して削除する方法について説明します。

詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html)を参照してください。

>[!NOTE]
>
>詳しくは、[AEM の GDPR 対応](/help/managing/data-protection-and-privacy.md)を参照してください。

## オーサーサーバー {#author-server}

オーサーサーバー上のユーザーアカウントと UGC コンテンツについては、[プラットフォームの GDPR ドキュメント](/help/managing/data-protection-and-privacy.md)を参照してください。

## パブリッシュサーバー {#publish-server}

サイト上で訪問者の認証に使用されるユーザーアカウント、およびパブリッシュサーバー上の UGC コンテンツについては、[プラットフォームの GDPR ドキュメント](/help/managing/data-protection-and-privacy.md)を参照してください。

デフォルトの AEM Sites コンポーネントは、訪問者から入力されたフォームデータをパブリッシュサーバーに保存しません。サードパーティのシステムまたは Adobe Campaign にデータを転送してさらに処理を行うことをお勧めします。

## オプトイン／オプトアウト {#opt-in-opt-out}

AEM に含まれる [cookie オプトアウトサービス](/help/sites-developing/cookie-optout.md)を使用すれば、ユーザーのオプトイン／オプトアウトを管理できます。

## Analytics によるインサイトの拡張 {#enhanced-insights-by-analytics}

AEM Sites には、Adobe Analytics On-demand サービス内の機能を使用した、Analytics によるインサイトの拡張との統合（オプション）が含まれています。

Adobe Analytics に関連する GDPR データサブジェクトリクエストの管理について詳しくは、[Adobe Analytics と GDPR](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=ja) を参照してください。

## Target によるパーソナライゼーションの拡張 {#enhanced-personalization-by-target}

AEM Sitesには、Adobe Target On-demand サービス内の機能を使用した、Target によるパーソナライゼーションの拡張との統合（オプション）が含まれています。

Adobe Target に関連する GDPR データサブジェクトリクエストの管理について詳しくは、[Adobe Target - プライバシーと一般データ保護規則](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=ja)を参照してください。

## ContextHub {#contexthub}

AEM には、[ContextHub](/help/sites-developing/contexthub.md) を使用するオプションのデータレイヤーが用意されています。これにより、ブラウザーに訪問者固有のデータが保持され、そのデータに基づいてルールベースのパーソナライズ機能が実行されます。

この訪問者データはデフォルトでは AEM に格納されません。ブラウザー内でパーソナライゼーションに関する決定を行うためのルールが、AEM からデータレイヤーに送信されます。

>[!NOTE]
>
>AEM（CQ） 5.6 より前のAdobeでは、ClientContext（以前のバージョンの ContextHub）はデータをサーバーに送信していましたが、保存はしませんでした。
>
>Adobe AEM 6.4 以前のバージョンはサポート終了となり、このドキュメントでは扱いません。 [Adobe Experience Manager、CQ およびCRXの以前のバージョンのドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions) を参照してください。

### オプトイン／オプトアウトの実装 {#implementing-opt-in-opt-out}

サイト所有者は、次のガイドラインに従ってオプトアウトコンポーネントを実装する必要があります。

以下のガイドラインでは、デフォルトでオプトインが実装されています。そのため、web サイトの訪問者は、個人データがブラウザーの（クライアント側）永続ストレージに格納される前に、明確に同意する必要があります。

* オプトアウトコンポーネントは、ContextHub コンポーネントを組み込むたびに必ず組み込んでください。
* Web サイトの GDPR に関連する利用条件を web サイトの訪問者に表示して、訪問者が以下を行えるようにする必要があります。

   * 同意
   * 拒否
   * 以前の選択の変更

* サイト訪問者がサイトの利用条件に同意した場合は、ContextHub のオプトアウト cookie を削除する必要があります。

  ```java
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  ```

* サイト訪問者がサイトの利用条件に同意しない場合は、ContextHub オプトアウト cookie を次のように設定する必要があります。

  ```java
  ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
  ```

* ContextHub がオプトアウトモードで動作しているかどうかを確認するには、ブラウザーのコンソールで次の呼び出しを行う必要があります。

  ```java
  var isOptedOut = ContextHub.isOptedOut(true) === true;
  // if isOptedOut is true, ContextHub is running in opt-out mode
  ```

### ContextHub の永続性のプレビュー {#previewing-persistence-of-contexthub}

ContextHub を使用した永続性をプレビューするには、次の操作を行うことができます。

* ブラウザーのコンソールを使用する。例：

   * Chrome:

      * 開発者ツール／アプリケーション／ストレージを選択

         * ローカルストレージ／（Web サイト）／ContextHubPersistence
         * セッションストレージ／（web サイト）／ContextHubPersistence
         * Cookie／（Web サイト）／SessionPersistence

   * Firefox:

      * 開発者ツール／ストレージを選択

         * ローカルストレージ／（Web サイト）／ContextHubPersistence
         * セッションストレージ／（web サイト）／ContextHubPersistence
         * Cookie／（Web サイト）／SessionPersistence

   * Safari:

      * メニューバーで、環境設定／詳細／開発者メニューを表示を選択
      * 開発／JavaScript コンソールを表示を選択

         * コンソール／ストレージ／ローカルストレージ／（web サイト）／ContextHubPersistence
         * コンソール／ストレージ／セッションストレージ／（web サイト）／ContextHubPersistence
         * コンソール／ストレージ／Cookie／（web サイト）／ContextHubPersistence

   * Internet Explorer:

      * F12 開発者ツール／コンソールを選択

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie

* ブラウザーのコンソールで ContextHub API を使用する。

   * ContextHub には、次のデータ永続性レイヤーが用意されています。

      * ContextHub.Utils.Persistence.Modes.LOCAL（デフォルト）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     ContextHub ストアは、使用する永続性レイヤーを定義します。永続性の現在の状態を表示するには、すべてのレイヤーを確認する必要があります。

例えば、localStorage に格納されているデータを表示するには、次のようにします。

ContextHub を使用した永続性をプレビューするには、次の操作を行うことができます。

* ブラウザーのコンソールを使用する。

   * Chrome - 開発者ツール／アプリケーション／ストレージを選択

      * ローカルストレージ／（Web サイト）／ContextHubPersistence
      * セッションストレージ／（web サイト）／ContextHubPersistence
      * Cookie／（Web サイト）／SessionPersistence

   * Firefox - 開発者ツール／ストレージを選択

      * ローカルストレージ／（Web サイト）／ContextHubPersistence
      * セッションストレージ／（web サイト）／ContextHubPersistence
      * Cookie／（Web サイト）／SessionPersistence

* ブラウザーのコンソールで ContextHub API を使用する。

   * ContextHub には、次のデータ永続性レイヤーが用意されています。

      * ContextHub.Utils.Persistence.Modes.LOCAL（デフォルト）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     ContextHub ストアは、使用する永続性レイヤーを定義します。永続性の現在の状態を表示するには、すべてのレイヤーを確認する必要があります。

例えば、localStorage に格納されているデータを表示するには、次のようにします。

```java
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### ContextHub の永続性の削除 {#clearing-persistence-of-contexthub}

ContextHub の永続性を削除するには、以下を実行します。

* 現在読み込まれているストアの永続性を削除するには、以下を実行します。

  ```java
  // to be able to fully access persistence layer, Opt-Out must be turned off
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  
  // following call asks all currently loaded stores to clear their data
  ContextHub.cleanAllStores();
  
  // following call asks all currently loaded stores to set back default values (provided in their configs)
  ContextHub.resetAllStores();
  ```

* 特定の永続性レイヤーを削除するには、例えば、sessionStorage は次のようになります。

  ```java
  var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
  storage.setItem('/store', null);
  storage.setItem('/_', null);
  
  // to confirm that nothing is stored:
  console.log(storage.getTree());
  ```

* すべての ContextHub 永続性レイヤーを削除するには、すべてのレイヤーに対して適切なコードを呼び出す必要があります。

   * ContextHub.Utils.Persistence.Modes.LOCAL（デフォルト）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
