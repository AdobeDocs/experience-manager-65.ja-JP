---
title: 'オーサリング時の AEM のトラブルシューティング '
seo-title: Troubleshooting AEM when Authoring
description: 以下のセクションでは、AEM の使用時に発生する可能性のあるいくつかの問題を取り上げます。それらのトラブルシューティング方法に関する推奨事項についても説明します。
seo-description: The following section covers some issues that you might encounter when using AEM, together with suggestions on how to troubleshoot them.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: ht
source-wordcount: '430'
ht-degree: 100%

---

# オーサリング時の AEM のトラブルシューティング {#troubleshooting-aem-when-authoring}

ここでは、AEM の使用時に発生する可能性のあるいくつかの問題を取り上げます。また、それらのトラブルシューティング方法に関する推奨事項についても説明します。

>[!NOTE]
>
>問題が発生した場合は、そのインスタンス（リリースおよびサービスパック）の[既知の問題](/help/release-notes/release-notes.md)のリストを確認すると役に立ちます。

>[!NOTE]
>
>管理者権限を持つユーザー、および AEM を使用して問題のトラブルシューティングをおこなうユーザーは、[AEM のトラブルシューティング（管理者向け）](/help/sites-administering/troubleshoot.md)に説明のあるトラブルシューティング方法を使用できます。十分な権限を持っていない場合は、AEM のトラブルシューティングに関してシステム管理者にお問い合わせください。

## 公開されたサイト上に古いバージョンのページがまだある {#old-page-version-still-on-published-site}

* **問題**：

   * ページに変更を加えてそのページを公開サイトにレプリケートしましたが、公開サイトでは古いバージョンのページが依然として表示されます&#x200B;*。*

* **理由**:

   * いくつかの原因が考えられます。キャッシュ（ローカルブラウザーまたは Dispatcher のキャッシュ）が原因である場合がほとんどですが、レプリケーションキューに問題があることもあります。

* **ソリューション**:

   * これには、様々な原因が考えられます。
   * ページが正しくレプリケートされていることを確認します。ページのステータスや、必要に応じてレプリケーションキューの状態をチェックします。
   * ローカルブラウザーのキャッシュをクリアして、ページに再度アクセスします。
   * ページ URL の末尾に `?` を追加します。以下に例を示します。

      `http://localhost:4502/sites.html/content?`

       これによって、ページが AEM から直接リクエストされ、Dispatcher がスキップされます。更新されたページを受け取った場合、Dispatcher のキャッシュをクリアする必要があることを表しています。

   * システム管理者に問い合わせて、レプリケーションキューに問題があることを伝えます。

## サイドキックが表示されない {#sidekick-not-visible}

* **問題**：

   * オーサー環境でのコンテンツページの編集中にサイドキックが表示されません。

* **理由**:

   * まれに、サイドキックのヘッダーが現在のウィンドウの範囲外になるように置かれてしまうことがあります。この場合、サイドキックの位置を再び変更することができなくなります。

* **ソリューション**：

   * 現在のセッションからログアウトして、ログインし直してください。サイドキックがデフォルトの位置に戻ります。

## 検索と置換 - すべてのインスタンスが置換されない {#find-replace-not-all-instances-are-replaced}

* **問題:**

   * 「**検索と置換**」オプションを使用するとき、`find` 検索語句の一部のインスタンスがページ上で置換されないことがあります。

* **理由**:

   * **検索と置換**&#x200B;の機能は、コンテンツの保存のされ方と、コンテンツを検索できるかどうかに依存しています。例えば、ブログテキストは `jcr:text` プロパティに格納されますが、このプロパティは検索対象として設定されません。検索と置換のサーブレットのデフォルトスコープには、次のプロパティが含まれています。

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **ソリューション**：

   * これらの定義は、例えば次の場所にある **web コンソール**&#x200B;を使用して、**Day CQ WCM 検索置換サーブレット** を設定することで変更できます。

      `http://localhost:4502/system/console/configMgr`
