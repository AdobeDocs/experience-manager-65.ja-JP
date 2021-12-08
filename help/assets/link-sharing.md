---
title: リンクを使用したアセットの共有
description: アセット、フォルダー、コレクションを URL として共有します。
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
source-git-commit: fb9de8a0303edd7e54639f7bb9c8a4f8e9227fa8
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 30%

---

# アセットをリンクとして共有 {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] では、アセット、フォルダー、コレクションを URL として組織のメンバーや外部（パートナーやベンダーを含む）と共有できます。 リンクを通じたアセットの共有は、外部の関係者がにログインしなくてもリソースを利用できる便利な方法です。 [!DNL Assets].

>[!PREREQUISITES]
>
>* 必要な項目 `Edit ACL` リンクとして共有するフォルダーまたはアセットに対する権限。
>* ユーザーに電子メールを送信するには、で SMTP サーバーの詳細を設定します。 [Day CQ Mail Service](#configmailservice).


## アセットの共有 {#share-assets}

ユーザーと共有するアセットの URL を生成するには、 [!UICONTROL リンク共有] ダイアログ。

* 管理者権限を持つユーザー、またはでの読み取り権限を持つユーザー `/var/dam/share` 場所には、共有されたリンクが表示されます。
* に読み取り権限を持つユーザー `/var/dam/jobs/download` の場所では、共有リンクからアセットをダウンロードできます。

1. [!DNL Assets] のユーザーインターフェイスで、リンクとして共有するアセットを選択します。

1. ツールバーの **[!UICONTROL リンクを共有]** ![アセットを共有アイコン](assets/do-not-localize/assets_share.png). クリックした後に作成されるリンク **[!UICONTROL 共有]** は、事前に [!UICONTROL リンクを共有] フィールドに入力します。 リンクは、 **[!UICONTROL 送信]**.

   ![「リンクを共有」と表示されたダイアログ](assets/share-assets-as-link.png)

   *図：アセットをリンクとして共有するためのダイアログ。*

1. **[!UICONTROL リンク共有]**&#x200B;ダイアログの電子メールアドレスボックスに、リンクを共有するユーザーの電子メール ID を入力します。1 人または複数のユーザーを追加できます。

   >[!NOTE]
   >
   >組織のメンバーでないユーザーの電子メール ID を入力すると、 [!UICONTROL 外部ユーザー] には、ユーザーの電子メール ID のプレフィックスが付きます。

1. 「**[!UICONTROL 件名]**」ボックスに、共有するアセットの件名を入力します。

1. 「**[!UICONTROL メッセージ]**」ボックスに、オプションでメッセージを入力します。

1. 内 **[!UICONTROL 有効期限]** 「 」フィールドで、リンクが機能を停止する日時を指定します。 リンクのデフォルトの有効期間は 1 日です。

   ![共有リンクの有効期限を設定](assets/Set-shared-link-expiration.png)

1. 元のアセットをユーザーがダウンロードできるようにするには、「 **[!UICONTROL 元のファイルのダウンロードを許可]**. ユーザーが共有アセットのレンディションのみをダウンロードできるようにするには、 **[!UICONTROL ファイルのレンディションのダウンロードを許可]**.

1. 「**[!UICONTROL 共有]**」をクリックします。リンクが電子メールでユーザーと共有されることを確認するメッセージが表示されます。

1. 共有アセットを表示するには、ユーザーに送信された電子メールに記載されているリンクをクリックします。 アセットのプレビューを生成するには、共有アセットをクリックします。 プレビューを閉じるには、 **[!UICONTROL 戻る]**. フォルダーを共有している場合は、 **[!UICONTROL 親フォルダー]** をクリックして親フォルダーに戻ります。

   ![共有アセットのプレビュー](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] は、次のアセットのプレビューの生成のみをサポートしています： [サポートされているファイルタイプ](/help/assets/assets-formats.md). 他の MIME タイプが共有されている場合は、アセットのダウンロードのみ可能で、プレビューはできません。

1. 共有アセットをダウンロードするには、 **[!UICONTROL 選択]** ツールバーでアセットをクリックし、 **[!UICONTROL ダウンロード]** をクリックします。

   ![共有アセットをダウンロードするためのツールバーオプション](assets/chlimage_1-547.png)

1. リンクとして共有したアセットを表示するには、 [!DNL Assets] ユーザーインターフェイスで [!DNL Experience Manager] ロゴ 選択 **[!UICONTROL ナビゲーション]**. ナビゲーションウィンドウで、「 」を選択します。 **[!UICONTROL 共有リンク]** 共有アセットのリストを表示する。

1. アセットの共有を解除するには、アセットを選択して、 **[!UICONTROL 共有しない]** をクリックします。 確認メッセージが表示されます。 そのアセットのエントリがリストから削除されます。

## Day CQ Mail Service の設定 {#configure-day-cq-mail-service}

1. の [!DNL Experience Manager] ホームページ、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL Web コンソール]**.
1. サービスのリストから、**[!UICONTROL Day CQ Mail Service]** を探します。
1. クリック **[!UICONTROL 編集]** を選択し、 **[!UICONTROL Day CQ Mail Service]** 彼らの名前に関して詳しく述べた

   * SMTP server host name：電子メールサーバーのホスト名
   * SMTP server port：電子メールサーバーのポート
   * SMTP user：メールサーバーのユーザー名
   * SMTP password：電子メールサーバーのパスワード

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

