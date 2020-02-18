---
title: 電子メールの設定
seo-title: 電子メールの設定
description: コミュニティ用の電子メールの設定
seo-description: コミュニティ用の電子メールの設定
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 電子メールの設定 {#configuring-email}

AEM Communities では次の用途のために電子メールを使用します。

* [コミュニティの通知](notifications.md)
* [コミュニティの購読](subscriptions.md)

電子メール機能には SMTP サーバーと SMTP ユーザーの指定が必要なので、この機能はデフォルトでは使用できません。

>[!CAUTION]
>
>Email for notifications and subscriptions must be configured only on the [primary publisher](deploy-communities.md#primary-publisher).

## デフォルトの電子メールサービス設定 {#default-mail-service-configuration}

デフォルトの電子メールサービスは、通知と購読の両方に必要です。

* プライマリパブリッシャー
* 管理者権限でサインインしています
* Access the [Web Console](../../help/sites-deploying/configuring-osgi.md)

   * For example, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Folio Builderで `Day CQ Mail Service`
* 編集アイコンを選択します

This is based on the documentation for [Configuring Email Notification](../../help/sites-administering/notification.md), but with a difference in that the field `"From" address` is *not* required and should be left empty.

例（入力されている値は例としてのみ使用されています）：

![chlimage_1-98](assets/chlimage_1-98.png)

* **[!UICONTROL SMTPサーバーのホスト名]**: *（必須）* 、使用するSMTPサーバー。

* **[!UICONTROL SMTPサーバーポート]** （必須） ** SMTPサーバーポートは25以上である必要があります。

* **[!UICONTROL SMTP user]**: *（必須）* SMTPユーザー。

* **[!UICONTROL SMTP password]**: *（必須）* SMTPユーザーのパスワードです。

* **[!UICONTROL &quot;送信者&quot;アドレス]**:空白のままにする
* **[!UICONTROL SMTP use SSL]**:オンにすると、セキュリティで保護された電子メールが送信されます。 ポートが465に設定されているか、SMTPサーバーに必要なポートであることを確認します。
* **[!UICONTROL Debug email]**:オンの場合、SMTPサーバーの操作のログを有効にします。

## AEM Communities の電子メール設定 {#aem-communities-email-configuration}

Once the [default mail service](#default-mail-service-configuration) is configured, the two existing instances of the `AEM Communities Email Reply Configuration` OSGi config, included in the release, become functional.

電子メールによる返信を許可する際、購読用のインスタンスはさらに設定をおこなう必要があります。

1. ` [email](#configuration-for-notifications)` インスタンス

   通知に対して使用します。この通知は、返信電子メールをサポートせず、変更しないでください。

1. ` [subscriptions-email](#configuration-for-subscriptions)` インスタンス

   返信電子メールからの投稿の作成を完全に有効にする設定が必要です

Communities の電子メール設定インスタンスに接続するには：

* プライマリパブリッシャー
* 管理者権限でサインインしています
* Access the [Web Console](../../help/sites-deploying/configuring-osgi.md)

   * For example, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Locate `AEM Communities Email Reply Configuration`

![chlimage_1-99](assets/chlimage_1-99.png)

### 通知用の設定 {#configuration-for-notifications}

名前電子メールを `AEM Communities Email Reply Configuration` 使用したOSGi設定のインスタンスは通知機能です。 この機能には、電子メールの返信は含まれません。

この設定は変更しないでください。

* Folio Builderで `AEM Communities Email Reply Configuration`
* 編集アイコンを選択します
* Verify the **Name** is `email`

* Verify **Create post from reply email** is `unchecked`

![chlimage_1-100](assets/chlimage_1-100.png)

### 購読用の設定 {#configuration-for-subscriptions}

コミュニティ購読の場合、メンバーが電子メールに返信することによりコンテンツを投稿する機能を有効にしたり無効にしたりできます。

* Folio Builderで `AEM Communities Email Reply Configuration`
* 編集アイコンを選択します
* Verify the **Name** is `subscriptions-email`

![chlimage_1-101](assets/chlimage_1-101.png)

* **[!UICONTROL 名前]** : *（必須）*`subscriptions-email`。 編集しない。

* **[!UICONTROL Create post from reply email]**：オンにすると、購読電子メールの受信者は応答を送信することによりコンテンツを投稿できます。初期設定はオンです。
* **[!UICONTROL Add tracked id to header]**：デフォルトは `Reply-To` です。

* **[!UICONTROL 件名の最大長]**:トラッカーIDを件名行に追加した場合、これは件名の最大長です（追跡対象IDは除く）。この長さを超えると、トリミングされます。 トラッカー ID 情報が失われないように、可能な限り小さい値を設定する必要があります。初期設定は 200 です。
* **[!UICONTROL 電子メール「送信者」アドレス]**: *（必須）* 、通知電子メールの配信元のアドレス。 Likely the same **SMTP user** specified for the [default mail service](#configuredefaultmailservice). デフォルトは `no-reply@example.com` です。

* **[!UICONTROL Reply-to-Delimiter]**:トラッカーIDが返信先ヘッダーに追加された場合、この区切り文字が使用されます。 Default is `+` (plus sign).

* **[!UICONTROL 件名のトラッカーIDプレフィックス]**:トラッカーIDが件名行に追加された場合は、このプレフィックスが使用されます。 デフォルトは `post#` です。

* **[!UICONTROL メッセージ本文のトラッカーIDプレフィックス]**:トラッカーIDがメッセージの本文に追加された場合は、このプレフィックスが使用されます。 デフォルトは `Please do not remove this:` です。

* **[!UICONTROL HTMLとして電子メール]**:オンにすると、電子メールのコンテンツタイプがとして設定されま `"text/html;charset=utf-8"`す。 初期設定はオンです。

* **[!UICONTROL デフォルトのユーザー名]**:この名前は、名前を持つユーザーには使用されません。 デフォルトは `no-reply@example.com` です。

* **[!UICONTROL テンプレートのルートパス]**:電子メールは、このルートパスに保存されたテンプレートを使用して作成されます。 デフォルトは `/etc/community/templates/subscriptions-email` です。

## ポーリングインポーターの設定 {#configure-polling-importer}

電子メールがリポジトリに取り込まれるように、ポーリングインポーターを設定し、そのプロパティをリポジトリで手動で設定する必要があります。

### 新しいポーリングインポーターの追加 {#add-new-polling-importer}

* プライマリパブリッシャー
* 管理者権限でサインインしています
* ポーリングインポーターコンソール(例： [http://localhost:4503/etc/importers/polling.html)を参照します。](http://localhost:4503/etc/importers/polling.html)
* Select **[!UICONTROL Add]**

![chlimage_1-102](assets/chlimage_1-102.png)

* **[!UICONTROL タイプ]**: *（必須）* Pull down to select `POP3 (over SSL).`

* **[!UICONTROL URL]**：*（必須）*&#x200B;アウトバウンド電子メールサーバー。例：`pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`

* **[!UICONTROL パスマップに読み込み]**(&amp;A);ast;: *（必須）* 、フォルダ `/content/usergenerated/mailFolder/postEmails`ーを参照し、「 `postEmails`OK」 **を選択します**

* **[!UICONTROL 更新間隔(秒]**):デフォ ** ルトのメールサービス用に設定されたメールサーバーは、更新間隔の値に関する要件を持つ場合があります。 例えば、Gmail では間隔を `300` にする必要がある場合があります。

* **[!UICONTROL ログイン]**: *（オプション）*

* **[!UICONTROL パスワード]**：*（オプション）*

* 「**[!UICONTROL OK]**」を選択します。

### 新しいポーリングインポーターのプロトコルの調整 {#adjust-protocol-for-new-polling-importer}

新しいポーリング設定が保存されたら、購読電子メールインポーターのプロパティをさらに変更し、プロトコルを `POP3` から `emailreply` に変更する必要があります

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* プライマリパブリッシャー
* 管理者権限でサインインしています
* Browse to [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)
* 新しく作成した設定を選択します
* 次のプロパティを変更します

   * **feedType**:置き換 `pop3s` える **`emailreply`**
   * **source**:ソースのプロトコルを～に置き換 `pop3s://` える **`emailreply://`**

![chlimage_1-103](assets/chlimage_1-103.png)

赤い三角は、変更したプロパティを示します。変更内容を保存してください。

* 「**[!UICONTROL すべて保存]**」を選択します。

