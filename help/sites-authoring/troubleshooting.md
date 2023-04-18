---
title: AEMでのオーサリング時のトラブルシューティング
description: AEMの使用時に発生する可能性のある問題をいくつか紹介します。
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 52%

---

# オーサリング時の AEM のトラブルシューティング {#troubleshooting-aem-when-authoring}

ここでは、AEM の使用時に発生する可能性のあるいくつかの問題を取り上げます。また、それらのトラブルシューティング方法に関する推奨事項についても説明します。

>[!NOTE]
>
>問題が発生した場合は、リストを確認することも重要です [既知の問題](/help/release-notes/release-notes.md) インスタンス（リリースおよびサービスパック）の

>[!NOTE]
>
>管理者権限を持ち、AEMの問題をトラブルシューティングするユーザーは、 [トラブルシューティングAEM （管理者向け）](/help/sites-administering/troubleshoot.md). 十分な権限がない場合は、AEMのトラブルシューティングに関して、システム管理者に問い合わせてください。

## 公開されたサイト上に古いバージョンのページがまだある {#old-page-version-still-on-published-site}

* **問題**：

   * ページに変更を加えてそのページを公開サイトにレプリケートしましたが、公開サイトでは古いバージョンのページが依然として表示されます&#x200B;*。*

* **理由**:

   * これには複数の原因が考えられます。ほとんどの場合、キャッシュ（ローカルブラウザーまたは Dispatcher）が原因ですが、レプリケーションキューに問題が発生する場合があります。

* **ソリューション**:

   * ここには、様々な可能性があります。
   * ページが正しくレプリケートされていることを確認します。 ページのステータスと、必要に応じてレプリケーションキューの状態を確認します。
   * ローカルブラウザーのキャッシュをクリアして、ページに再度アクセスします。
   * ページ URL の末尾に `?` を追加します。以下に例を示します。

      * `http://localhost:4502/sites.html/content?`
      *  これによって、ページが AEM から直接リクエストされ、Dispatcher がスキップされます。更新されたページを受け取った場合、Dispatcher のキャッシュをクリアする必要があることを表しています。
   * システム管理者に問い合わせて、レプリケーションキューに問題があることを伝えます。


## コンポーネントのアクションがツールバーに表示されない {#component-actions-not-visible-on-toolbar}

* **問題**：

   * オーサー環境でのコンテンツページの編集中に、使用可能なすべてのコンポーネントのアクションが表示されません。

* **理由**:

   * まれに、前のアクションがツールバーに影響を与える場合があります。

* **解決策**:

   * ページを更新します。
