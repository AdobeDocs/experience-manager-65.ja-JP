---
title: リンクを使用したアセットの共有
description: アセット、フォルダー、コレクションをURLとして共有します。
contentOwner: AG
role: Business Practitioner
feature: リンク共有，アセット管理
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
source-git-commit: 3ec39279d001297dcc11ebd1110bb452de8ca980
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 36%

---

# リンク{#asset-link-sharing}を介したアセットの共有

[!DNL Adobe Experience Manager Assets] では、アセット、フォルダー、コレクションをURLとして組織のメンバーや外部（パートナーやベンダーを含む）と共有できます。リンクによるアセットの共有は、外部の関係者が [!DNL Assets] にログインすることなくリソースを利用するための便利な方法です。

>[!PREREQUISITES]
>
>* リンクとして共有するフォルダーまたはアセットに対する編集ACL権限が必要です。
>* ユーザーに電子メールを送信するには、[Day CQ Mail Service](#configmailservice)でSMTPサーバーの詳細を設定します。


## アセットの共有 {#share-assets}

ユーザーと共有するアセットのURLを生成するには、リンク共有ダイアログを使用します。 `/var/dam/share` の場所への管理者特権または読み取り権限を持つユーザーが、共有されたリンクを表示することができます。

1. [!DNL Assets] のユーザーインターフェイスで、リンクとして共有するアセットを選択します。
1. ツールバーの「**[!UICONTROL リンクを共有]** ![アセットを共有アイコン](assets/do-not-localize/assets_share.png) 」をクリックします。 「**[!UICONTROL 共有]**」をクリックした後に作成されるリンクが、「[!UICONTROL リンクを共有]」フィールドにあらかじめ表示されます。 「**[!UICONTROL 送信]**」をクリックするまで、リンクはまだ作成されません。

   ![「リンクを共有」と表示されたダイアログ](assets/Link-sharing-dialog-box.png)

   *図：アセットをリンクとして共有するためのダイアログ。*

1. **[!UICONTROL リンク共有]**&#x200B;ダイアログの電子メールアドレスボックスに、リンクを共有するユーザーの電子メール ID を入力します。1人以上のユーザーを追加できます。

   ![アセットへのリンクをリンク共有ダイアログから直接共有する](assets/Asset-Sharing-LinkShareDialog.png)

   *図：リンク共有ダイアログから直接アセットへのリ [!UICONTROL ンクを] 共有します。*

   >[!NOTE]
   >
   >組織のメンバーでないユーザーの電子メールIDを入力する場合、「[!UICONTROL External User]」という語には、ユーザーの電子メールIDがプレフィックスとして付加されます。

1. 「**[!UICONTROL 件名]**」ボックスに、共有するアセットの件名を入力します。

1. 「**[!UICONTROL メッセージ]**」ボックスに、オプションでメッセージを入力します。

1. 「**[!UICONTROL 有効期限]**」フィールドに、リンクの動作を停止する有効期限の日時を指定します。 リンクのデフォルトの有効期間は 1 日です。

   ![共有リンクの有効期限の設定](assets/Set-shared-link-expiration.png)

1. ユーザーがレンディションと共に元のアセットをダウンロードできるようにするには、「**[!UICONTROL 元のファイルのダウンロードを許可]**」を選択します。 デフォルトでは、ユーザーはリンクとして共有されているアセットのレンディションのみをダウンロードできます。

1. 「**[!UICONTROL 共有]**」をクリックします。リンクが電子メールでユーザーと共有されることを確認するメッセージが表示されます。

1. 共有アセットを表示するには、ユーザーに送信された電子メールのリンクをクリックします。 アセットのプレビューを生成するには、共有アセットをクリックします。 プレビューを閉じるには、「**[!UICONTROL 戻る]**」をクリックします。 フォルダーを共有している場合、「**[!UICONTROL 親フォルダー]**」をクリックして親フォルダーに戻ります。

   ![共有アセットのプレビュー](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] では、サポートされているファイルタイプのアセットのプ [レビューの生成のみサポートしています](/help/assets/assets-formats.md)。他のMIMEタイプが共有されている場合は、アセットのダウンロードのみが可能で、プレビューはできません。

1. 共有アセットをダウンロードするには、ツールバーの「**[!UICONTROL 選択]**」をクリックし、アセットをクリックして、ツールバーの「**[!UICONTROL ダウンロード]**」をクリックします。

   ![共有アセットをダウンロードするツールバーオプション](assets/chlimage_1-547.png)

1. リンクとして共有したアセットを表示するには、[!DNL Assets]ユーザーインターフェイスに移動し、[!DNL Experience Manager]ロゴをクリックします。 **[!UICONTROL ナビゲーション]**&#x200B;を選択します。 ナビゲーションウィンドウで、「**[!UICONTROL 共有リンク]**」を選択して共有アセットのリストを表示します。

1. アセットの共有を解除するには、アセットを選択し、ツールバーの「**[!UICONTROL 共有しない]**」をクリックします。 確認メッセージが表示されます。 アセットのエントリがリストから削除されます。

## Day CQ Mail Service の設定 {#configure-day-cq-mail-service}

1. [!DNL Experience Manager]ホームページで、**[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソール]**&#x200B;に移動します。
1. サービスのリストから、**[!UICONTROL Day CQ Mail Service]** を探します。
1. サービスの横にある「**[!UICONTROL 編集]**」をクリックし、**[!UICONTROL Day CQ Mail Service]**&#x200B;の次のパラメーターを設定します。詳細は、名前に基づいて示されます。

   * SMTP server host name：電子メールサーバーのホスト名
   * SMTP server port：電子メールサーバーのポート
   * SMTP user：メールサーバーのユーザー名
   * SMTP password：電子メールサーバーのパスワード

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

## 最大データサイズの設定 {#configure-maximum-data-size}

リンク共有機能を使用して共有されたリンクからアセットをダウンロードすると、[!DNL Experience Manager]はリポジトリーのアセット階層を圧縮し、ZIPファイルでアセットを返します。 ただし、ZIP ファイルとして圧縮できるデータ量に制限がないと、膨大なデータが圧縮の対象となり、JVM のメモリ不足エラーの原因となります。この状況による潜在的な DoS 攻撃からシステムを保護するには、Configuration Manager で Day CQ DAM Adhoc Asset Share Proxy Servlet の「**[!UICONTROL Max Content Size (uncompressed)]**」パラメーターを使用して、最大サイズを設定します。****&#x200B;アセットの未圧縮時のサイズが設定値を超えていると、アセットのダウンロード要求は拒否されます。デフォルト値は 100 MB です。

1. [!DNL Experience Manager]ロゴをクリックし、**[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソール]**&#x200B;に移動します。
1. Webコンソールで、「**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**」設定を探します。
1. 「**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**」設定を編集モードで開き、「**[!UICONTROL Max Content Size (uncompressed)]**」パラメーターの値を変更します。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 変更内容を保存します。

## ベストプラクティスとトラブルシューティング {#best-practices-and-troubleshooting}

* 名前に空白を含むアセットフォルダーまたはコレクションは共有されない場合があります。
* ユーザーが共有アセットをダウンロードできない場合は、[ダウンロード制限](#configure-maximum-data-size)を[!DNL Experience Manager]管理者に確認してください。
* 共有アセットへのリンクを含む電子メールを送信できない場合や、他のユーザーが電子メールを受信できない場合は、[電子メールサービス](#configure-day-cq-mail-service)が設定されているかどうかを[!DNL Experience Manager]管理者に確認してください。
* リンク共有機能を使用してアセットを共有できない場合は、適切な権限を持っていることを確認してください。[アセットの共有](#share-assets)を参照してください。
* 共有アセットが別の場所に移動されると、そのリンクは機能しなくなります。リンクを再作成し、ユーザーと再共有します。

* [!DNL Experience Manager]オーサーのデプロイメントから外部エンティティにリンクを共有する場合は、`GET`リクエストに対してのみ、リンク共有に使用される次のURLのみを公開するようにします。 セキュリティ上の理由から、他のURLをブロックします。

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`
   [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソール]**&#x200B;にアクセスします。 **[!UICONTROL Day CQ Link Externalizer]**&#x200B;設定を開き、**[!UICONTROL Domains]**&#x200B;フィールドの次のプロパティの値を`local`、`author`および`publish`に変更します。 `local`プロパティと`author`プロパティに、それぞれローカルインスタンスとオーサーインスタンスのURLを指定します。 1つの[!DNL Experience Manager]オーサーインスタンスを実行する場合、`local`と`author`のプロパティに同じ値を使用します。 パブリッシュインスタンスの場合は、 [!DNL Experience Manager]パブリッシュインスタンスのURLを指定します。
