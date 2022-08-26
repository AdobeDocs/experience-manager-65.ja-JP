---
title: Adobe Sign の AEM Forms への統合
seo-title: Integrate Adobe Sign with AEM Forms
description: AEM Forms 用に Adobe Sign を設定する方法
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Adobe Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: e46d77caf831324f077315df43b8f3a0267bef9a
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 92%

---

# [!DNL Adobe Sign] の AEM [!DNL Forms] との統合{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] により、アダプティブフォームの電子サインワークフローを有効にできます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

[!DNL Adobe Sign] とアダプティブフォームの一般的なシナリオでは、ユーザーがアダプティブフォームに入力して&#x200B;**サービスを申し込みます**。例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームの入力、送信、署名を行うと、サービスプロバイダーにそのフォームが送信され、追加の処理が実行されます。サービスプロバイダーは受信した申込フォームを確認し、[!DNL Adobe Sign] を使用して申請を承認します。これに類似した電子サインワークフローを有効にするには、[!DNL Adobe Sign] を AEM [!DNL Forms] に統合します。

AEM [!DNL Forms] で [!DNL Adobe Sign] を使用するには、AEM Cloud Services で [!DNL Adobe Sign] を設定します。

## 前提条件 {#prerequisites}

[!DNL Adobe Sign] を AEM [!DNL Forms] に統合するには、以下のものが必要になります。

