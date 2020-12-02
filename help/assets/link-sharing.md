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


# リンク{#asset-link-sharing}を介してアセットを共有

[!DNL Adobe Experience Manager Assets] アセット、フォルダー、コレクションをURLとして組織のメンバーと、パートナーやベンダーを含む外部エンティティと共有できます。リンクを通じてアセットを共有すると、[!DNL Assets]に最初にログインしなくても、外部のユーザーがリソースを利用できる便利な方法です。

>[!PREREQUISITES]
>
>* リンクとして共有するフォルダーまたはアセットのACLを編集権限が必要です。
>* ユーザーに電子メールを送信するには、[Day CQ Mail Service](#configmailservice)でSMTPサーバーの詳細を設定します。


## アセットの共有 {#sharelink}

ユーザーと共有するアセットのURLを生成するには、リンクの共有ダイアログを使用します。 `/var/dam/share` の場所への管理者特権または読み取り権限を持つユーザーが、共有されたリンクを表示することができます。

1. [!DNL Assets]ユーザーインターフェイスで、リンクとして共有するアセットを選択します。
1. ツールバーで、**[!UICONTROL リンクを共有]** ![アセットを共有アイコン](assets/do-not-localize/assets_share.png)をクリックします。

   「[!UICONTROL 共有]」をクリックした後に作成されるリンクは、あらかじめ「[!UICONTROL 共有リンク]」フィールドに表示されます。 リンクのデフォルトの有効期間は 1 日です。

   ![「リンクを共有」と表示されたダイアログ](assets/Link-sharing-dialog-box.png)

   *図：アセットをリンクとして共有するためのダイアログ。*

   >[!NOTE]
   >
   >[!DNL Experience Manager]作成者デプロイメントから外部エンティティにリンクを共有する場合は、`GET`リクエストのみに次のURL（リンク共有に使用）のみを公開するようにします。 セキュリティ上の理由から他のURLをブロックします。
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]**/**[!UICONTROL 操作]**/**[!UICONTROL Webコンソール]**&#x200B;にアクセスします。

1. **[!UICONTROL Day CQ Link Externalizer]**&#x200B;の設定を開き、**[!UICONTROL Domains]**&#x200B;フィールドの次のプロパティを変更して、`local`、`author`および`publish`に関する値を入力します。 `local`プロパティと`author`プロパティには、それぞれローカルインスタンスとオーサーインスタンスのURLを指定します。 1つの[!DNL Experience Manager]作成者インスタンスを実行する場合、`local`プロパティと`author`プロパティの両方が同じ値を持ちます。 発行インスタンスの場合、[!DNL Experience Manager]発行インスタンスのURLを指定します。

1. **[!UICONTROL リンク共有]**&#x200B;ダイアログの電子メールアドレスボックスに、リンクを共有するユーザーの電子メール ID を入力します。1人以上のユーザーを追加できます。

   ![アセットへのリンクをリンク共有ダイアログから直接共有する](assets/Asset-Sharing-LinkShareDialog.png)

   *図：リンクの共有ダイアログからアセットへのリンクを直接 [!UICONTROL 共有] します。*

   >[!NOTE]
   >
   >組織のメンバーでないユーザーの電子メールIDを入力すると、[!UICONTROL External User]という語の前に、ユーザーの電子メールIDが付加されます。

1. 「**[!UICONTROL 件名]**」フィールドに件名を入力します。

1. 「**[!UICONTROL メッセージ]**」フィールドに、オプションのメッセージを入力します。

1. 「**[!UICONTROL 有効期限]**」フィールドに、リンクの動作を停止する有効期限の日時を指定します。 デフォルトでは、有効期限日はリンクを共有した日から 1 週間後に設定されます。

   ![共有リンクの有効期限の設定](assets/Set-shared-link-expiration.png)

1. ユーザーがレンディションと共に元のアセットをダウンロードできるようにするには、「**[!UICONTROL 元のファイルのダウンロードを許可]**」を選択します。 デフォルトでは、ユーザーはリンクとして共有されているアセットのレンディションのみをダウンロードできます。

1. 「**[!UICONTROL 共有]**」をクリックします。リンクが電子メールでユーザーと共有されていることを確認するメッセージが表示されます。

1. 共有アセットを表示するには、ユーザーに送信する電子メール内のリンクをクリックします。 共有アセットが **[!UICONTROL Adobe Marketing Cloud]** ページに表示されます。

   ![chlimage_1-260](assets/chlimage_1-545.png)

