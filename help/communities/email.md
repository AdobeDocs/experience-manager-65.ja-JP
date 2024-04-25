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
>通知および購読用の電子メールは、 [プライマリ発行者](deploy-communities.md#primary-publisher).

## デフォルトのメールサービス設定 {#default-mail-service-configuration}

通知と購読の両方にデフォルトのメールサービスが必要です。

* 管理者権限でプライマリパブリッシャーにログインし、 [Web コンソール](../../help/sites-deploying/configuring-osgi.md):

   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* を見つけます。 `Day CQ Mail Service`.
* 編集アイコンを選択します。

これは、のドキュメントに基づいています。 [メール通知の設定](../../help/sites-administering/notification.md)しかし、そのフィールドの違いを持つ `"From" address` 等しい *ではない* 必須。は空のままにする必要があります。

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

* **[!UICONTROL 「差出人」のアドレス]**

  空のままにします
* **[!UICONTROL SMTP SSL を使用]**

  オンにした場合、セキュリティで保護されたメールを送信します。 ポートが 465 か、SMTP サーバーの要件に応じて設定されていることを確認します。
* **[!UICONTROL Debug email]**

  オンにすると、SMTP サーバーインタラクションのログが有効になります。

## AEM Communitiesのメール設定 {#aem-communities-email-configuration}

に達したら、 [既定のメール サービス](#default-mail-service-configuration) が設定され、の 2 つの既存のインスタンスが `AEM Communities Email Reply Configuration` リリースに含まれている OSGi 設定が機能するようになります。

メールによる返信を許可する場合は、購読のインスタンスのみを、さらに設定する必要があります。

1. [電子メール](#configuration-for-notifications) インスタンス：

   は、返信メールをサポートしないので、変更しないでください。

1. [購読 – メール](#configuration-for-subscriptions) インスタンス：

   返信メールからの投稿の作成を完全に有効にするための設定が必要です。

Communities のメール設定インスタンスにアクセスするには：

* 管理者権限でプライマリパブリッシャーにログインし、 [Web コンソール](../../help/sites-deploying/configuring-osgi.md)

   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* を見つける `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### 通知の設定 {#configuration-for-notifications}

次のインスタンス `AEM Communities Email Reply Configuration` 名前がメールの OSGi 設定は、認証機能です。 この機能にはメール返信は含まれません。

この設定は変更しないでください。

* を見つけます。 `AEM Communities Email Reply Configuration`.
* 編集アイコンを選択します。
* を確認します **名前** 等しい `email`.

* を確認します。 **返信メールから投稿を作成** 等しい `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### サブスクリプションの設定 {#configuration-for-subscriptions}

コミュニティの購読の場合、メンバーがメールに返信してコンテンツを投稿する機能を有効または無効にすることができます。

* を見つけます。 `AEM Communities Email Reply Configuration`.
* 編集アイコンを選択します。
* を確認します **名前** 等しい `subscriptions-email`.

  ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL 名前]**

  *（必須）* `subscriptions-email`. 編集しないでください。

* **[!UICONTROL 返信メールから投稿を作成]**

  オンにすると、購読メールの受信者は、返信を送信してコンテンツを投稿できます。 デフォルトではオンになっています。
* **[!UICONTROL トラッキングされた ID をヘッダーに追加]**

  デフォルトは `Reply-To` です。

* **[!UICONTROL 件名の最大長]**

  件名行にトラッカー ID が追加されている場合、これは、トラッキングされた ID を除く、件名の最大長であり、その後でトリミングされます。 トラッキング対象の ID 情報が失われるのを防ぐため、この値はできるだけ小さくしてください。 デフォルトは 200 です。

* **[!UICONTROL 「返信先」のメールアドレス]**

  「返信先」メールアドレスとして使用するアドレス。 デフォルトは `no-reply@example.com` です。

* **[!UICONTROL 返信先区切り文字]**

  返信先ヘッダーにトラッカー ID が追加されている場合は、この区切り文字が使用されます。 デフォルトは `+` （プラス記号）。

* **[!UICONTROL 件名のトラッカー ID プレフィックス]**

  件名行にトラッカー ID が追加されている場合は、このプレフィックスが使用されます。 デフォルトは `post#` です。

* **[!UICONTROL メッセージ本文のトラッカー ID プレフィックス]**

  トラッカー ID がメッセージ本文に追加された場合は、このプレフィックスが使用されます。 デフォルトは `Please do not remove this:` です。

* **[!UICONTROL HTMLとしてメールを送信]**：オンにした場合、メールのコンテンツタイプは次のように設定されます `"text/html;charset=utf-8"`. デフォルトではオンになっています。

* **[!UICONTROL デフォルトのユーザー名]**

  この名前は、名前のないユーザーに使用されます。 デフォルトは `no-reply@example.com` です。

* **[!UICONTROL テンプレートのルートパス]**

  メールは、このルートパスに保存されたテンプレートを使用して作成されます。 デフォルトは `/etc/community/templates/subscriptions-email` です。

## ポーリングインポーターの設定 {#configure-polling-importer}

メールをリポジトリに取得するには、ポーリングインポーターを設定し、リポジトリでそのプロパティを手動で設定する必要があります。

### 新しいポーリングインポーターを追加 {#add-new-polling-importer}

* 管理者権限でプライマリパブリッシャーにログインし、ポーリングインポーターコンソールを参照します。

  例： [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* を選択 **[!UICONTROL 追加]**

  ![polling-importer](assets/polling-importer.png)

* **[!UICONTROL タイプ]**

  *（必須）* プルダウンして選択 `POP3 (over SSL)`.

* **[!UICONTROL URL]**

  *（必須）* 送信メールサーバー。 例えば、`pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****` のように指定します。

* **[!UICONTROL パスにインポート]**&amp;ast;

  *（必須）* をに設定 `/content/usergenerated/mailFolder/postEmails`
にブラウジングする `postEmails`フォルダーと選択 **OK**.

* **[!UICONTROL 更新間隔（秒）]**

  *（オプション）* デフォルトメールサービス用に設定されたメールサーバーには、更新間隔の値に関する要件が存在する場合があります。 例えば、Gmail では次の間隔が必要な場合があります `300`.

* **[!UICONTROL ログイン]**

  *（オプション）*

* **[!UICONTROL パスワード]**

  *（オプション）*

* 「**[!UICONTROL OK]**」を選択します。

### 新しいポーリングインポーターのプロトコルの調整 {#adjust-protocol-for-new-polling-importer}

新しいポーリング設定を保存したら、プロトコルを変更するサブスクリプションメールインポーターのプロパティをさらに変更する必要があります。 `POP3` 対象： `emailreply`.

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 管理者権限でプライマリパブリッシャーにログインし、を参照します。 [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* 新しく作成した設定を選択し、次のプロパティを変更します。

   * **feedType**:Replace `pop3s` （を使用） **`emailreply`**
   * **ソース**：ソースのプロトコルを置換 `pop3s://` （を使用） **`emailreply://`**

![ポーリングプロトコル](assets/polling-protocol.png)

赤い三角形は、変更されたプロパティを示します。 必ず変更内容を保存してください。

* 「**[!UICONTROL すべて保存]**」を選択します。
