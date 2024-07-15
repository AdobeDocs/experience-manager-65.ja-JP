---
title: メールの設定
description: Adobe Experience Manager Communities のメール通知と購読を設定する方法について説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 4%

---

# メールの設定 {#configuring-email}

AEM Communitiesは、次の目的でメールを使用します。

* [コミュニティの通知](notifications.md)
* [コミュニティの購読](subscriptions.md)

デフォルトでは、メール機能は機能しません。SMTP サーバーと SMTP ユーザーを指定する必要があるからです。

>[!CAUTION]
>
>通知および購読の電子メールは、[ プライマリ発行者 ](deploy-communities.md#primary-publisher) 上でのみ設定する必要があります。

## デフォルトのメールサービス設定 {#default-mail-service-configuration}

通知と購読の両方にデフォルトのメールサービスが必要です。

* 管理者権限でプライマリパブリッシャーにログインし、[Web コンソール ](../../help/sites-deploying/configuring-osgi.md) にアクセスします。

   * 例：[http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* `Day CQ Mail Service` を見つけます。
* 編集アイコンを選択します。

これは [ メール通知の設定 ](../../help/sites-administering/notification.md) のドキュメントに基づいていますが、「`"From" address`」フィールドは必須 *ではなく* 空のままにする必要がある点が異なります。

例（例として値が入力されている）:

![email-config](assets/email-config.png)

* **[!UICONTROL SMTP サーバーのホスト名]**

  *（必須）* 使用する SMTP サーバー。

* **[!UICONTROL SMTP サーバーポート]**

  *（必須）* SMTP サーバーポートは 25 以上にする必要があります。

* **[!UICONTROL SMTP ユーザー]**

  *（必須）* SMTP ユーザー。

* **[!UICONTROL SMTP パスワード]**

  *（必須）* SMTP ユーザーのパスワード。

* **[!UICONTROL 「送信者」アドレス]**

  空のままにします
* **[!UICONTROL SMTP での SSL の使用]**

  オンにした場合、セキュリティで保護されたメールを送信します。 ポートが 465 か、SMTP サーバーの要件に応じて設定されていることを確認します。
* **[!UICONTROL Debug Email]**

  オンにすると、SMTP サーバーインタラクションのログが有効になります。

## AEM Communitiesのメール設定 {#aem-communities-email-configuration}

[ デフォルトメールサービス ](#default-mail-service-configuration) を設定すると、リリースに含まれている `AEM Communities Email Reply Configuration` OSGi 設定の既存の 2 つのインスタンスが機能するようになります。

メールによる返信を許可する場合は、購読のインスタンスのみを、さらに設定する必要があります。

1. [ メール ](#configuration-for-notifications) インスタンス：

   は、返信メールをサポートしないので、変更しないでください。

1. [Subscriptions-email](#configuration-for-subscriptions) インスタンス：

   返信メールからの投稿の作成を完全に有効にするための設定が必要です。

Communities のメール設定インスタンスにアクセスするには：

* 管理者権限でプライマリパブリッシャーにログインし、[Web コンソール ](../../help/sites-deploying/configuring-osgi.md) にアクセスします

   * 例：[http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* `AEM Communities Email Reply Configuration` を見つけます。

![email-reply-config](assets/email-reply-config.png)

### 通知の設定 {#configuration-for-notifications}

名前がメール `AEM Communities Email Reply Configuration` 持つ OSGi 設定のインスタンスは、forthenotifications 機能です。 この機能にはメール返信は含まれません。

この設定は変更しないでください。

* `AEM Communities Email Reply Configuration` を見つけます。
* 編集アイコンを選択します。
* **Name** が `email` であることを確認します。

* **返信メールから投稿を作成** が `unchecked` しいことを確認します。

![configure-email-reply](assets/configure-email-reply.png)

### サブスクリプションの設定 {#configuration-for-subscriptions}

コミュニティの購読の場合、メンバーがメールに返信してコンテンツを投稿する機能を有効または無効にすることができます。

* `AEM Communities Email Reply Configuration` を見つけます。
* 編集アイコンを選択します。
* **Name** が `subscriptions-email` であることを確認します。

  ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL 名前]**

  *（必須）* `subscriptions-email`。 編集しないでください。

* **[!UICONTROL 返信メールから投稿を作成]**

  オンにすると、購読メールの受信者は、返信を送信してコンテンツを投稿できます。 デフォルトではオンになっています。
* **[!UICONTROL トラッキング対象 ID をヘッダーに追加]**

  デフォルトは `Reply-To` です。

* **[!UICONTROL 対象の最大長]**

  件名行にトラッカー ID が追加されている場合、これは、トラッキングされた ID を除く、件名の最大長であり、その後でトリミングされます。 トラッキング対象の ID 情報が失われるのを防ぐため、この値はできるだけ小さくしてください。 デフォルトは 200 です。

* **[!UICONTROL 「返信先」のメールアドレス]**

  「返信先」メールアドレスとして使用するアドレス。 デフォルトは `no-reply@example.com` です。

* **[!UICONTROL Reply-to-Delimiter]**

  返信先ヘッダーにトラッカー ID が追加されている場合は、この区切り文字が使用されます。 デフォルトは `+` （プラス記号）です。

* **[!UICONTROL 件名のトラッカー ID プレフィックス]**

  件名行にトラッカー ID が追加されている場合は、このプレフィックスが使用されます。 デフォルトは `post#` です。

* **[!UICONTROL メッセージ本文のトラッカー ID プレフィックス]**

  トラッカー ID がメッセージ本文に追加された場合は、このプレフィックスが使用されます。 デフォルトは `Please do not remove this:` です。

* **[!UICONTROL HTMLとしてメール]**: オンにすると、メールのコンテンツタイプが `"text/html;charset=utf-8"` に設定されます。 デフォルトではオンになっています。

* **[!UICONTROL デフォルトのユーザー名]**

  この名前は、名前のないユーザーに使用されます。 デフォルトは `no-reply@example.com` です。

* **[!UICONTROL テンプレートのルートパス]**

  メールは、このルートパスに保存されたテンプレートを使用して作成されます。 デフォルトは `/etc/community/templates/subscriptions-email` です。

## ポーリングインポーターの設定 {#configure-polling-importer}

メールをリポジトリに取得するには、ポーリングインポーターを設定し、リポジトリでそのプロパティを手動で設定する必要があります。

### 新しいポーリングインポーターを追加 {#add-new-polling-importer}

* 管理者権限でプライマリパブリッシャーにログインし、ポーリングインポーターコンソールを参照します。

  例：[http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* 「**[!UICONTROL 追加]**」を選択します

  ![polling-importer](assets/polling-importer.png)

* **[!UICONTROL タイプ]**

  *（必須）* プルダウンして `POP3 (over SSL)` を選択します。

* **[!UICONTROL URL]**

  *（必須）* 送信メールサーバー。 例えば、`pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****` のように指定します。

* **[!UICONTROL パスにインポート]**&amp;ast;

  *（必須）*`/content/usergenerated/mailFolder/postEmails` に設定
`postEmails` フォルダーに移動して、「**OK**」を選択します。

* **[!UICONTROL 更新間隔（秒）]**

  *（任意）* デフォルトのメールサービス用に設定されたメールサーバーには、更新間隔の値に関する要件が存在する場合があります。 例えば、Gmail では `300` の間隔が必要な場合があります。

* **[!UICONTROL ログイン]**

  *（オプション）*

* **[!UICONTROL パスワード]**

  *（オプション）*

* 「**[!UICONTROL OK]**」を選択します。

### 新しいポーリングインポーターのプロトコルの調整 {#adjust-protocol-for-new-polling-importer}

新しいポーリング設定を保存したら、サブスクリプションメールインポーターのプロパティをさらに変更して、プロトコルを `POP3` から `emailreply` に変更する必要があります。

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用：

* 管理者権限でプライマリパブリッシャーにログインし、[https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling) を参照します。
* 新しく作成した設定を選択し、次のプロパティを変更します。

   * **feedType**: `pop3s` を **`emailreply`** に置き換えます
   * **source**: ソースのプロトコル `pop3s://` を **`emailreply://`** に置き換えます

![polling-protocol](assets/polling-protocol.png)

赤い三角形は、変更されたプロパティを示します。 必ず変更内容を保存してください。

* 「**[!UICONTROL すべて保存]**」を選択します。
