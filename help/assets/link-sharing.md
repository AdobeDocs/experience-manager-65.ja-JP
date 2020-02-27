---
title: 共有アセットへのURLの生成
description: この記事では、AEM Assets 内のアセット、フォルダーおよびコレクションを URL として外部の関係者と共有する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# リンクを使用したアセットの共有 {#asset-link-sharing}

Adobe Experience Manager（AEM）Assets では、アセット、フォルダーおよびコレクションを URL として、組織内や外部（パートナー、ベンダーを含む）のメンバーと共有できます。リンクを使用したアセットの共有は、AEM Assetsに最初にログインしなくても、外部のユーザーがリソースを利用できるようにする便利な方法です。

>[!NOTE]
>
>リンクとして共有するフォルダーまたはアセットに対するACLの編集権限が必要です。

## アセットの共有 {#sharelink}

ユーザーと共有するアセットの URL を生成するには、リンク共有ダイアログを使用します。Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them.

>[!NOTE]
>
>リンクをユーザーと共有する前に、Day CQ Mail Service が設定されていることを確認してください。[Day CQ Mail Service を設定](/help/assets/link-sharing.md#configmailservice)せずにリンクの共有を試行すると、エラーが発生します。

1. Assets のユーザーインターフェイスで、リンクとして共有するアセットを選択します。
1. From the toolbar, click/tap the **[!UICONTROL Share Link]** ![assets_share](assets/assets_share.png).

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. このリンクをコピーしてユーザーと共有します。リンクのデフォルトの有効期間は 1 日です。

   ![「リンクを共有」と表示されたダイアログ](assets/Link-sharing-dialog-box.png)

   *図：リンク共有のダイアログ*

   または、この手順の 3～7 に進んで電子メールの受信者を追加し、リンクの有効期限を設定して、ダイアログから送信することもできます。

   >[!NOTE]
   >
   >If you want to share links from your AEM Author instance to external entities, ensure that you only expose the following URLs (which are used for link sharing) for `GET` requests only. 他のURLをブロックして、AEM Authorのセキュリティを確保します。
   >
   >* http://&lt;aem_server>:&lt;port>/linkshare.html
   * http://&lt;aem_server>:&lt;port>/linksharepreview.html
   * http://&lt;aem_server>:&lt;port>/linkexpired.html


   >[!NOTE]
   共有アセットが別の場所に移動されると、そのリンクは機能しなくなります。リンクを再作成し、ユーザーと再共有します。

1. Web コンソールで、**[!UICONTROL Day CQ Link Externalizer]** 設定を開き、「**[!UICONTROL ドメイン]**」フィールドで次のプロパティの値をそれぞれ変更します。

   * local
   * author
   * publish
   local プロパティと author プロパティには、それぞれローカルインスタンスとオーサーインスタンスの URL を指定します。単一の AEM オーサーインスタンスを実行している場合、local プロパティと author プロパティの値は同じになります。publish には、パブリッシュインスタンスの URL を指定します。

1. **[!UICONTROL リンク共有]**&#x200B;ダイアログの電子メールアドレスボックスに、リンクを共有するユーザーの電子メール ID を入力します。このリンクを複数のユーザーと共有することもできます。

   ユーザーが組織内のメンバーの場合は、入力領域の下のリストに表示される電子メール ID の候補から、ユーザーの電子メール ID を選択します。外部ユーザーの場合は、完全な電子メール ID を入力してリストから選択します。

   ユーザーへの電子メールの送信を有効にするには、[Day CQ Mail Service](#configmailservice) で SMTP サーバーの詳細を設定します。

   ![アセットへのリンクをリンク共有ダイアログから直接共有する](assets/Asset-Sharing-LinkShareDialog.png)

   アセットへのリンクをリンク共有ダイアログから直接共有する

   >[!NOTE]
   組織内のメンバーではないユーザーの電子メール ID を入力した場合、ユーザーの電子メール ID に「外部ユーザー」というプレフィックスが付けられます。

1. 「**[!UICONTROL 件名]**」ボックスに、共有するアセットの件名を入力します。
1. 「**[!UICONTROL メッセージ]**」ボックスに、オプションでメッセージを入力します。
1. 「**[!UICONTROL 有効期限]**」フィールドに、日付選択を使用してリンクの有効期限の日付と時間を指定します。デフォルトでは、有効期限日はリンクを共有した日から 1 週間後に設定されます。

   ![共有リンクの有効期限の設定](assets/Set-shared-link-expiration.png)

1. ユーザーが元の画像をレンディションと共にダウンロードすることを許可するには、「**[!UICONTROL 元のファイルのダウンロードを許可]**」を選択します。

   >[!NOTE]
   デフォルトでは、ユーザーはリンクとして共有されているアセットのレンディションのみをダウンロードできます。

1. 「**[!UICONTROL 共有]**」をクリックします。リンクが電子メールでユーザーと共有されていることを確認するメッセージが表示されます。
1. 共有アセットを表示するには、ユーザーに送信された電子メールのリンクをクリックまたはタップします。共有アセットが **[!UICONTROL Adobe Marketing Cloud]** ページに表示されます。

   ![chlimage_1-260](assets/chlimage_1-545.png)

   リスト表示に切り替えるには、ツールバーのレイアウトオプションをクリックまたはタップします。

1. アセットのプレビューを生成するには、共有アセットをクリックまたはタップします。プレビューを閉じて **[!UICONTROL Experience Cloud]** ページに戻るには、ツールバーの「**[!UICONTROL 戻る]**」をクリックまたはタップします。フォルダーを共有している場合は、「**[!UICONTROL 親フォルダー]**」をクリックまたはタップして親フォルダーに戻ります。

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   AEM は、これらの MIME タイプ（JPG、PNG、GIF、BMP、INDD、PDF、および PPT）のアセットのプレビューの生成をサポートしています。他の MIME タイプのアセットのみをダウンロードできます。

1. To download the shared asset, tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. リンクとして共有したアセットを表示するには、Assets UIに移動し、Experience Managerのロゴをタップします。 Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. ナビゲーションウィンドウで、「**[!UICONTROL 共有リンク]**」を選択して共有アセットのリストを表示します。
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar. 確認メッセージが次に表示されます。 アセットのエントリがリストから削除されます。

## Day CQ 電子メールサービスの設定 {#configmailservice}

1. Experience Managerのホームページで、ツール/操作/ **** Webコンソールに移動し **[!UICONTROL ます]******。
1. サービスのリストから、**[!UICONTROL Day CQ Mail Service]** を探します。
1. Tap **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * SMTP server host name：電子メールサーバーのホスト名
   * SMTP server port：電子メールサーバーのポート
   * SMTP user：メールサーバーのユーザー名
   * SMTP password：電子メールサーバーのパスワード
   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 「**[!UICONTROL 保存]**」をクリックまたはタップします。

## 最大データサイズの設定 {#maxdatasize}

リンク共有機能を使用して共有されているリンクからアセットをダウンロードすると、AEM は、リポジトリのアセットの階層を圧縮して、ZIP ファイルにしてアセットを返します。ただし、ZIP ファイルとして圧縮できるデータ量に制限がないと、膨大なデータが圧縮の対象となり、JVM のメモリ不足エラーの原因となります。To secure the system from a potential denial of service attack due to this situation, configure the maximum size using the **[!UICONTROL Max Content Size (uncompressed)]** parameter for [!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet] in Configuration Manager. アセットの未圧縮時のサイズが設定値を超えていると、アセットのダウンロード要求は拒否されます。デフォルト値は 100 MB です。

1. AEM のロゴをクリックまたはタップし、**[!UICONTROL ツール]**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;に移動します。
1. From the Web Console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. 「**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**」設定を編集モードで開き、「**[!UICONTROL 最大コンテンツサイズ（非圧縮）]**」パラメーターの値を変更します。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 変更内容を保存します。

## ベストプラクティスとトラブルシューティング {#bestpractices}

* 名前に空白を含むアセットフォルダーまたはコレクションは共有されない場合があります。
* ユーザーが共有アセットをダウンロードできない場合は、AEM 管理者に[ダウンロード制限](#maxdatasize)を確認してください。
* 共有アセットへのリンクを含むメールを送信できない場合、または他のユーザーがお客様からのメールを受信できない場合、AEM 管理者に[メールサービス](#configmailservice)が構成されているかどうかを確認してください。
* リンク共有機能を使用してアセットを共有できない場合は、適切な権限を持っていることを確認してください。[アセットの共有](#sharelink)を参照してください。