## 最大データサイズの設定 {#configure-maximum-data-size}

リンク共有機能を使用して共有されたリンクからアセットをダウンロードする場合、 [!DNL Experience Manager] はリポジトリーからのアセット階層を圧縮し、アセットを ZIP ファイルで返します。 ただし、ZIP ファイルとして圧縮できるデータ量に制限がないと、膨大なデータが圧縮の対象となり、JVM のメモリ不足エラーの原因となります。この状況による潜在的な DoS 攻撃からシステムを保護するには、Configuration Manager で Day CQ DAM Adhoc Asset Share Proxy Servlet の「**[!UICONTROL Max Content Size (uncompressed)]**」パラメーターを使用して、最大サイズを設定します。****&#x200B;アセットの未圧縮時のサイズが設定値を超えていると、アセットのダウンロード要求は拒否されます。デフォルト値は 100 MB です。

1. 次をクリック： [!DNL Experience Manager] ロゴをクリックし、次ににに移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL Web コンソール]**.
1. Web コンソールで、 **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** 設定。
1. 「**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**」設定を編集モードで開き、「**[!UICONTROL Max Content Size (uncompressed)]**」パラメーターの値を変更します。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 変更内容を保存します。

## ベストプラクティスとトラブルシューティング {#best-practices-and-troubleshooting}

* 名前に空白を含むアセットフォルダーまたはコレクションは共有されない場合があります。
* ユーザーが共有アセットをダウンロードできない場合は、 [!DNL Experience Manager] 管理者 [ダウンロード制限](#configure-maximum-data-size) はです。
* 共有アセットへのリンクを含む電子メールを送信できない場合や、他のユーザーが電子メールを受信できない場合は、 [!DNL Experience Manager] 管理者 ( [電子メールサービス](#configure-day-cq-mail-service) が設定されているかどうか。
* リンク共有機能を使用してアセットを共有できない場合は、適切な権限を持っていることを確認してください。[アセットの共有](#share-assets)を参照してください。
* 共有アセットが別の場所に移動されると、そのリンクは機能しなくなります。リンクを再作成し、ユーザーと再共有します。

* リンクを [!DNL Experience Manager] 外部エンティティへのオーサーのデプロイメント。次のリンク共有に使用される URL のみを公開するようにしてください。 `GET` リクエストのみ。 セキュリティ上の理由から、他の URL をブロックします。

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`
   In [!DNL Experience Manager] インターフェイス、アクセス **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL Web コンソール]**. を開きます。 **[!UICONTROL Day CQ Link Externalizer]** を設定し、 **[!UICONTROL ドメイン]** 値が記載されたフィールド `local`, `author`、および `publish`. の `local` および `author` プロパティには、それぞれローカルインスタンスとオーサーインスタンスの URL を指定します。 1 つの [!DNL Experience Manager] オーサーインスタンス、同じ値を次に使用： `local` および `author` プロパティ。 パブリッシュインスタンスの場合は、 [!DNL Experience Manager] パブリッシュインスタンス。
