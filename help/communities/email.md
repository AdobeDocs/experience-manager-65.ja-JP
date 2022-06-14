---
title: 電子メールの設定
seo-title: Configuring Email
description: コミュニティ用の電子メールの設定
seo-description: Email configuration for Communities
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 34%

---

# 電子メールの設定 {#configuring-email}

AEM Communities では次の用途のために電子メールを使用します。：

* [コミュニティの通知](notifications.md)
* [コミュニティの購読](subscriptions.md)

電子メール機能には SMTP サーバーと SMTP ユーザーの指定が必要なので、この機能はデフォルトでは使用できません。

>[!CAUTION]
>
>通知および購読用の電子メールは、 [主発行者](deploy-communities.md#primary-publisher).

## デフォルトの電子メールサービス設定 {#default-mail-service-configuration}

デフォルトの電子メールサービスは、通知と購読の両方に必要です。

* 管理者権限でプライマリパブリッシャにログインし、 [Web コンソール](../../help/sites-deploying/configuring-osgi.md):

   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* を `Day CQ Mail Service`.
* 編集アイコンを選択します。

これは、 [電子メール通知の設定](../../help/sites-administering/notification.md)が、フィールドに違いがある場合は `"From" address` が *not* 必須およびは空のままにする必要があります。

例（入力されている値は例としてのみ使用されています）：

![email-config](assets/email-config.png)

* **[!UICONTROL SMTP サーバーのホスト名]**

   *（必須）* 使用する SMTP サーバーです。

* **[!UICONTROL SMTP サーバーポート]**

   *（必須）* SMTP サーバーポートは 25 以上にする必要があります。

* **[!UICONTROL SMTP ユーザー]**

   *（必須）* SMTP ユーザーです。

* **[!UICONTROL SMTP パスワード]**

   *（必須）* SMTP ユーザーのパスワードです。

* **[!UICONTROL 「送信元」アドレス]**

   空のままにする
* **[!UICONTROL SMTP use SSL]**

   オンにすると、セキュアな E メールが送信されます。 ポートが 465 または SMTP サーバーの必要に応じて設定されていることを確認します。
* **[!UICONTROL E メールをデバッグ]**

   オンにすると、SMTP サーバーの操作のログが有効になります。

## AEM Communities の電子メール設定 {#aem-communities-email-configuration}

一度 [デフォルトのメールサービス](#default-mail-service-configuration) が設定されている場合、 `AEM Communities Email Reply Configuration` リリースに含まれる OSGi 設定が機能します。

電子メールによる返信を許可する際、購読用のインスタンスはさらに設定をおこなう必要があります。

1. [電子メール](#configuration-for-notifications) インスタンス：

   通知の場合は、返信 E メールをサポートせず、変更しないでください。

1. [購読 — 電子メール](#configuration-for-subscriptions) インスタンス：

   返信メールからの投稿の作成を完全に有効にする設定が必要です。

Communities の電子メール設定インスタンスに接続するには：

* 管理者権限でプライマリパブリッシャにログインし、 [Web コンソール](../../help/sites-deploying/configuring-osgi.md)

   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 場所 `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### 通知用の設定 {#configuration-for-notifications}

のインスタンス `AEM Communities Email Reply Configuration` 名前電子メールを使用する OSGi 設定は通知機能です。 この機能には、電子メールの返信は含まれません。

この設定は変更しないでください。

* を `AEM Communities Email Reply Configuration`.
* 編集アイコンを選択します。
* を確認します。 **名前** が `email`.

* 検証 **返信メールから投稿を作成** が `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### 購読用の設定 {#configuration-for-subscriptions}

コミュニティ購読の場合、メンバーが電子メールに返信することによりコンテンツを投稿する機能を有効にしたり無効にしたりできます。

* を `AEM Communities Email Reply Configuration`.
* 編集アイコンを選択します。
* を確認します。 **名前** が `subscriptions-email`.

   ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL 名前]**

   *（必須）* `subscriptions-email`. 編集しないでください。

* **[!UICONTROL 返信メールから投稿を作成]**

   オンにすると、購読 E メールの受信者は返信を送信してコンテンツを投稿できます。 初期設定はオンです。
* **[!UICONTROL ヘッダーにトラッキング ID を追加]**

   デフォルトは `Reply-To` です。

* **[!UICONTROL 件名の最大長]**

   トラッカー ID が件名行に追加される場合、これは件名の最大長です（トラッキングされる ID を除く）。この長さを超えると、件名はトリミングされます。 トラッカー ID 情報が失われないように、可能な限り小さい値を設定する必要があります。初期設定は 200 です。

* **[!UICONTROL 「返信先」メールアドレス]**

   「返信先」の E メールアドレスとして使用されるアドレス。 デフォルトは `no-reply@example.com` です。

* **[!UICONTROL Reply-to-Delimiter]**

   トラッカー ID が返信先ヘッダーに追加される場合は、この区切り文字が使用されます。 デフォルトはです。 `+` （プラス記号）

* **[!UICONTROL 件名のトラッカー ID プレフィックス]**

   トラッカー ID が件名行に追加される場合は、このプレフィックスが使用されます。 デフォルトは `post#` です。

* **[!UICONTROL メッセージ本文のトラッカー ID プレフィックス]**

   トラッカー ID がメッセージ本文に追加される場合は、このプレフィックスが使用されます。 デフォルトは `Please do not remove this:` です。

* **[!UICONTROL メールをHTML]**:オンにすると、Content-Type の E メールが `"text/html;charset=utf-8"`. 初期設定はオンです。

* **[!UICONTROL デフォルトのユーザー名]**

   この名前は、名前を持たないユーザーに対して使用されます。 デフォルトは `no-reply@example.com` です。

* **[!UICONTROL テンプレートのルートパス]**

   このルートパスに保存されているテンプレートを使用して電子メールが作成されます. デフォルトは `/etc/community/templates/subscriptions-email` です。

## ポーリングインポーターの設定 {#configure-polling-importer}

電子メールがリポジトリに取り込まれるように、ポーリングインポーターを設定し、そのプロパティをリポジトリで手動で設定する必要があります。

### 新しいポーリングインポーターの追加 {#add-new-polling-importer}

* 管理者権限でプライマリパブリッシャーにログインし、ポーリングインポーターコンソールを参照します。

   例： [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* 選択 **[!UICONTROL 追加]**

   ![polling importer](assets/polling-importer.png)

* **[!UICONTROL タイプ]**

   *（必須）* プルダウンして選択 `POP3 (over SSL)`.

* **[!UICONTROL URL]**

   *（必須）* 送信メールサーバー。 （例：`pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`）。

* **[!UICONTROL 読み込み先パス]**&amp;ast;

   *（必須）* に設定 `/content/usergenerated/mailFolder/postEmails`
参照して `postEmails`フォルダーと選択 **OK**.

* **[!UICONTROL 更新間隔 (単位：秒)]**

   *（オプション）* デフォルトのメールサービス用に設定されたメールサーバーには、更新間隔の値に関する要件がある場合があります。 例えば、Gmail では間隔を `300` にする必要がある場合があります。

* **[!UICONTROL ログイン]**

   *(オプション)*

* **[!UICONTROL パスワード]**

   *(オプション)*

* 「**[!UICONTROL OK]**」を選択します。

### 新しいポーリングインポーターのプロトコルの調整 {#adjust-protocol-for-new-polling-importer}

新しいポーリング設定を保存したら、プロトコルを `POP3` から `emailreply`.

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* 管理者権限でプライマリパブリッシャにログインし、次の場所を参照します。 [https://&lt;server>:&lt;port>/crx/de/index.jsp](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* 新しく作成した設定を選択し、次のプロパティを変更します。

   * **feedType**:置換 `pop3s` と **`emailreply`**
   * **ソース**:ソースのプロトコルを置換 `pop3s://` と **`emailreply://`**

![polling-protocol](assets/polling-protocol.png)

赤い三角は、変更したプロパティを示します。変更内容を保存してください。

* **[!UICONTROL すべて保存]** を選択します。
