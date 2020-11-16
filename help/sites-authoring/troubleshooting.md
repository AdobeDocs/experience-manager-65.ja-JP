---
title: オーサリング時の AEM のトラブルシューティング
seo-title: オーサリング時の AEM のトラブルシューティング
description: AEM を使用する際に発生する可能性のあるいくつかの問題です
seo-description: AEM を使用する際に発生する可能性のあるいくつかの問題です
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 100%

---


# オーサリング時の AEM のトラブルシューティング{#troubleshooting-aem-when-authoring}

ここでは、AEM の使用時に発生する可能性のあるいくつかの問題を取り上げます。また、それらのトラブルシューティング方法に関する推奨事項についても説明します。

>[!NOTE]
>
>問題が発生した場合は、そのインスタンス（リリースおよびサービスパック）の[既知の問題](/help/release-notes/known-issues.md)のリストを確認すると役に立ちます。

>[!NOTE]
>
>管理者権限を持つユーザー、および AEM を使用して問題のトラブルシューティングをおこなうユーザーは、[AEM のトラブルシューティング（管理者向け）](/help/sites-administering/troubleshoot.md)に説明のあるトラブルシューティング方法を使用できます。十分な権限を持っていない場合は、AEM のトラブルシューティングに関してシステム管理者にお問い合わせください。

## 公開されたサイト上に古いバージョンのページがまだある {#old-page-version-still-on-published-site}

* **問題**：

   * ページに変更を加えてそのページを公開サイトにレプリケートしましたが、公開サイトでは古い&#x200B;**&#x200B;バージョンのページが依然として表示されます。

* **理由**:

   * いくつかの原因が考えられます。キャッシュ（ローカルブラウザーまたは Dispatcher のキャッシュ）が原因である場合がほとんどですが、レプリケーションキューに問題があることもあります。

* **ソリューション**:

   * これには、様々な原因が考えられます。
   * ページが正しくレプリケートされていることを確認します。ページのステータスや、必要に応じてレプリケーションキューの状態をチェックします。
   * ローカルブラウザーのキャッシュをクリアして、ページに再度アクセスします。
   * ページ URL の末尾に `?` を追加します。以下に例を示します。

      * `http://localhost:4502/sites.html/content?`
      *  これによって、ページが AEM から直接リクエストされ、Dispatcher がスキップされます。更新されたページを受け取った場合、Dispatcher のキャッシュをクリアする必要があることを表しています。
   * システム管理者に問い合わせて、レプリケーションキューに問題があることを伝えます。


## コンポーネントのアクションがツールバーに表示されない {#component-actions-not-visible-on-toolbar}

* **問題**：

   * オーサー環境でのコンテンツページの編集中に、使用可能なすべてのコンポーネントのアクションが表示されません。

* **理由**:

   * まれに、前のアクションがツールバーに影響を及ぼすことがあります。

* **解決策**:

   * ページを更新します。

