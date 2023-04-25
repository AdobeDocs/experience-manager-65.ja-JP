---
title: AEM Sites - GDPR 対応
seo-title: AEM Sites - GDPR Readiness
description: AEM Sitesの GDPR 対応の詳細について説明します。
seo-description: Learn about the details of GDPR Readiness for AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 28%

---

# AEM Sites - GDPR 対応{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制（GDPR、CCPA など）に適用できます。

データのプライバシー権に関する EU 一般データ保護規則（GDPR）が 2018 年 5 月に発効します。

AEM Sitesは、お客様が GDPR に準拠するための義務を果たすのを支援する準備が整っています。 このページでは、AEM Sitesで GDPR 要求を処理する手順を説明します。 プライベートデータの格納場所や、それらのデータを手動で、またはコードを使用して削除する方法について説明します。

詳しくは、 [GDPR ページ (Adobeプライバシーセンター )](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>詳しくは、 [AEM GDPR 対応](/help/managing/data-protection-and-privacy.md) 詳しくは、を参照してください。

## オーサーサーバー {#author-server}

オーサーサーバー上のユーザーアカウントと UGC コンテンツについては、 [Platform GDPR ドキュメント](/help/managing/data-protection-and-privacy.md).

## 公開サーバ {#publish-server}

サイトで訪問者を認証するために使用されるユーザーアカウントと、パブリッシュサーバー上の UGC コンテンツは、 [Platform GDPR ドキュメント](/help/managing/data-protection-and-privacy.md).

AEM Sites コンポーネントはデフォルトでは、訪問者から入力されたフォームデータをパブリッシュサーバーに保存しません。サードパーティのシステムまたは Adobe Campaign にデータを転送してさらに処理を行うことをお勧めします。

## オプトイン／オプトアウト {#opt-in-opt-out}

AEM に含まれる [cookie オプトアウトサービス](/help/sites-developing/cookie-optout.md)を使用すれば、ユーザーのオプトイン／オプトアウトを管理できます。

## Analytics によるインサイトの強化 {#enhanced-insights-by-analytics}

AEM Sitesには、Adobe Analytics On-demand Service 内の機能を使用する、Enhanced Insights by Analytics とのオプションの統合が含まれています。

Adobe Analyticsに関連する GDPR データ主体リクエストの管理について詳しくは、 [Adobe Analyticsと GDPR](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=ja).

## Target によるパーソナライゼーションの強化 {#enhanced-personalization-by-target}

AEM Sitesには、Adobe Target On-demand Service 内の機能を使用する、Target による拡張パーソナライゼーションとのオプションの統合が含まれています。

Adobe Targetに関連する GDPR データ主体リクエストの管理について詳しくは、 [Adobe Target — プライバシーと一般データ保護規則](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en).

## ContextHub {#contexthub}

AEM には、[ContextHub](/help/sites-developing/contexthub.md) を使用するオプションのデータレイヤーが用意されています。これにより、ブラウザーに訪問者固有のデータを保持し、ルールベースのパーソナライゼーションに使用できます。

この訪問者データはデフォルトでは AEM に格納されません。ブラウザー内でパーソナライゼーションに関する決定を行うためのルールが、AEM からデータレイヤーに送信されます。

>[!NOTE]
>
>Adobe CQ 5.6 以前は、ClientContext（ContextHub の以前のバージョン）はデータをサーバーに送信しましたが、保存していませんでした。
>
>Adobe CQ 5.5 以前は現在 EOL で、このドキュメントでは扱われていません。

### オプトイン／オプトアウトの実装 {#implementing-opt-in-opt-out}

サイトの所有者は、次のガイドラインに従ってオプトアウトコンポーネントを実装する必要があります。

以下のガイドラインでは、オプトインがデフォルトとして実装されています。 したがって、個人データがブラウザーの（クライアント側の）永続性に保存される前に、Web サイトの訪問者は明確に同意する必要があります。

* オプトアウトコンポーネントは、ContextHub コンポーネントを組み込むたびに必ず組み込んでください。
* Web サイトの GDPR に関連する利用条件を Web サイトの訪問者に表示し、次の操作を許可する必要があります。

   * 同意
   * reject
   * 以前の選択を変更する

* サイトの訪問者がサイトの利用条件に同意した場合は、ContextHub のオプトアウト Cookie を削除する必要があります。

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* サイトの訪問者がサイトの利用条件に同意しない場合は、ContextHub オプトアウト Cookie を次のように設定する必要があります。

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* ContextHub がオプトアウトモードで動作しているかどうかを確認するには、ブラウザーのコンソールで次の呼び出しを行う必要があります。

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### ContextHub の永続性のプレビュー {#previewing-persistence-of-contexthub}

ContextHub で使用される永続性をプレビューするには、次の操作をおこないます。

* ブラウザーのコンソールを使用します。例：

   * Chrome:

      * 開発者ツール/アプリケーション/ストレージを開きます。

         * ローカルストレージ／（Web サイト）／ContextHubPersistence
         * セッションストレージ/（Web サイト）/ContextHubPersistence
         * Cookie／（Web サイト）／SessionPersistence
   * Firefox:

      * 開発者ツール/ストレージを開きます。

         * ローカルストレージ／（Web サイト）／ContextHubPersistence
         * セッションストレージ/（Web サイト）/ContextHubPersistence
         * Cookie／（Web サイト）／SessionPersistence
   * Safari:

      * メニューバーで、環境設定/詳細設定/開発メニューを表示を開きます。
      * 開発/ JavaScript コンソールを表示を開きます。

         * コンソール/ストレージ/ローカルストレージ/（Web サイト）/ContextHubPersistence
         * コンソール/ストレージ/セッションストレージ/ （Web サイト）/ ContextHubPersistence
         * コンソール/ストレージ/ Cookies / （Web サイト）/ ContextHubPersistence
   * Internet Explorer:

      * F12 開発者ツール／コンソールを選択

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* ブラウザーのコンソールで ContextHub API を使用します。

   * ContextHub には、次のデータ永続性レイヤーが用意されています。

      * ContextHub.Utils.Persistence.Modes.LOCAL（デフォルト）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub ストアは、使用する永続性レイヤーを定義します。これにより、永続性の現在の状態を表示するために、すべてのレイヤーを確認する必要があります。


例えば、localStorage に格納されたデータを表示するには、次のようにします。

ContextHub で使用される永続性をプレビューするには、次の操作をおこないます。

* ブラウザーのコンソールを使用します。

   * Chrome — デベロッパーツール/アプリケーション/ストレージを開きます。

      * ローカルストレージ／（Web サイト）／ContextHubPersistence
      * セッションストレージ/（Web サイト）/ContextHubPersistence
      * Cookie／（Web サイト）／SessionPersistence
   * Firefox — デベロッパーツール/ストレージを開きます。

      * ローカルストレージ／（Web サイト）／ContextHubPersistence
      * セッションストレージ/（Web サイト）/ContextHubPersistence
      * Cookie／（Web サイト）／SessionPersistence


* ブラウザーのコンソールで ContextHub API を使用します。

   * ContextHub には、次のデータ永続性レイヤーが用意されています。

      * ContextHub.Utils.Persistence.Modes.LOCAL（デフォルト）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub ストアは、使用する永続性レイヤーを定義します。これにより、永続性の現在の状態を表示するために、すべてのレイヤーを確認する必要があります。


例えば、localStorage に格納されたデータを表示するには、次のようにします。

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### ContextHub の永続性のクリア {#clearing-persistence-of-contexthub}

ContextHub の永続性をクリアするには：

* 現在読み込まれているストアの永続性をクリアするには：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 特定の永続性レイヤーをクリアするには：例えば、sessionStorage は次のようになります。

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* すべての ContextHub 永続性レイヤーをクリアするには、すべてのレイヤーに対して適切なコードを呼び出す必要があります。

   * ContextHub.Utils.Persistence.Modes.LOCAL（デフォルト）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