* 有効な [Adobe Sign 開発者アカウント](https://acrobat.adobe.com/jp/ja/why-adobe/developer-form.html)
* [SSL が有効になっている](/help/sites-administering/ssl-by-default.md) AEM サーバー[!DNL Forms]
* [Adobe Sign API アプリケーション](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* [!DNL Adobe Sign] API アプリケーションの資格情報（クライアント ID およびクライアントの秘密鍵）。
* 再構成時に、作成インスタンスと公開インスタンスの両方から既存の [!DNL Adobe Sign] 構成を削除します。
* オーサーインスタンスとパブリッシュインスタンスには、[同一の暗号キー](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)を使用します。

## AEM [!DNL Forms] を使用して [!DNL Adobe Sign] を設定する {#configure-adobe-sign-with-aem-forms}

上記の前提条件の準備が完了したら、以下の手順により、オーサーインスタンス上の AEM [!DNL Forms] を使用して [!DNL Adobe Sign] を設定します。

1. AEM [!DNL Forms] のオーサーインスタンスで、**ツール** ![ハンマー](assets/hammer.png)／**[!UICONTROL 一般]**／**[!UICONTROL 設定ブラウザー]**&#x200B;に移動します。
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで「**[!UICONTROL 作成]**」をタップします。
   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、「**[!UICONTROL クラウド設定]**」を有効にして「**[!UICONTROL 作成]**」をタップします。これにより、Cloud Services 用の設定コンテナが作成されます。
1. **ツール** ![ハンマー](assets/hammer.png)／**[!UICONTROL Cloud Services]**／**[!UICONTROL Adobe Sign]** に移動し、上記の手順で作成した設定コンテナを選択します。

   >[!NOTE]
   >
   >手順1〜4を実行して、新しい構成コンテナを作成し、コンテナで [!DNL Adobe Sign] 構成を作成するか、**ツール** ![ハンマー](assets/hammer.png)／**[!UICONTROL Cloud Services]**／**[!UICONTROL Adobe Sign]**&#x200B;で既存の `global` フォルダーを使用できます。新しい設定コンテナで設定を作成する場合、必ず&#x200B;**[!UICONTROL 設定コンテナ]**&#x200B;フィールドに値を入力する必要があります。

   >[!NOTE]
   Cloud Services 設定ページの URL が「**HTTPS**」で始まっていることを確認してください。「HTTPS」で始まっていない場合は、AEM [!DNL Forms] サーバーで [SSL を有効](/help/sites-administering/ssl-by-default.md)にしてください。

1. 設定ページで「**[!UICONTROL 作成]**」をタップして、AEM [!DNL Forms] 内に [!DNL Adobe Sign] の設定を作成します。
1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページの「**[!UICONTROL 一般]**」タブで、設定の&#x200B;**[!UICONTROL 名前]**&#x200B;を指定して「**[!UICONTROL 次へ]**」をタップします。必要に応じてタイトルを指定し、設定のサムネールを参照して選択することもできます。

1. 現在のブラウザーウィンドウの URL をメモ帳にコピーします。この URL は、AEM [!DNL Forms] で [!DNL Adobe Sign] アプリケーションを設定する際に必要になります。

1. 内 **[!UICONTROL 設定]** タブ、 **[!UICONTROL OAuth URL]** フィールドにはデフォルトの URL が含まれます。 URL の形式は次の通りです。

   `https://<shard>/public/oAuth/v2`

   次に例を示します。
   `https://secure.na1.echosign.com/public/oauth/v2`

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。データベースシャードの値を更新することができます。[!DNL  Adobe Sign] クラウド設定で、[正しいシャード](https://helpx.adobe.com/jp/sign/using/identify-account-shard.html)をポイントしていることを確認します。

   別の [!DNL Adobe Sign] 設定を Adobe Experience Manager の機能またはコンポーネント用に作成する場合は、すべての [!DNL Adobe Sign] クラウド設定が同じシャードをポイントしていることを確認してください。

   >[!NOTE]
   キープ **Adobe Sign設定を作成** ページが開きます。 閉じないでください。 次を検索： **クライアント ID** および **クライアント秘密鍵** 次の項目の OAuth 設定を行った後 [!DNL Adobe Sign] 今後の手順で説明するアプリケーション


1. 以下の手順に従って、[!DNL Adobe Sign] アプリケーションの OAuth 設定を指定します。

   1. ブラウザーウィンドウを開き、[!DNL Adobe Sign] 開発者アカウントにサインインします。
   1. AEM [!DNL Forms] 用に設定されているアプリケーションを選択し、「**[!UICONTROL アプリケーションの OAuth を設定]**」をタップします。
   1. **[!UICONTROL クライアント ID]** および&#x200B;**[!UICONTROL クライアント秘密鍵]**&#x200B;をメモ帳に追加します。
   1. 上記の手順でコピーした HTTPS URL を「**[!UICONTROL リダイレクト URL]**」ボックスに追加します。
   1. [!DNL Adobe Sign] アプリケーションに対して以下の OAuth 設定を有効にして、「**[!UICONTROL 保存]**」をクリックします。
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   [!DNL Adobe Sign] アプリケーション用に OAuth 設定を構成してキーを取得するための詳しい手順については、開発者用ドキュメントの[アプリケーション用に OAuth 設定を構成する](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)を参照してください。

   ![OAuth 設定](assets/oauthconfig_new.png)

1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページに戻ります。「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL OAuth URL]**」フィールドに以下のデフォルトの URL が表示されます。URL の形式は次の通りです。

   `https://<shard>/public/oAuth/v2`

   次に例を示します。
   `https://secure.na1.echosign.com/public/oauth/v2`

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。

   データベースシャードの値を更新することができます。サーバーを再起動すると、データベースシャードの新しい値を使用することができます。

   >[!NOTE]
   オーサーインスタンスとパブリッシュインスタンスの設定が同じシャードを指していることを確認します。1 つの組織に対して複数の Adobe Sign 設定を作成する場合は、すべての設定で同じシャードが使用されていることを確認します。

1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページに戻ります。内 **[!UICONTROL 設定]** タブで、 **クライアント ID** （アプリケーション ID とも呼ばれます）および **クライアント秘密鍵**. 以下を使用： [Adobe Signアプリケーションのクライアント ID およびクライアント秘密鍵](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) AEM Forms用に作成されました。

1. 「**[!UICONTROL 添付ファイルにも Adobe Sign を有効にする]**」オプションを選択すると、アダプティブフォームに添付されているファイルが、署名用に送信された対応する [!DNL Adobe Sign] ドキュメントに添付されます。

1. 「**[!UICONTROL Adobe Sign に接続]**」をタップします。資格情報の入力画面が表示されたら、[!DNL Adobe Sign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。

1. 「**[!UICONTROL 作成]**」をタップして、[!DNL Adobe Sign] 設定を作成します。

1. AEM web コンソールを開きます。URL は `https://'[server]:[port]'/system/console/configMgr` です。
1. **[!UICONTROL Forms 共通設定サービス]を開きます。**
1. 「**[!UICONTROL 許可]**」フィールドで、「すべてのユーザー - すべてのユーザーに（匿名かログインしているかによらず）添付ファイルのプレビューとフォームの検証と署名を許可」を&#x200B;**選択**&#x200B;して「**[!UICONTROL 保存]」をクリックします。**&#x200B;オーサーインスタンスが [!DNL Adobe Sign] を使用するように設定されます。
1. 設定を公開します。
1. [レプリケーション](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=ja)を使用して、対応する公開インスタンスに同一の構成を作成します。

これで [!DNL Adobe Sign] が AEM [!DNL Forms] に統合され、アダプティブフォームで使用できるようになりました。[アダプティブフォームで Adobe Sign サービスを使用する](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)には、上記のとおりアダプティブフォームのプロパティで作成した設定コンテナを指定します。



## [!DNL Adobe Sign] スケジューラーを設定して署名ステータスを同期する {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

[!DNL Adobe Sign] が有効になっているアダプティブフォームは、すべての署名者がフォームに署名するまで送信されません。[!DNL Adobe Sign] Scheduler サービスは、デフォルトで、署名者からの応答を 24 時間ごとにチェック（ポーリング）するように設定されています。このデフォルトの間隔は、ご利用の環境に合わせて変更できます。デフォルトの間隔を変更するには、次の手順を実行します。

1. 管理者の資格情報を使用して AEM [!DNL Forms] サーバーにログインし、**ツール**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;に移動します。

   ブラウザーウィンドウで、以下の URL に移動することもできます。
   `https://[localhost]:'port'/system/console/configMgr`

1. 「**[!UICONTROL Adobe Sign 設定サービス]**」オプションを探して選択します。「[ステータス更新スケジューラーの式](https://en.wikipedia.org/wiki/Cron#CRON_expression)」フィールドで **[!UICONTROL Cron 式]**&#x200B;を指定して「**[!UICONTROL 保存]**」をクリックします。例えば、毎日午前 0 時に設定サービスを実行するには、**[!UICONTROL ステータス更新スケジューラー式]**&#x200B;フィールドに `0 0 0 1/1 * ? *` を指定します。

これで、[!DNL Adobe Sign] のステータスを同期するデフォルトの間隔が変更されました。

## 関連記事 {#related-articles}

* [アダプティブフォームで Adobe Sign を使用する](../../forms/using/working-with-adobe-sign.md)
* [AEM Forms で Adobe Sign を利用する（ビデオ）](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/forms-and-sign/introduction.html?lang=ja)
