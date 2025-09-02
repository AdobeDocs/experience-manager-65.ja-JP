---
title: AEM アダプティブフォーム 6.5 で Turnstile を使用する方法
description: Turnstile サービスでフォームのセキュリティを容易に強化できます。ステップバイステップガイドをご用意しております。
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: bed93ce3-89db-477a-8316-7598275e4bca
source-git-commit: 94a9f4087e36bfe5701ad9aafd4e8446ca643ddf
workflow-type: ht
source-wordcount: '851'
ht-degree: 100%

---

# AEM Forms 環境と Turnstile の接続 {#connect-your-forms-environment-with-turnstile-service}

<!--
<span class="preview">This feature is based on Feature Toggle id `FT_FORMS-12407`. To enable the feature, follow the steps given in the [Enable Feature Toggle](/help/forms/using/enable-feature-toggle.md) article. </span>
-->

<span class="preview">この機能は、デフォルトでは有効になっていません。公式アドレスから aem-forms-ea@adobe.com に書き込んで、機能へのアクセスをリクエストできます。</span>

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人間と自動化されたプログラム／ボットを区別するために、オンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のある目的を防止することで、オンライントランザクションの安全性を高めます。

AEM Forms 6.5 は、次の CAPTCHA ソリューションをサポートしています。

* [Turnstile Captcha](/help/forms/using/integrate-adaptive-forms-turnstile.md)
* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)


<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## AEM Forms 環境と Turnstile Captcha の統合

Cloudflare の Turnstile Captcha は、自動ボット、悪意のある攻撃、スパム、不要な自動トラフィックからフォームとサイトを保護することを目的としたセキュリティ対策です。フォームの送信を許可する前に、フォームの送信時にユーザーが人間であることを確認するチェックボックスが表示されます。

