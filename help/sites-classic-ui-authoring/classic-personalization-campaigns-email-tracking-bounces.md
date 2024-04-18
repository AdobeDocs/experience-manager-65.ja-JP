---
title: バウンス（配信不能）メールの追跡
description: 多数のユーザーにニュースレターを送信する場合、一般的に、リスト内に無効なメールアドレスが一部含まれています。それらのアドレスにニュースレターを送信すると、配信不能として戻ってきます。AEM にはそうしたバウンスを管理する機能があり、バウンスカウンターの設定値を超えると、それらのアドレスへのニュースレターの送信を停止できます。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 100%

---

# バウンス（配信不能）メールの追跡 {#tracking-bounced-emails}

>[!NOTE]
>
>アドビは、AEM SMTP サービスによって送信される開封済みまたはバウンス済みのメールの追跡をさらに強化する予定はありません。
>
>レコメンデーションは、[Adobe Campaign および AEM の統合を使用](/help/sites-administering/campaign.md)することです。

多数のユーザーにニュースレターを送信する場合、一般的に、リスト内に無効なメールアドレスが一部含まれています。それらのアドレスにニュースレターを送信すると、配信不能として戻ってきます。AEM にはそうしたバウンスを管理する機能があり、バウンスカウンターの設定値を超えると、それらのアドレスへのニュースレターの送信を停止できます。デフォルトではバウンス率は 3 になっていますが、設定可能です。

AEM でバウンスメールを追跡するには、バウンスメールが受信される既存のメールボックスをポーリングするように AEM をセットアップします。通常、この場所は、ニュースレターを送信をする際に指定する「送信元」のメールアドレスです。AEM はこのインボックスをポーリングし、ポーリング設定で指定されたパスの下のすべてのメールを読み込みます。次に、ワークフローがトリガーされ、各ユーザー内のバウンスメールアドレスが検索され、それに応じて、ユーザーの bounceCounter プロパティの値が更新されます。設定された最大バウンス数を超えると、そのユーザーはニュースレターリストから削除されます。

## フィードインポーターの設定 {#configuring-the-feed-importer}

フィードインポーターを使用すると、外部ソースからリポジトリにコンテンツを繰り返し読み込むことができます。フィードインポーターのこの設定を使用して、AEM は送信者のメールボックスでバウンスメールを確認します。

バウンスメールを追跡するためにフィードインポーターを設定するには、次の手順を実行します。

1. 「**ツール**」で、「フィードインポーター」を選択します。

1. 「**追加**」をクリックして、設定を作成します。

   ![chlimage_1](assets/chlimage_1a.png)

1. タイプを選択し、ポーリング URL に情報を追加して、ホストとポートを設定することで、設定を追加します。また、URL クエリに対する、メールおよびプロトコル固有のパラメーターをいくつか追加します。最低 1 日に 1 回はポーリングを行うように設定します

   すべての設定で、ポーリング URL 内に次の情報が必要です。

   `username`：接続に使用するユーザー名

   `password`：接続に使用するパスワード

   また、プロトコルによっては、特定の設定を指定することができます。

   **POP3 設定プロパティ：**

   `pop3.leave.on.server`：サーバー上にメッセージを残すかどうかを定義します。サーバーにメッセージを残す場合は true に、そうでない場合は false に設定します。デフォルトは true です。

   **POP3 の例：**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | SSL 経由の POP3 を使用して、ポート 995 で Gmail に接続（user と secret を使用）すると、デフォルトでサーバー上にメッセージが残されます。 |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP 構成プロパティ：**

   検索するフラグを設定できます。

   `imap.flag.SEEN`：新規または未読のメッセージには false を、既読のメッセージには true を設定します。

   フラグの完全リストについて詳しくは、[https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) を参照してください。

   **IMAP の例：**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | SSL 経由の IMAP を使用して、ポート 993 で Gmail に接続（user と secret を使用）します。デフォルトで、新規のメッセージのみが取得されます。 |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | SSL 経由の IMAP を使用して、ポート 993 で Gmail に接続（user と secret を使用）すると、既読のメッセージのみが取得されます。 |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | SSL 経由の IMAP を使用して、ポート 993 で Gmail に接続（user と secret を使用）すると、既読または新規のメッセージが取得されます。 |

1. 設定を保存します。

## ニュースレターサービスコンポーネントの設定 {#configuring-the-newsletter-service-component}

フィードインポーターを設定した後、送信元アドレスとバウンスカウンターを設定します。

ニュースレターサービスを設定するには：

1. `<host>:<port>/system/console/configMgr` の OSGi コンソールで、「**MCM ニュースレター**」に移動します。

1. サービスを設定して、完了したら変更内容を保存します。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   次の設定を指定すると、動作を調整できます。

   | バウンスカウンターの最大値（max.bounce.count） | ニュースレターの送信時に、ユーザーをスキップするまでのバウンス回数を定義します。この値を 0 に設定すると、バウンスのチェックが完全に無効になります。 |
   |---|---|
   | アクティビティをキャッシュしない（sent.activity.nocache） | ニュースレターの送信アクティビティに対して使用するキャッシュの設定を定義します。 |

   設定が保存されると、ニュースレター MCM サービスは次の動作を行います。

   * ニュースレター送信の正常終了時に、users の非表示ストリームにアクティビティを書き込みます。
   * バウンスが検出された場合、および users のバウンスカウンターが変化した場合に、アクティビティを書き込みます。
