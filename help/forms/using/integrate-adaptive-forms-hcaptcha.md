---
title: AEM 6.5 Forms での hCaptcha&reg; の使用方法
description: hCaptcha® サービスでフォームのセキュリティを容易に強化できます。ステップバイステップガイドをご用意しております。
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: 6aa7a0a5-bd45-4628-abd0-312a9e6cf6fe
source-git-commit: 94a9f4087e36bfe5701ad9aafd4e8446ca643ddf
workflow-type: ht
source-wordcount: '872'
ht-degree: 100%

---

# AEM Forms 環境と hCaptcha® の接続 {#connect-your-forms-environment-with-hcaptcha-service}

<!--
<span class="preview">This feature is based on Feature Toggle id `FT_FORMS-12407`. To enable the feature, follow the steps given in the [Enable Feature Toggle](/help/forms/using/enable-feature-toggle.md) article. </span>
-->

<span class="preview">この機能は、デフォルトでは有効になっていません。公式アドレスから aem-forms-ea@adobe.com に書き込んで、機能へのアクセスをリクエストできます。</span>

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人間と自動化されたプログラム／ボットを区別するために、オンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のある目的を防止することで、オンライントランザクションの安全性を高めます。

hCaptcha® に加えて、AEM Forms 6.5 は、次の CAPTCHA ソリューションをサポートしています。

* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [Cloudflare Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md)

## AEM Forms 環境と hCaptcha® の統合

hCaptcha® サービスは、ボット、スパム、自動化された不正使用からフォームを保護します。チェックボックスウィジェットテストを行ってユーザーの反応を評価し、フォームを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のあるアクティビティを防止することで、オンライントランザクションの安全性を高めます。

AEM 6.5 アダプティブフォームは、hCaptcha&amp;reg をサポートしています。これを使用して、フォームの送信時にチェックボックスウィジェットの課題を提示できます。

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### AEM Forms 環境を hCaptcha® と統合するための前提条件 {#prerequisite}

AEM Forms で hCaptcha® を設定するには、hCaptcha® web サイトから [hCaptcha® サイトキーと秘密鍵](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key)を取得する必要があります。

### hCaptcha® の設定 {#steps-to-configure-hcaptcha}

AEM Forms を hCaptcha® サービスと統合するには、次の手順を実行します。

1. AEM Forms 環境に、AEM を外部サービスに接続するために使用されるクラウド設定を格納する設定コンテナを作成します。設定コンテナを作成するには：
   1. AEM Forms 環境を開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. 設定ブラウザーで、既存のフォルダーを選択するか、新規フォルダーを作成できます。
      * 新規フォルダーを作成し、クラウド設定を有効にするには：
         1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
         1. 設定を作成ダイアログで、名前とタイトルを指定し、「**[!UICONTROL クラウド設定]**」をオンにします。
         1. 「**[!UICONTROL 作成]**」をクリックします。
      * 既存のフォルダーに対してクラウド設定を有効にするには：
         1. 設定ブラウザーで、フォルダーを選択して「**[!UICONTROL プロパティ]**」を選択します。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. 「**[!UICONTROL 保存して閉じる]**」をクリックして設定内容を保存し、ダイアログを閉じます。

