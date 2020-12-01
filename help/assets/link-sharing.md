---
title: リンクを使用したアセットの共有
description: アセット、フォルダーおよびコレクションをURLとして共有します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 1f6da1c69ea3b3c3f07e8ac10fd8e1e9c7208158
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 33%

---


# リンクを使用したアセットの共有 {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] アセット、フォルダー、コレクションをURLとして組織のメンバーと、パートナーやベンダーを含む外部エンティティと共有できます。 Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to [!DNL Assets].

>[!PREREQUISITES]
>
>* リンクとして共有するフォルダーまたはアセットのACLを編集権限が必要です。
>* ユーザーに電子メールを送信するには、 [Day CQ Mail ServiceでSMTPサーバーの詳細を設定します](#configmailservice)。


## アセットの共有 {#sharelink}

ユーザーと共有するアセットのURLを生成するには、リンクの共有ダイアログを使用します。 `/var/dam/share` の場所への管理者特権または読み取り権限を持つユーザーが、共有されたリンクを表示することができます。

1. In the [!DNL Assets] user interface, select the asset to share as a link.
1. From the toolbar, click the **[!UICONTROL Share Link]** ![share assets icon](assets/do-not-localize/assets_share.png).

   「 [!UICONTROL 共有] 」をクリックした後に作成されるリンクは、あらかじめ「 [!UICONTROL 共有リンク] 」フィールドに表示されます。 リンクのデフォルトの有効期間は 1 日です。

   ![「リンクを共有」と表示されたダイアログ](assets/Link-sharing-dialog-box.png)

   *図：アセットをリンクとして共有するためのダイアログ。*

   >[!NOTE]
   >
   >If you want to share links from your [!DNL Experience Manager] Author deployment to external entities, ensure that you only expose the following URLs (which are used for link sharing) for `GET` requests only. セキュリティ上の理由から他のURLをブロックします。
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. インター [!DNL Experience Manager] フェイスで、 **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソールにアクセスします]**。

1. **[!UICONTROL Day CQ Link Externalizerの設定を開き、「]** Domains **[!UICONTROL 」フィールドの次のプロパティを、「]** 、 `local`」、「」、「」に関する値で変更しま `author``publish`す。 For the `local` and `author` properties, provide the URL for the local and the author instance respectively. Both `local` and `author` properties have the same value if you run a single [!DNL Experience Manager] author instance. For Publish instances, provide the URL for the [!DNL Experience Manager] publish instance.

1. **[!UICONTROL リンク共有]**&#x200B;ダイアログの電子メールアドレスボックスに、リンクを共有するユーザーの電子メール ID を入力します。1人以上のユーザーを追加できます。

   ![アセットへのリンクをリンク共有ダイアログから直接共有する](assets/Asset-Sharing-LinkShareDialog.png)

   *図：リンクの共有ダイアログからアセットへのリンクを直接 [!UICONTROL 共有します] 。*

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words [!UICONTROL External User] are prefixed with the email ID of the user.

1. 「 **[!UICONTROL 件名]** 」フィールドに、件名を入力します。

1. In the **[!UICONTROL Message]** field, enter an optional message.

1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link to stop working. デフォルトでは、有効期限日はリンクを共有した日から 1 週間後に設定されます。

   ![共有リンクの有効期限の設定](assets/Set-shared-link-expiration.png)

1. To let users download the original asset along with the renditions, select **[!UICONTROL Allow download of original file]**. デフォルトでは、ユーザーはリンクとして共有されているアセットのレンディションのみをダウンロードできます。

1. 「**[!UICONTROL 共有]**」をクリックします。リンクが電子メールでユーザーと共有されていることを確認するメッセージが表示されます。

1. 共有アセットを表示するには、ユーザーに送信する電子メール内のリンクをクリックします。 共有アセットが **[!UICONTROL Adobe Marketing Cloud]** ページに表示されます。

   ![chlimage_1-260](assets/chlimage_1-545.png)

1. アセットのプレビューを生成するには、共有アセットをクリックします。 To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] は、サポートされているファイルタイプのみのアセット [のプレビューの生成をサポートしています](/help/assets/assets-formats.md)。 他のMIMEタイプが共有されている場合は、アセットのダウンロードのみが可能で、プレビューはできません。

1. To download the shared asset, click **[!UICONTROL Select]** from the toolbar, click the asset, and then click **[!UICONTROL Download]** from the toolbar.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. リンクとして共有したアセットを表示するには、ユー [!DNL Assets] ザインターフェイスに移動し、ロ [!DNL Experience Manager] ゴをクリックします。 「 **[!UICONTROL ナビゲーション]**」を選択します。 In the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.

1. To un-share an asset, select it and click **[!UICONTROL Unshare]** from the toolbar. 確認メッセージが次に表示されます。 アセットのエントリがリストから削除されます。

## Day CQ 電子メールサービスの設定 {#configmailservice}

1. ホームページで、 [!DNL Experience Manager] ツール **[!UICONTROL /]** 操作 **[!UICONTROL /]** Webコンソールに移動します ****。
1. サービスのリストから、**[!UICONTROL Day CQ Mail Service]** を探します。
1. Click **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * SMTP server host name：電子メールサーバーのホスト名
   * SMTP server port：電子メールサーバーのポート
   * SMTP user：メールサーバーのユーザー名
   * SMTP password：電子メールサーバーのパスワード

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

## 最大データサイズの設定 {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, [!DNL Experience Manager] compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. ただし、ZIP ファイルとして圧縮できるデータ量に制限がないと、膨大なデータが圧縮の対象となり、JVM のメモリ不足エラーの原因となります。この状況による潜在的な DoS 攻撃からシステムを保護するには、Configuration Manager で Day CQ DAM Adhoc Asset Share Proxy Servlet の「**[!UICONTROL Max Content Size (uncompressed)]**」パラメーターを使用して、最大サイズを設定します。アセットの未圧縮時のサイズが設定値を超えていると、アセットのダウンロード要求は拒否されます。デフォルト値は 100 MB です。

1. Click the [!DNL Experience Manager] logo and then go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. From the Web Console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. 「**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**」設定を編集モードで開き、「**[!UICONTROL Max Content Size (uncompressed)]**」パラメーターの値を変更します。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 変更内容を保存します。

## ベストプラクティスとトラブルシューティング {#bestpractices}

* 名前に空白を含むアセットフォルダーまたはコレクションは共有されない場合があります。
* If users cannot download the shared assets, check with your [!DNL Experience Manager] administrator what the [download limits](#maxdatasize) are.
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your [!DNL Experience Manager] administrator if the [email service](#configmailservice) is configured or not.
* リンク共有機能を使用してアセットを共有できない場合は、適切な権限を持っていることを確認してください。[アセットの共有](#sharelink)を参照してください。
* 共有アセットが別の場所に移動されると、そのリンクは機能しなくなります。リンクを再作成し、ユーザーと再共有します。
