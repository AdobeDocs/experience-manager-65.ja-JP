---
title: AEM Sites - GDPR 対応
seo-title: AEM Sites - GDPR 対応
description: AEM Sites の GDPR 対応について詳しく説明します。
seo-description: AEM Sites の GDPR 対応について詳しく説明します。
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 91%

---


# AEM Sites - GDPR 対応{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>以下の節ではGDPRを例に挙げていますが、詳細はデータ保護とプライバシーに関するすべての規制に適用されます。GDPR、CCPAなど

データのプライバシー権に関する EU 一般データ保護規則（GDPR）が 2018 年 5 月に発効します。

AEM Sites は、GDPR コンプライアンスの義務に関してお客様を支援する準備ができています。このページでは、AEM Sites での GDPR 要求の処理手順について詳しく説明します。プライベートデータの格納場所や、それらのデータを手動で、またはコードを使用して削除する方法について説明します。

詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html)を参照してください。

>[!NOTE]
>
>詳しくは、[AEM の GDPR 対応](/help/managing/data-protection-and-privacy.md)を参照してください。

## オーサーサーバー {#author-server}

オーサーサーバー上のユーザーアカウントと UGC コンテンツについては、[プラットフォームの GDPR ドキュメント](/help/managing/data-protection-and-privacy.md)を参照してください。

## パブリッシュサーバー {#publish-server}

サイト上で訪問者の認証に使用されるユーザーアカウント、およびパブリッシュサーバー上の UGC コンテンツについては、[プラットフォームの GDPR ドキュメント](/help/managing/data-protection-and-privacy.md)を参照してください。

AEM Sites コンポーネントはデフォルトでは、訪問者によって入力されたフォームデータを  パブリッシュサーバー。 サードパーティのシステムまたは Adobe Campaign にデータを転送してさらに処理をおこなうことをお勧めします。

## オプトイン／オプトアウト {#opt-in-opt-out}

AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md) that can be used for managing the opt-in/opt-out for users.

## Analytics によるインサイトの拡張 {#enhanced-insights-by-analytics}

AEM Sitesには、Adobe Analytics On-demand サービス内の機能を使用した、Analytics によるインサイトの拡張との統合（オプション）が含まれています。

Adobe Analytics に関連する GDPR データサブジェクトリクエストの管理についての詳細は、[Adobe Analytics と GDPR](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html) を参照してください。

## Target によるパーソナライゼーションの拡張 {#enhanced-personalization-by-target}

AEM Sitesには、Adobe Target On-demand サービス内の機能を使用した、Target によるパーソナライゼーションの拡張との統合（オプション）が含まれています。

Adobe Target に関連する GDPR データサブジェクトリクエストの管理についての詳細は、[Adobe Target - プライバシーと一般データ保護規則](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)を参照してください。

## ContextHub {#contexthub}

AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md). ContextHub を使用する場合、訪問者固有のデータがブラウザー内に格納され、そのデータに基づいてルールベースのパーソナライゼーションが実行されます。

この訪問者データはデフォルトでは AEM に格納されません。ブラウザー内でパーソナライゼーションに関する決定をおこなうためのルールが、AEM からデータレイヤーに送信されます。

>[!NOTE]
>
>Adobe CQ 5.6 より前は、ClientContext（ContextHub の旧バージョン）からサーバーにデータが送信されていましたが、そのデータはサーバーに格納されませんでした。
>
>Adobe CQ 5.5 以前はサポートが終了している（EOL）ので、このドキュメントでは説明しません。

### オプトイン／オプトアウトの実装 {#implementing-opt-in-opt-out}

サイトの所有者は、オプトアウトコンポーネントを実装する際、以下のガイドラインに従う必要があります。

これらのガイドラインでは、デフォルトでオプトインが実装されます。そのため、Web サイトの訪問者は、個人データがブラウザーの（クライアント側）永続ストレージに格納される前に、明確に同意する必要があります。