1. アセットのプレビューを生成するには、共有アセットをクリックします。 プレビューを閉じてMarketing Cloud ]**ページに戻るには、ツールバーの**[!UICONTROL &#x200B;戻る&#x200B;]**をクリックします。**[!UICONTROL &#x200B;フォルダーを共有している場合は、「**[!UICONTROL 親フォルダー]**」をクリックして親フォルダーに戻ります。

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] は、サポートされているファイルタイプのみのアセット [のプレビューの生成をサポートしています](/help/assets/assets-formats.md)。他のMIMEタイプが共有されている場合は、アセットのダウンロードのみが可能で、プレビューはできません。

1. 共有アセットをダウンロードするには、ツールバーの「**[!UICONTROL 選択]**」をクリックし、アセットをクリックしてから、ツールバーの「**[!UICONTROL ダウンロード]**」をクリックします。

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. リンクとして共有したアセットを表示するには、[!DNL Assets]ユーザーインターフェイスに移動し、[!DNL Experience Manager]ロゴをクリックします。 **[!UICONTROL ナビゲーション]**&#x200B;を選択します。 ナビゲーションペインで、「**[!UICONTROL 共有リンク]**」を選択して、共有アセットのリストを表示します。

1. アセットの共有を解除するには、アセットを選択し、ツールバーの「**[!UICONTROL 共有解除]**」をクリックします。 確認メッセージが次に表示されます。 アセットのエントリがリストから削除されます。

## Day CQ 電子メールサービスの設定 {#configmailservice}

1. [!DNL Experience Manager]ホームページで、**[!UICONTROL ツール]** > **[!UICONTROL 操作]** > **[!UICONTROL Webコンソール]**&#x200B;に移動します。
1. サービスのリストから、**[!UICONTROL Day CQ Mail Service]** を探します。
1. サービスの横にある「**[!UICONTROL 編集]**」をクリックし、**[!UICONTROL Day CQ Mail Service]**&#x200B;の次のパラメーターを設定し、名前に記載されている詳細を入力します。

   * SMTP server host name：電子メールサーバーのホスト名
   * SMTP server port：電子メールサーバーのポート
   * SMTP user：メールサーバーのユーザー名
   * SMTP password：電子メールサーバーのパスワード

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

## 最大データサイズの設定 {#maxdatasize}

リンク共有機能を使用して共有されたリンクからアセットをダウンロードすると、[!DNL Experience Manager]はリポジトリからアセット階層を圧縮し、ZIPファイルに戻します。 ただし、ZIP ファイルとして圧縮できるデータ量に制限がないと、膨大なデータが圧縮の対象となり、JVM のメモリ不足エラーの原因となります。この状況による潜在的な DoS 攻撃からシステムを保護するには、Configuration Manager で Day CQ DAM Adhoc Asset Share Proxy Servlet の「**[!UICONTROL Max Content Size (uncompressed)]**」パラメーターを使用して、最大サイズを設定します。アセットの未圧縮時のサイズが設定値を超えていると、アセットのダウンロード要求は拒否されます。デフォルト値は 100 MB です。

1. [!DNL Experience Manager]ロゴをクリックし、**[!UICONTROL ツール]**/**[!UICONTROL 操作]**/**[!UICONTROL Webコンソール]**&#x200B;に移動します。
1. Webコンソールから、**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**&#x200B;設定を探します。
1. 「**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**」設定を編集モードで開き、「**[!UICONTROL Max Content Size (uncompressed)]**」パラメーターの値を変更します。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 変更内容を保存します。

## ベストプラクティスとトラブルシューティング {#bestpractices}

* 名前に空白を含むアセットフォルダーまたはコレクションは共有されない場合があります。
* ユーザーが共有アセットをダウンロードできない場合は、[!DNL Experience Manager]管理者に、[ダウンロードの制限](#maxdatasize)が何であるかを確認してください。
* 共有アセットへのリンクを含む電子メールを送信できない場合、または他のユーザーが電子メールを受信できない場合は、[電子メールサービス](#configmailservice)が設定されているかどうかを[!DNL Experience Manager]管理者に問い合わせてください。
* リンク共有機能を使用してアセットを共有できない場合は、適切な権限を持っていることを確認してください。[アセットの共有](#sharelink)を参照してください。
* 共有アセットが別の場所に移動されると、そのリンクは機能しなくなります。リンクを再作成し、ユーザーと再共有します。