1. クラウドサービスを設定します。
   1. AEM オーサーインスタンスで、![tools-1](assets/tools-1.png)／**[!UICONTROL クラウドサービス]**&#x200B;に移動し、 「**[!UICONTROL hCaptcha®]**」をクリックします。
      ![hCaptcha® の ui](assets/hcaptcha-in-ui.png)
   1. 前の節で説明したように、作成または更新した設定コンテナを選択します。「**[!UICONTROL 作成]**」を選択します。
      ![hCaptcha® の設定](assets/config-hcaptcha.png)
   1. **[!UICONTROL タイトル]**、<!--**[!UICONTROL Name]**--> **[!UICONTROL サイトキー]**&#x200B;および&#x200B;**[!UICONTROL 秘密鍵]**&#x200B;を、[前提条件で取得](#prerequisite)した hCaptcha® サービスに指定します。
   1. 「**[!UICONTROL 作成]**」をクリックします。

      ![AEM Forms 環境を hCaptcha® に接続するよう Cloud Service を設定](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > [クライアントサイド JavaScript 検証 URL](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) と[サーバーサイド検証 URL](https://docs.hcaptcha.com/#verify-the-user-response-server-side) は、hCaptcha® 検証用に既に事前入力されているので、ユーザーは変更する必要がありません。

   hCAPTCHA サービスを設定すると、アダプティブフォームで使用できるようになります。

## アダプティブフォームでの hCaptcha® の使用 {#using-hCaptcha-in-aem-6.5}

1. AEM Forms 環境を開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択して、「**[!UICONTROL プロパティ]**」をクリックします。
1. **[!UICONTROL 設定コンテナ]**&#x200B;で、AEM Forms と hCaptcha を接続するクラウド設定が含まれる設定コンテナを選択します。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   hCaptcha 用の設定コンテナがない場合、設定コンテナを作成する方法について詳しくは、[AEM Forms 環境と hCaptcha® の接続](#configure-hcaptcha-steps-to-configure-hcaptcha)の節を参照してください。

   ![設定コンテナの選択](/help/forms/using/assets/captcha-properties.png)

1. アダプティブフォームを選択し、「**[!UICONTROL 編集]**」をクリックして、エディターでフォームを開きます。
1. コンポーネントブラウザーから **[!UICONTROL Captcha]** コンポーネントを、アダプティブフォームにドラッグ＆ドロップします。
1. **[!UICONTROL Captcha]** コンポーネントを選択し、プロパティ ![プロパティアイコン](assets/configure-icon.svg) をクリックして、プロパティダイアログを開きます。次のプロパティを指定します。

   ![hCaptcha® v1](assets/config-hcaptcha-v1-img.png)

   * **[!UICONTROL タイトル]：** Captcha コンポーネントのタイトルを指定します。
   * **[!UICONTROL 検証メッセージ]：**&#x200B;フォームの送信時またはユーザーアクション時に Captcha の検証用の検証メッセージを指定します。
   * **[!UICONTROL Captcha サービス]：**&#x200B;フォーム送信用の CAPTCHA サービスを選択します。ここでは、「hCaptcha®」を選択します。
   * **[!UICONTROL 設定]：** hCaptcha® 用に設定されたクラウド設定を選択します。
     >[!NOTE]
     >同様の目的で、環境内に複数のクラウド設定を作成することができます。そのため、サービスは慎重に選択してください。サービスが表示されない場合は、[AEM Forms 環境と hCaptcha® の接続](#connect-your-forms-environment-with-hcaptcha-service)で、AEM Forms 環境と hCaptcha® サービスを接続する Cloud Service を作成する方法を参照してください。

   * **[!UICONTROL エラーメッセージ]：** Captcha の送信が失敗した際にユーザーに表示するエラーメッセージを指定します。
   * **[!UICONTROL Captcha サイズ]：** hCaptcha® テストダイアログの表示サイズを選択できます。「**[!UICONTROL コンパクト]**」オプションを選択すると小さいサイズ、「**[!UICONTROL 標準]**」を選択すると比較的大きなサイズのhCaptcha® テストダイアログを表示できます。また、「**[!UICONTROL 非表示]**」オプションを選択すると、ユーザーインターフェイス上にチェックボックスウィジェットを明示的にレンダリングせずに hCaptcha® を検証できます。

1. 「**[!UICONTROL 完了]**」を選択します。


現在、フォームの入力者は hCaptcha® サービスによって提供される課題を正常にクリアした正規のフォームのみをフォーム送信できます。

**hCaptcha® は、Intuition Machines, Inc. の登録商標です。**


## よくある質問

* **Q：アダプティブフォーム内で複数の Captcha コンポーネントを使用できますか？**
* **A：**&#x200B;アダプティブフォームでは、複数の Captcha コンポーネントを使用することはできません。また、遅延読み込みのマークが付けられたフラグメントやパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

* [アダプティブフォームの CAPTCHA の使用](/help/forms/using/captcha-adaptive-forms.md)
* [アダプティブフォームで Turnstile Captcha を使用する](/help/forms/using/integrate-adaptive-forms-turnstile.md)
