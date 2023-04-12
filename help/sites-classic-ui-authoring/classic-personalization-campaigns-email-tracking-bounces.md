---
title: バウンス（配信不能）メールの追跡
seo-title: Tracking Bounced Emails
description: 多くのユーザーにニュースレターを送信する場合、通常、リストに無効な電子メールアドレスが含まれています。 そのアドレスにニュースレターを送信すると、バウンスが戻ります。 AEMは、これらのバウンスを管理し、設定されたバウンスカウンターを超えた後に、それらのアドレスへのニュースレターの送信を停止できます。
seo-description: When you send a newsletter to many users, there are usually some invalid emails addresses in the list. Sending newsletters to those addresses bounce back. AEM is capable of managing those bounces and can stop sending newsletters to those addresses after the configured bounce counter is exceeded.
uuid: 749959f2-e6f8-465f-9675-132464c65f11
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: fde9027b-9057-48c3-ae34-3f3258c5b371
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 15%

---

# バウンス（配信不能）メールの追跡 {#tracking-bounced-emails}

>[!NOTE]
>
>アドビは、AEM SMTP サービスによって送信される開封済みまたはバウンス済みのメールの追跡をさらに強化する予定はありません。
>
>お勧めは、 [Adobe CampaignとそのAEM統合の使用](/help/sites-administering/campaign.md).

多くのユーザーにニュースレターを送信する場合、通常、リストに無効な電子メールアドレスが含まれています。 そのアドレスにニュースレターを送信すると、バウンスが戻ります。 AEMは、これらのバウンスを管理し、設定されたバウンスカウンターを超えた後に、それらのアドレスへのニュースレターの送信を停止できます。 デフォルトではバウンス率は 3 になっていますが、設定可能です。

バウンスメールを追跡するAEMを設定するには、バウンスメールが受信された既存のメールボックスをポーリングするAEMを設定します。 通常、この場所は、ニュースレターの送信先を指定する「送信者」の電子メールアドレスです。 AEM はこのインボックスをポーリングし、ポーリング設定で指定されたパスの下のすべてのメールを読み込みます。次に、ワークフローがトリガーされ、各ユーザー内のバウンスメールアドレスが検索され、それに応じて、ユーザーの bounceCounter プロパティの値が更新されます。設定された最大バウンス数を超えると、ユーザーはニュースレターリストから削除されます。

## フィードインポーターの設定 {#configuring-the-feed-importer}

フィードインポーターを使用すると、外部ソースからリポジトリにコンテンツを繰り返し読み込むことができます。 フィードインポーターのこの設定を使用して、AEMは送信者のメールボックスでバウンスメールを確認します。

バウンスメールを追跡するようにフィードインポーターを設定するには、以下の手順を実行します。

1. In **ツール**」で、「フィードインポーター」を選択します。

1. クリック **追加** 設定を作成します。

   ![chlimage_1](assets/chlimage_1a.png)

1. タイプを選択し、ポーリング URL に情報を追加して、ホストとポートを設定することで、設定を追加します。 さらに、URL クエリにメールおよびプロトコル固有のパラメーターを追加します。 1 日に 1 回以上ポーリングするように設定します。

   すべての設定で、ポーリング URL に以下に関する情報が必要です。

   `username`:接続に使用するユーザー名

   `password`:接続に使用するパスワード

   さらに、プロトコルに応じて、特定の設定を指定できます。

   **POP3 設定プロパティ：**

   `pop3.leave.on.server`：サーバー上にメッセージを残すかどうかを定義します。メッセージをサーバーに残す場合は true に、それ以外の場合は false に設定します。 デフォルトは true です。

   **POP3 の例：**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | SSL 経由の pop3 を使用して、ポート 995 の GMail に user/secret で接続し、デフォルトでサーバー上にメッセージを残す |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP 構成プロパティ：**

   検索するフラグを設定できます。

   `imap.flag.SEEN`：新規または未読のメッセージには false を、既読のメッセージには true を設定します。

   詳しくは、 [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) フラグの完全なリストを参照してください。

   **IMAP の例：**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | SSL 経由の IMAP を使用して、ポート 993 の GMail に、user/secret で接続します。 デフォルトでのみ新しいメッセージを取得します。 |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | IMAP over SSL を使用して、user/secret で GMail 993 に接続し、既にメッセージが表示されている場合に限り、 |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | SSL 経由の IMAP を使用して、user/secret で GMail 993 に接続し、既に読み込まれている、または新しいメッセージを取得します。 |

1. 設定を保存します。

## ニュースレターサービスコンポーネントの設定 {#configuring-the-newsletter-service-component}

フィードインポーターを設定した後、送信元アドレスとバウンスカウンターを設定します。

ニュースレターサービスを設定するには：

1. OSGi コンソールで、 `<host>:<port>/system/console/configMgr`に移動します。 **MCM ニュースレター**.

1. サービスを設定して、完了したら変更内容を保存します。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   動作を調整するには、次の設定を指定できます。

   | バウンスカウンターの最大値 (max.bounce.count) | ニュースレターの送信時にユーザーが省略されるまでのバウンス数を定義します。 この値を 0 に設定すると、バウンスのチェックが完全に無効になります。 |
   |---|---|
   | アクティビティキャッシュなし (sent.activity.nocache) | ニュースレター送信アクティビティで使用するキャッシュ設定を定義します |

   保存すると、ニュースレター MCM サービスは次の処理を実行します。

   * ニュースレターの送信が成功した場合に、ユーザーの非表示ストリームにアクティビティを書き込みます。
   * バウンスが検出され、ユーザーのバウンスカウンターが変更された場合に、アクティビティを書き込みます。
