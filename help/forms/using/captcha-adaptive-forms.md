---
title: アダプティブフォームの CAPTCHA の使用
seo-title: アダプティブフォームの CAPTCHA の使用
description: アダプティブフォームで AEM CAPTCHA または Google reCAPTCHA サービスを設定する方法を説明します。
seo-description: アダプティブフォームで AEM CAPTCHA または Google reCAPTCHA サービスを設定する方法を説明します。
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 83%

---


# アダプティブフォームの CAPTCHA の使用{#using-captcha-in-adaptive-forms}

CAPTCHA（Completely Automated Public Turing test to tell Computers and Humans Apart）は、オンライントランザクションにおいて人間と自動プログラムやボットとを区別するために一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。これにより、テストに失敗した場合ユーザーは続行できないため、ボットによるスパムの投稿や悪意のある目的を防止し、オンライントランザクションを安全に保ちます。

AEM によるアダプティブフォームの CAPTCHA のサポートGoogleのreCAPTCHAサービスを使用して、CAPTCHAを実装できます。

>[!NOTE]
>
>* AEM Forms は reCaptcha v2 のみをサポートします。その他のバージョンはサポートされません。
>* アダプティブフォームの CAPTCHA は、AEM Forms アプリケーションのオフラインモードではサポートされていません。
>



## Google が提供する reCAPTCHA サービスの設定 {#google-recaptcha}

フォームの作成者は、Google による reCAPTCHA サービスを使用してアダプティブフォームに CAPTCHA を実装することができます。これにより、サイトを保護する高度な CAPTCHA 機能が提供されます。reCAPTCHA の仕組みについて詳しくは、「[Google reCAPTCHA](https://developers.google.com/recaptcha/)」を参照してください。

![Recaptcha](assets/recaptcha_new.png)

AEM Forms で reCAPTCHAを実装するには：

1. Google から [reCAPTCHA API キーペア](https://www.google.com/recaptcha/admin)を取得します。これにはサイトキーと秘密鍵が含まれます。
1. クラウドサービス用の設定コンテナを作成します。

   1. Go to **[!UICONTROL Tools > General > Configuration Browser]**.
   1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。

      1. 設定ブラウザーで、「**[!UICONTROL global]**」フォルダーを選択して「**[!UICONTROL プロパティ]**」をタップします。

      1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
      1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。
   1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
   1. 設定を作成ダイアログでフォルダーのタイトルを指定し、「**[!UICONTROL クラウド設定]**」を有効にします。
   1. Tap **[!UICONTROL Create]** to create the folder enabled for cloud service configurations.


1. reCAPTCHA のクラウドサービスを設定します。

   1. On your AEM author instance, go to ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. 「**[!UICONTROL reCAPTCHA]**」をタップします。設定ページが表示されます。上記の手順で作成した設定コンテナを選択し、「**[!UICONTROL 作成]**」をタップします。
   1. Specify Name, Site key, and Secret Key for reCAPTCHA service and tap **[!UICONTROL Create]** to create the cloud service configuration.
   1. コンポーネントを編集ダイアログで、サイトおよび手順 1 で取得した秘密鍵を指定します。Tap **Save Settings** and then tap **OK** to complete the configuration.
   reCAPTCHA サービスを設定すると、アダプティブフォームで使用できるようになります。詳しくは、「[アダプティブフォームの CAPTCHA の使用](#using-captcha)」を参照してください。

## アダプティブフォームで CAPTCHA を使用する {#using-captcha}

アダプティブフォームで CAPTCHA を使用するには：

1. アダプティブフォームを編集モードで開きます。

   >[!NOTE]
   >
   >アダプティブフォームの作成時に選択した設定コンテナに、reCAPTCHA クラウドサービスが含まれていることを確認してください。アダプティブフォームのプロパティを編集して、そのアダプティブフォームに関連付けられている設定コンテナを変更することもできます。

1. コンポーネントブラウザーから&#x200B;**Captcha** コンポーネントを、アダプティブフォームにドラッグアンドドロップしますす。

   >[!NOTE]
   >
   >アダプティブフォームにおける複数の Captcha コンポーネントの使用はサポートされていません。また、遅延読み込みとしてマークされているパネルやフラグメント内のパネルで CAPTCHA を使用することはお勧めしません。

   >[!NOTE]
   >
   >Captcha は、約 1 分間で期限切れになります。そのため、アダプティブフォームに「送信」ボタンを配置する直前に Captcha コンポーネントを配置することをお勧めします。

1. Select the Captcha component you added and tap ![cmppr](assets/cmppr.png) to edit its properties.
1. CAPTCHA ウィジェットのタイトルを指定します。The default value is **Captcha**. タイトルを表示しない場合は、「**タイトルを非表示にする**」を選択します。
1. From the **Captcha service** drop-down, select **reCaptcha** to enable reCAPTCHA service if you configured it as described in [ReCAPTCHA service by Google](#google-recaptcha). 「設定」ドロップダウンから設定を選択します。また、reCAPTCHA ウィジェットのサイズを「**標準**」または「**コンパクト**」から選択します。

   >[!NOTE]
   >
   >デフォルトの AEM CAPTCHA サービスは非推奨であるため、「Captcha サービス」ドロップダウンで「**[!UICONTROL デフォルト]**」を選択しないでください。

1. 各プロパティを保存します。

アダプティブフォーム上で reCAPTCHA サービスが有効になります。フォームをプレビューして、CAPTCHA が機能していることを確認できます。