>[!VIDEO](https://video.tv.adobe.com/v/3440940/)

### AEM Forms 環境と Turnstile Captcha を統合するための前提条件 {#prerequisite}

AEM Forms 用に Turnstile を設定するには、Turnstile web サイトから [Turnstile サイトキーと秘密鍵](https://developers.cloudflare.com/turnstile/get-started/)を取得する必要があります。

### Turnstile の設定 {#steps-to-configure-hcaptcha}

AEM Forms を Turnstile サービスと統合するには、次の手順を実行します。

1. AEM Forms 環境に設定コンテナを作成します。設定コンテナには、AEM Forms を外部サービスに接続するために使用されるクラウド設定が格納されます。設定コンテナを作成するには：
   1. AEM Forms 環境を開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. 設定ブラウザーで、既存のフォルダーを選択するか、新規フォルダーを作成します。
      * **新規フォルダー**&#x200B;を作成し、クラウド設定を有効にするには：
         1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
         1. 設定を作成ダイアログで、名前とタイトルを指定し、「**[!UICONTROL クラウド設定]**」をオンにします。
         1. 「**[!UICONTROL 作成]**」をクリックします。
      * **既存のフォルダー**&#x200B;に対してクラウド設定を有効にするには：
         1. 設定ブラウザーで、フォルダーを選択して「**[!UICONTROL プロパティ]**」をクリックします。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. 「**[!UICONTROL 保存して閉じる]**」をクリックして設定を保存します。

1. クラウドサービスを設定します。
   1. AEM オーサーインスタンスで、![tools-1](assets/tools-1.png)／**[!UICONTROL クラウドサービス]**&#x200B;に移動し、 「**[!UICONTROL Turnstile]**」をクリックします。
      ![クラウドサービスの Turnstile](assets/turnstile-in-ui.png)
   1. 前の節で説明したように、作成または更新した設定コンテナを選択します。「**[!UICONTROL 作成]**」をクリックします。
      ![設定 Turnstile](assets/config-hcaptcha.png)
   1. **[!UICONTROL ウィジェットタイプ]**&#x200B;を管理対象、非インタラクティブまたは非表示として指定します。
   1. **[!UICONTROL タイトル]**、**[!UICONTROL 名前]**&#x200B;など、その他の詳細を入力します。
   1. [前提条件で取得した](#prerequisite) Turnstile サービスの&#x200B;**[!UICONTROL サイトキー]**&#x200B;と&#x200B;**[!UICONTROL 秘密鍵]**&#x200B;を指定します。
   1. 「**[!UICONTROL 作成]**」をクリックします。

      ![AEM Forms 環境を Turnstile に接続するよう Cloud Service を設定](assets/config-turntstile.png)

   >[!NOTE]
   > クライアントサイド JavaScript 検証 URL とサーバーサイド検証 URL は、Turnstile 検証用に既に事前入力されているので、ユーザーは変更する必要がありません。

   Turnstile Captcha サービスを設定すると、アダプティブフォームで使用できるようになります。

## アダプティブフォームでの Turnstile の使用 {#using-turnstile-aem-6.5}

1. AEM Forms 環境を開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択して、「**[!UICONTROL プロパティ]**」をクリックします。**[!UICONTROL 設定コンテナ]**&#x200B;で、AEM Forms と Turnstile を接続するクラウド設定が含まれる設定コンテナを選択します。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   Captcha サービスを設定するための設定コンテナがない場合、設定コンテナを作成する方法について詳しくは、[Turnstile の設定](#configure-turnstile-steps-to-configure-hcaptcha)の節を参照してください。

   ![設定コンテナの選択](assets/captcha-properties.png)

1. アダプティブフォームを選択し、「**[!UICONTROL 編集]**」をクリックして、エディターでアダプティブフォームを開きます。
1. コンポーネントブラウザーから **[!UICONTROL Captcha]** コンポーネントを、アダプティブフォームにドラッグ＆ドロップします。
1. **[!UICONTROL Captcha]** コンポーネントを選択し、プロパティ ![プロパティアイコン](assets/configure-icon.svg) アイコンをクリックします。プロパティダイアログが開きます。次のプロパティを指定します。

   <!--![Turnstile v2](assets/turnstile-settings-v2.png)-->
   ![Cloudfare Turnstile v1](assets/turnstile-setting-v1.png)

   * **[!UICONTROL タイトル]：** Captcha コンポーネントのタイトルを指定します。フォームとルールエディターの両方で、一意のタイトルを使用して、フォームコンポーネントを簡単に特定できます。
   * **[!UICONTROL 設定]：** Turnstile 用に設定されたクラウド設定を選択します。
   * **[!UICONTROL 検証メッセージ]：**&#x200B;フォームの送信時またはユーザーアクション時に Captcha を検証するための検証メッセージを指定します。
   * **[!UICONTROL Captcha サービス]：**&#x200B;フォーム送信用の CAPTCHA サービスを選択します。ここでは、「Turnstile®」を選択します。
   * **[!UICONTROL 設定]：** Turnstile® 用に設定されたクラウド設定を選択します。
     >[!NOTE]
     >同様の目的で、環境内に複数のクラウド設定を作成することができます。そのため、サービスは慎重に選択してください。サービスが表示されない場合は、[AEM Forms 環境と Turnstile の接続](#connect-your-forms-environment-with-turnstile-service)で、AEM Forms 環境と Turnstile サービスを接続する Cloud Service を作成する方法を参照してください。

   * **[!UICONTROL エラーメッセージ]：** Captcha の送信が失敗した際にユーザーに表示するエラーメッセージを指定します。
   * **Captcha サイズ：** hCaptcha® テストダイアログの表示サイズを選択できます。「**[!UICONTROL コンパクト]**」オプションを選択すると小さいサイズ、「**[!UICONTROL 標準]**」を選択すると比較的大きなサイズの hCaptcha® テストダイアログを表示できます。

1. 「**[!UICONTROL 完了]**」を選択します。


現在、フォームの入力者は Turnstile サービスによって提供される課題を正常にクリアした正規のフォームのみをフォーム送信できます。

![Turnstile の課題](assets/turnstile-challenge.png)


## よくある質問

* **Q：アダプティブフォーム内で複数の Captcha コンポーネントを使用できますか？**
* **A：**&#x200B;アダプティブフォームでは、複数の Captcha コンポーネントを使用することはできません。また、遅延読み込みのマークが付けられたフラグメントやパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

* [アダプティブフォームの CAPTCHA の使用](/help/forms/using/captcha-adaptive-forms.md)
* [アダプティブフォームで hCaptcha を使用する](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)