* オプトアウトコンポーネントは、ContextHub コンポーネントを組み込むたびに必ず組み込んでください。
* Web サイトの GDPR に関連する利用条件を Web サイトの訪問者に表示して、訪問者が以下をおこなえるようにする必要があります。

   * 同意
   * 拒否
   * 以前の選択の変更

* サイト訪問者がサイトの利用条件に同意する場合は、次のようにして、ContextHub のオプトアウト Cookie を削除する必要があります。

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* サイト訪問者がサイトの利用条件に同意しない場合は、次のようにして、ContextHub のオプトアウト Cookie を設定する必要があります。

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* ContextHub がオプトアウトモードで動作しているかどうかを確認するには、ブラウザーのコンソールで次の呼び出しをおこなう必要があります。

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### ContextHub の永続性のプレビュー {#previewing-persistence-of-contexthub}

ContextHub で使用されている永続性をプレビューするには、次の方法があります。

* ブラウザーのコンソールを使用する。以下に例を示します。

   * Chrome の場合：

      * デベロッパー ツール／Application／Storage を選択

         * Local Storage／（Web サイト）／ContextHubPersistence
         * Session Storage／（Web サイト）／ContextHubPersistence
         * Cookies／（Web サイト）／SessionPersistence
   * Firefox の場合：

      * 開発ツールを表示／ストレージを選択

         * ローカルストレージ／（Web サイト）／ContextHubPersistence
         * Session Storage／（Web サイト）／ContextHubPersistence
         * Cookie／（Web サイト）／SessionPersistence
   * Safari の場合：

      * 環境設定／詳細／メニューバーに“開発”メニューを表示を選択
      * 開発／JavaScriptコンソールを表示を選択

         * コンソール／ストレージ／ローカルストレージ／（Web サイト）／ContextHubPersistence
         * コンソール／ストレージ／セッションストレージ／（Web サイト）／ContextHubPersistence
         * コンソール／ストレージ／Cookie／（Web サイト）／ContextHubPersistence
   * Internet Explorer:

      * F12 開発者ツール／コンソールを選択

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* ブラウザーのコンソールで ContextHub API を使用する。

   * ContextHub には次のデータ永続性レイヤーが用意されています。

      * ContextHub.Utils.Persistence.Modes.LOCAL（デフォルト）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      どの永続性レイヤーが使用されるかは ContextHub ストアに定義されているので、永続性の現在の状態を確認するには、すべてのレイヤーをチェックする必要があります。


例えば、ローカルストレージに格納されているデータを表示するには、次のようにします。

ContextHub で使用されている永続性をプレビューするには、次の方法があります。

* ブラウザーのコンソールを使用する。以下に例を示します。

   * Chrome の場合：デベロッパー ツール／Application／Storage を選択

      * Local Storage／（Web サイト）／ContextHubPersistence
      * Session Storage／（Web サイト）／ContextHubPersistence
      * Cookies／（Web サイト）／SessionPersistence
   * Firefox の場合：開発ツールを表示／ストレージを選択

      * ローカルストレージ／（Web サイト）／ContextHubPersistence
      * Session Storage／（Web サイト）／ContextHubPersistence
      * Cookie／（Web サイト）／SessionPersistence


* ブラウザーのコンソールで ContextHub API を使用する。

   * ContextHub には次のデータ永続性レイヤーが用意されています。

      * ContextHub.Utils.Persistence.Modes.LOCAL（デフォルト）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      どの永続性レイヤーが使用されるかは ContextHub ストアに定義されているので、永続性の現在の状態を確認するには、すべてのレイヤーをチェックする必要があります。


例えば、ローカルストレージに格納されているデータを表示するには、次のようにします。

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### ContextHub の永続性の解除 {#clearing-persistence-of-contexthub}

ContextHub の永続性を解除するには：

* 現在読み込まれているストアの永続性を解除するには、以下を実行します。

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 特定の永続性レイヤー（例：セッションストレージ）を解除するには、以下を実行します。

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* ContextHub のすべての永続性レイヤーを解除するには、以下のすべてのレイヤーに対して適切なコードを呼び出す必要があります。

   * ContextHub.Utils.Persistence.Modes.LOCAL（デフォルト）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW

