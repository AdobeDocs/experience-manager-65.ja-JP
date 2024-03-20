---
title: アダプティブフォームの CAPTCHA の使用
description: アダプティブフォームで AEM CAPTCHA または Google reCAPTCHA サービスを設定する方法を説明します。
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 100%

---

# アダプティブフォームの CAPTCHA の使用{#using-captcha-in-adaptive-forms}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/captcha-adaptive-forms.html?lang=ja) |
| AEM 6.5 | この記事 |


<span class="preview"> [アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人間と自動化されたプログラム／ボットを区別するために、オンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットがスパムや悪意のある目的の投稿を防ぐことで、オンライントランザクションの安全性を高めます。

AEM Forms は、アダプティブフォームでの CAPTCHA をサポートします。Google が提供する reCAPTCHA サービスを使用して、CAPTCHA を実装できます。

>[!NOTE]
>
>* AEM Forms は、reCAPTCHA v2 および Enterprise をサポートします。その他のバージョンはサポートされません。
>* アダプティブフォームの CAPTCHA は、AEM Forms アプリのオフラインモードではサポートされていません。

## アダプティブフォーム向けに Google が提供する reCAPTCHA サービスを設定する {#google-reCAPTCHA}

AEM Forms のユーザーは、Google が提供する reCAPTCHA サービスを使用してアダプティブフォームに CAPTCHA を実装できます。サイトを保護する高度な CAPTCHA 機能を提供します。reCAPTCHA の仕組みについて詳しくは、[Google reCAPTCHA](https://developers.google.com/recaptcha/) を参照してください。reCAPTCHA v2 や reCAPTCHA Enterprise を含む reCAPTCHA サービスは、AEM Forms に統合されています。要件に基づいて、reCAPTCHA サービスを設定して、次を有効にすることができます。

* [AEM Forms の reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [AEM Forms の reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)

![reCAPTCHA](/help/forms/using/assets/recaptcha_new.png)

### reCAPTCHA Enterprise の設定  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys?hl=ja#enable-the-recaptcha-enterprise-api) で有効になった [reCAPTCHA Enterprise プロジェクト](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys?hl=ja#before-you-begin)を作成します。
1. プロジェクト ID を[取得](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed)します。
1. [API キー](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys?hl=ja#create_an_api_key)および [web サイトのサイトキー](https://cloud.google.com/recaptcha-enterprise/docs/create-key?hl=ja#create-key)を作成します。
1. クラウドサービス用の設定コンテナを作成します。

   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
   1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。
      1. 設定ブラウザーで、**[!UICONTROL global]** フォルダーを選択して「**[!UICONTROL プロパティ]**」を選択します。
      1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
      1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

   1. 設定ブラウザーで「**[!UICONTROL 作成]**」を選択します。
   1. 設定を作成ダイアログでフォルダーのタイトルを指定し、「**[!UICONTROL クラウド設定]**」を有効にします。
   1. 「**[!UICONTROL 作成]**」を選択します。これで、クラウドサービス設定が有効になったフォルダーが作成されました。
1. reCAPTCHA Enterprise のクラウドサービスを設定します。

   1. Experience Manager オーサーインスタンスで、![tools-1](assets/tools-1.png)／**[!UICONTROL クラウドサービス]**&#x200B;に移動します。
   1. 「**[!UICONTROL reCAPTCHA]**」を選択します。設定ページが表示されます。前の手順で作成した設定コンテナを選択し、「**[!UICONTROL 作成]**」を選択します。
   1. reCAPTCHA Enterprise としてバージョンを選択し、名前、reCAPTCHA Enterprise サービスのプロジェクト ID、サイトキーおよび API キー（手順 2 および 3 で取得）を指定します。
   1. キーのタイプを選択します。キーのタイプは、Google Cloud プロジェクトで設定したサイトキー（**チェックボックスサイトキー**&#x200B;または&#x200B;**スコアベースのサイトキー**&#x200B;など）と同じにする必要があります。
   1. 0～1 の範囲でしきい値スコアを指定します（[クリックしてスコアの詳細を見る](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment?hl=ja#interpret_scores)）。スコアがしきい値以上になると、人間のインタラクションを識別し、それ以外の場合はボットのインタラクションとみなされます。

      > メモ：
      >
      > * フォーム作成者は、フォームの送信を中断しないために適切な範囲でスコアを指定できます。

   1. 「**[!UICONTROL 作成]**」を選択して、クラウドサービス設定を作成します。

   1. コンポーネントを編集ダイアログで、名前、プロジェクト ID、サイトキー、API キー（手順 2 および 3 で取得）を指定し、キータイプを選択して、しきい値スコアを入力します。「**[!UICONTROL 設定を保存]**」を選択してから、「**[!UICONTROL OK]**」を選択して設定を完了します。

reCAPTCHA Enterprise サービスを有効にすると、アダプティブフォームで使用できるようになります。[アダプティブフォームでの CAPTCHA の使用](#using-reCAPTCHA)を参照してください。

![reCAPTCHA Enterprise](/help/forms/using/assets/recaptcha1-enterprise.png)


### Google reCAPTCHA v2 の設定 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Google から [reCAPTCHA API キーペア](https://www.google.com/recaptcha/admin)を取得します。これには、**サイトキー**&#x200B;と&#x200B;**秘密鍵**&#x200B;が含まれます。
1. クラウドサービス用の設定コンテナを作成します。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
   1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。

      1. 設定ブラウザーで、**[!UICONTROL global]** フォルダーを選択して「**[!UICONTROL プロパティ]**」を選択します。

      1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
      1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。

   1. 設定ブラウザーで「**[!UICONTROL 作成]**」を選択します。
   1. 設定を作成ダイアログでフォルダーのタイトルを指定し、「**[!UICONTROL クラウド設定]**」を有効にします。
   1. 「**[!UICONTROL 作成]**」を選択します。これで、クラウドサービス設定が有効になったフォルダーが作成されました。

1. reCAPTCHA v2 用にクラウドサービスを設定します。

   1. AEM オーサーインスタンスで、![tools-1](assets/tools-1.png)／**クラウドサービス**&#x200B;に移動します。
   1. 「**[!UICONTROL reCAPTCHA]**」を選択します。設定ページが表示されます。前の手順で作成した設定コンテナを選択し、「**[!UICONTROL 作成]**」を選択します。
   1. バージョンとして reCAPTCHA v2 を選択し、名前を指定します。reCAPTCHA サービスのサイトキーと秘密鍵（手順 1 で取得）を入力し、「**[!UICONTROL 作成]**」を選択してクラウドサービス設定を作成します。
   1. コンポーネントを編集ダイアログで、サイトおよび手順 1 で取得した秘密鍵を指定します。「**[!UICONTROL 設定を保存]**」を選択してから、「**OK**」を選択して設定を完了します。

   reCAPTCHA サービスを設定すると、アダプティブフォームで使用できるようになります。詳細情報は、[アダプティブフォームでの CAPTCHA の使用](#using-captcha)を参照してください。

![reCAPTCHA v2](/help/forms/using/assets/recaptcha-v2.png)


## アダプティブフォームでの reCAPTCHA の使用 {#using-reCAPTCHA}

アダプティブフォームで reCAPTCHA を使用するには、以下を実行します。

1. アダプティブフォームを編集モードで開きます。

   >[!NOTE]
   >
   >アダプティブフォームの作成時に選択した設定コンテナに、reCAPTCHA クラウドサービスが含まれていることを確認してください。アダプティブフォームのプロパティを編集して、そのアダプティブフォームに関連付けられている設定コンテナを変更することもできます。

1. **Captcha** コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。

   >[!NOTE]
   >
   >アダプティブフォームでの複数の Captcha コンポーネントの使用はサポートされていません。また、遅延読み込み用とマークされたパネルやフラグメントでは、CAPTCHA を使用しないことをお勧めします。

   >[!NOTE]
   >
   >Captcha には時間制限があり、約 1 分で有効期限が切れます。そのため、アダプティブフォームに「送信」ボタンを配置する直前に Captcha コンポーネントを配置することをお勧めします。

1. 追加した Captcha コンポーネントを選択し、「![cmppr](assets/cmppr.png)」を選択してそのプロパティを編集します。
1. CAPTCHA ウィジェットのタイトルを指定します。デフォルト値は **Captcha** です。タイトルを表示しない場合は、「**タイトルを非表示にする**」を選択します。
1. [Google が提供する reCAPTCHA サービス](#google-reCAPTCHA)の説明に従って設定した場合は、**Captcha サービス**&#x200B;ドロップダウンから「**reCAPTCHA**」を選択して reCAPTCHA サービスを有効にします。
1. 設定ドロップダウンから設定を選択します。
1. **選択した設定のバージョンが reCAPTCHA Enterprise の場合**：
   1. **キータイプ**&#x200B;を&#x200B;**チェックボックス**&#x200B;として、reCAPTCHA クラウド設定を選択できます。チェックボックスのキータイプでは、Captcha の検証が失敗した場合、カスタマイズされたエラーメッセージがインラインメッセージとして表示されます。サイズは、「**[!UICONTROL 標準]**」と「**[!UICONTROL コンパクト]**」から選択できます。
   1. **キータイプ**&#x200B;を&#x200B;**スコアベース**&#x200B;として、reCAPTCHA クラウド設定を選択できます。スコアベースのキータイプでは、Captcha の検証が失敗した場合、カスタマイズされたエラーメッセージがポップアップメッセージとして表示されます。
   1. **[!UICONTROL バインド参照]**&#x200B;を選択した場合は連結データが送信され、それ以外の場合は非連結データが送信されます。フォームが送信されたときの、非連結データと連結データ（バインド参照が SSN）の XML の例を以下に示します。

      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data>
                  <captcha16820607953761>
                      <captchaType>reCAPTCHAEnterprise</captchaType>
                      <captchaScore>0.9</captchaScore>
                  </captcha16820607953761>
              </data>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>371237912</SSN>
                      <FirstName>Sarah </FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608034928</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data/>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>
                          <captchaType>reCAPTCHAEnterprise</captchaType>
                          <captchaScore>0.9</captchaScore>
                      </SSN>
                      <FirstName>Sarah</FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608035111</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


   **選択した設定のバージョンが reCAPTCHA v2 の場合**：
   1. reCAPTCHA ウィジェットのサイズを、「**[!UICONTROL 標準]**」または「**[!UICONTROL コンパクト]**」から選択します。また、「**[!UICONTROL 非表示]**」オプションを使用して、疑わしいアクティビティの場合にのみ CAPTCHA チャレンジを表示できます。以下に表示されている **reCAPTCHA による保護**&#x200B;バッジが保護されたフォームに表示されます。

      ![reCAPTCHA バッジによって保護された Google](/help/forms/using/assets/google-recaptcha-v2.png)


   アダプティブフォーム上で reCAPTCHA サービスが有効になります。フォームをプレビューして、CAPTCHA が機能していることを確認できます。

1. 各プロパティを保存します。

>[!NOTE]
> 
> デフォルトの AEM CAPTCHA サービスは非推奨なので、Captcha サービスドロップダウンで「**[!UICONTROL デフォルト]**」を選択しないでください。

### ルールに基づいた CAPTCHA コンポーネントの表示／非表示 {#show-hide-captcha}

アダプティブフォームのコンポーネントに適用するルールに基づいて、CAPTCHA コンポーネントの表示／非表示を切り替えることができます。コンポーネントを選択して、「![ルールを編集](assets/edit-rules-icon.svg)」を選択し、「**[!UICONTROL 作成]**」を選択してルールを作成します。ルールの作成について詳しくは、「[ルールエディター](rule-editor.md)」を参照してください。

例えば、CAPTCHA コンポーネントは、フォームの「通貨の値」フィールドの値が 25000 を超える場合にのみ、アダプティブフォームに表示する必要があります。

フォームの「**[!UICONTROL 通貨の値]**」フィールドを選択して、以下のルールを作成します。

![ルールを表示／非表示](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> * サイズを&#x200B;**[!UICONTROL 非表示]**&#x200B;にするか、reCAPTCHA Enterprise スコアベースのキーを使用して reCAPTCHA v2 の設定を選択した場合、表示／非表示オプションは適用されません。

### CAPTCHA の検証 {#validate-captcha}

アダプティブフォーム内の CAPTCHA は、フォームを送信するとき、またはユーザーの操作や条件に基づいて CAPTCHA 検証を行うときに検証できます。

#### フォーム送信時の CAPTCHA の検証 {#validation-form-submission}

アダプティブフォームの送信時に CAPTCHA を自動的に検証するには、以下の手順を実行します。

1. CAPTCHA コンポーネントを選択し、![cmppr](assets/configure-icon.svg) を選択して、コンポーネントのプロパティを表示します。
1. 「**[!UICONTROL CAPTCHA を検証]**」セクションで、「**[!UICONTROL フォーム送信時に CAPTCHA を検証]**」を選択します。
1. 「![完了](assets/save_icon.svg)」を選択して、コンポーネントプロパティを保存します。

#### ユーザーの操作と条件に対する CAPTCHA の検証 {#validate-captcha-user-action}

条件とユーザー操作に基づいて CAPTCHA を検証するには、以下の手順を実行します。

1. Captcha コンポーネントを選択し、「![cmppr](assets/configure-icon.svg)」を選択してコンポーネントプロパティを表示します。
1. 「**[!UICONTROL CAPTCHA を検証]**」セクションの、「**[!UICONTROL ユーザーアクションで CAPTCHA を検証する]**」を選択します。
1. 「![完了](assets/save_icon.svg)」を選択して、コンポーネントプロパティを保存します。

   >[!NOTE]
   >
   >
   > サイズを&#x200B;**[!UICONTROL 非表示]**&#x200B;にするか、reCAPTCHA Enterprise スコアベースのキーを使用して reCAPTCHA v2 の設定を選択した場合、ユーザーアクションの有効な Captcha が適用されません。

[!DNL Experience Manager Forms] は、事前定義済みの条件を使用して CAPTCHA を検証する `ValidateCAPTCHA` API を提供します。この API は、カスタム送信アクションを使用するか、アダプティブフォームのコンポーネントにルールを定義することで呼び出すことができます。

以下の例は、事前定義された条件を使用して CAPTCHA を検証する `ValidateCAPTCHA` API の例です。

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
        GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

この例は、フォームの入力時にユーザーが指定した数値ボックスの桁数が 5 より大きい場合にのみ、`ValidateCAPTCHA` API がフォームの CAPTCHA を検証することを示しています。

**オプション 1：[!DNL Experience Manager Forms] ValidateCAPTCHA API を使用して、カスタム送信アクションを使用して CAPTCHA を検証する**

`ValidateCAPTCHA` API を使用してカスタム送信アクションを使用して CAPTCHA を検証するには、以下の手順を実行します。

1. `ValidateCAPTCHA` API を含むスクリプトをカスタム送信アクションに追加します。カスタム送信アクションについて詳しくは、「[アダプティブフォーム用のカスタム送信アクションの作成](custom-submit-action-form.md)」を参照してください。
1. アダプティブフォームの&#x200B;**[!UICONTROL 送信]**&#x200B;プロパティの「**[!UICONTROL 送信アクション]**」ドロップダウンリストから、カスタム送信アクションの名前を選択します。
1. 「**[!UICONTROL 送信]**」を選択します。CAPTCHA は、カスタム送信アクションの `ValidateCAPTCHA` API で定義された条件に基づいて検証されます。

**オプション 2：フォームを送信する前に、[!DNL Experience Manager Forms] ValidateCAPTCHA API を使用してユーザーアクションに対する CAPTCHA の検証を行う**

また、アダプティブフォーム内のコンポーネントにルールを適用することで、`ValidateCAPTCHA` API を呼び出すこともできます。

例えば、アダプティブフォームに「**[!UICONTROL CAPTCHA を検証]**」ボタンを追加し、ボタンをクリックするとサービスを呼び出すルールを作成します。

以下の図は、「**[!UICONTROL CAPTCHA を検証]**」ボタンをクリックしてサービスを呼び出す方法を示しています。

![CAPTCHA の検証](assets/captcha-validation1.gif)

`ValidateCAPTCHA` API を含むカスタムサーブレットをルールエディターを使用して呼び出し、検証結果に基づいてアダプティブフォームの送信ボタンを有効または無効にできます。

同様に、ルールエディターを使用して、アダプティブフォーム内の CAPTCHA を検証するカスタムメソッドを含めることができます。

<!--
### Add custom CAPTCHA services {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. However, you can add a custom service to display in the **[!UICONTROL CAPTCHA Service]** drop-down list.  

The following is a sample implementation of the interface to add additional CAPTCHA service to your Adaptive Form:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` Refers to the resource path of the CAPTCHA component in the Sling repository. Use this property to include details specific to the CAPTCHA component. For example, `captchaPropertyNodePath` includes information for the reCAPTCHA cloud configuration configured on the CAPTCHA component. The cloud configuration information provides **[!UICONTROL Site Key]** and **[!UICONTROL Secret Key]** settings for implementing the reCAPTCHA service.

`userResponseToken` Refers to the `g_reCAPTCHA_response` that gets generated after solving a CAPTCHA in a form. -->
