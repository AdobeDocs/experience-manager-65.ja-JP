---
title: Web.Financeおよび従業員のセルフサービスリファレンスサイトのセットアップと設定
seo-title: Web.Financeおよび従業員のセルフサービスリファレンスサイトのセットアップと設定
description: AEM Forms のリファレンスサイトでは、AEM Forms を使用して、組織内にエンドツーエンドのワークフローを実装する方法を参照することができます。
seo-description: AEM Forms のリファレンスサイトでは、AEM Forms を使用して、組織内にエンドツーエンドのワークフローを実装する方法を参照することができます。
uuid: 199349b7-97bd-4eca-a2e7-19d6708fcbee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 03886dd3-5873-4908-912b-fbbddb26c322
docset: aem65
translation-type: tm+mt
source-git-commit: b0e071cb3bf972ceaa2af3b70a7887557e6f10f9
workflow-type: tm+mt
source-wordcount: '2915'
ht-degree: 45%

---


# Web.Financeおよび従業員のセルフサービスリファレンスサイトのセットアップと設定{#set-up-and-configure-we-finance-and-employee-self-service-reference-sites}

AEM Forms のリファレンスサイトでは、金融サービス業界や各種行政機関が AEM Forms をどのように使用して、複雑なトランザクションを、場所、時間、デバイスを問わないシンプルで魅力的なデジタルサービスに変換しているかについて紹介しています。

We.Financeリファレンスサイトは、既存および見込み客との関わり合いを実際に引き出し、ファーストタッチから、パーソナライズされたコスト効率の高い方法で通信やトランザクションを管理します。

「 [Software Distribution](https://docs.adobe.com/content/help/en/experience-cloud/software-distribution/home.html)」を使用して、We.GovおよびWe.Financeリファレンスサイトパッケージをインストールします。 詳しくは、「リファレンスサイトパッケージの [展開](#refsite)」を参照してください。

AEM Forms のリファレンスサイトでは、以下に示す AEM Forms の主要な機能を参照することができます。

* 魅力的でレスポンシブなアダプティブフォームとインタラクティブな通信のオーサリング体験がシンプルになりました。
* 対話型通信を使用すると、デバイスの設定やレイアウトに合わせて、インタラクティブでパーソナライズされたレスポンシブな顧客通信を作成できます。
* データを統合して各種のデータソースに接続し、データをフォームに事前に取り込み、フォームデータモデル経由でフォームを送信。
* ビジネスの各種プロセスとワークフローを自動化するためのフォームワークフロー。
* 高度なユーザーデータ管理および処理機能。
* アダプティブフォームに安全に署名して送信するための Adobe Sign との統合。
* ターゲットを設定したレコメンデーションを提供し、フォームからの ROI を最大化する A/B テストを実行するための Adobe Target との統合。
* フォームとキャンペーンのパフォーマンスを計測し、十分な情報を得た上で意志決定を行うための Adobe Analytics との統合。
* フォーム入力の操作性が向上。

リファレンスサイトには、独自のアセットを作成するためのテンプレートとして使用可能なアセットが用意されています。これらのアセットは、繰り返し使用することができます。

* アダプティブフォームに安全に署名して送信するための Adobe Sign との統合。

* アダプティブフォームに安全に署名して送信するための Adobe Sign との統合。

## リファレンスサイトの設定手順と前提条件 {#prerequisites-and-steps-to-set-up-reference-sites}

リファレンスサイトを設定する前に、次の事項を確認してください。

* **AEM の必須要素** AEM QuickStart、AEM Forms のアドオンパッケージ、リファレンスサイトパッケージ。See [AEM Forms releases](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) for add-on and reference sites packages details.

* **SMTP サービス** 任意の SMTP サービスを使用することができます。

* **Adobe Sign 開発者アカウントと Adobe Sign API アプリケーション** 電子署名機能を使用するには、Adobe Sign 開発者アカウントが必要になります。詳しくは、「[Adobe Sign](https://acrobat.adobe.com/jp/ja/why-adobe/developer-form.html)」を参照してください。

* AEM Formsと統合するMicrosoft Dynamics 365の実行インスタンスです。 リファレンスサイトを実行するには、サンプルデータをMicrosoft Dynamicsインスタンスにインポートして、リファレンスサイトで使用される対話型通信を事前入力します。
* Formsアドオンパッケージを含むAEMの実行中のインスタンスです。 詳しくは、「[AEM Forms のインストールと設定](../../forms/using/installing-configuring-aem-forms-osgi.md)」を参照してください。

リファレンスサイトのセットアップと構成を行うには、以下の手順を実行します。以下に記載されているとおりの順序で実行することをお勧めします。

<table>
 <tbody>
  <tr>
   <th><strong>ステップ</strong></th>
   <th><strong>設定</strong></th>
   <th><strong>備考</strong></th>
  </tr>
  <tr>
   <td><a href="#installandconfigureaemform">AEM Forms のインストールと設定</a></td>
   <td>オーサーインスタンスとパブリッシュインスタンス</td>
   <td>AEM Forms のオーサーインスタンスとパブリッシュインスタンスをインストールして設定を行います。</td>
  </tr>
  <tr>
   <td><a href="#ssl">SSL の設定</a></td>
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td>
   <td>Adobe Sign とのセキュアな通信を行うために、SSL 経由の HTTP を有効にします。</td>
  </tr>
  <tr>
   <td><p><a href="#externalizer">Day CQ Link Externalizer の設定</a></p> </td>
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td>
   <td><p>リファレンスサイトの使用例では、異なるトランザクションの電子メールを配信しています。この設定は、電子メールでニュースレターを配信する場合に必要になります。この設定により、URL と画像でパブリッシュインスタンスが参照されるようになります。 </p> </td>
  </tr>
  <tr>
   <td><a href="#cqmail">Day CQ 電子メールサービスを設定する</a></td>
   <td>オーサーインスタンスとパブリッシュインスタンス</td>
   <td>電子メールによる通信を行う場合は、この設定が必要になります。</td>
  </tr>
  <tr>
   <td><a href="#xss">デフォルトの XSS 設定の上書き</a></td>
   <td>公開</td>
   <td>xssセキュリティでブロックされる$、{、}の文字を上書きするために使用します。</td>
  </tr>
  <tr>
   <td><a href="#aemds">AEM DS の設定</a></td>
   <td>作成者</td>
   <td>パブリッシュインスタンスでのフォーム送信と、オーサーインスタンスでのプロセスワークフローについて、AEM DS を設定します。</td>
  </tr>
  <tr>
   <td><a href="#refsite">リファレンスサイトパッケージのデプロイメント</a></td>
   <td>作成者</td>
   <td>AEM Forms のオーサーインスタンスに、リファレンスサイトパッケージをデプロイします。</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">サンプルデータを Microsoft Dynamics に読み込む</a></td>
   <td>オーサーインスタンスとパブリッシュインスタンス</td>
   <td>クレジットカード申し込み、住宅ローン申し込み、住宅保険申し込みチュートリアル用のサンプルデータをインポートします。</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">OAuth クラウドサービスを Microsoft Dynamics 用に設定する</a></td>
   <td>オーサーインスタンスとパブリッシュインスタンス</td>
   <td>AEM FormsとMicrosoft Dynamicsの間の通信を有効にするように、AEM FormsでOAuthクラウドサービスを構成します。 </td>
  </tr>
  <tr>
   <td><a href="#scheduler">Adobe Sign スケジューラーの設定</a></td>
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td>
   <td>ステータスを 2 秒間隔で確認するようにスケジューラーの設定を変更します。</td>
  </tr>
  <tr>
   <td><a href="#sign-service">リファレンスサイトの Adobe Sign クラウドサービスの設定</a></td>
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td>
   <td>リファレンスサイトパッケージに付属している設定を、有効な資格情報で設定し直す必要があります。</td>
  </tr>
  <tr>
   <td><a href="#anonymous">匿名ユーザー用のフォーム共通設定サービスの構成</a></td>
   <td>公開</td>
   <td>この設定では、匿名ユーザーに対してレコードの生成の送信、署名、ドキュメントが可能です。</td>
  </tr>
  <tr>
   <td><a href="#fdm">フォームデータモデルに対する REST サービス Swagger ファイルの修正</a></td>
   <td>オーサーインスタンスとパブリッシュインスタンス<br /> </td>
   <td>現在の環境に合わせてサービスを修正します。</td>
  </tr>
 </tbody>
</table>

## AEM Forms のインストールと設定 {#installandconfigureaemform}

Install and deploy AEM Forms as described in [Installing and configuring AEM Forms on OSGi](../../forms/using/installing-configuring-aem-forms-osgi.md).

>[!NOTE]
>
>複数のパブリッシュインスタンスが存在する場合や、オーサーインスタンスとパブリッシュインスタンスが異なるマシン上に存在する場合は、複製エージェントと逆複製エージェントを設定してください。

## SSL の設定 {#ssl}

Adobe Sign サーバーとの通信を行うには、SSL を設定する必要があります。For detailed steps, see [Enabling HTTP Over SSL](/help/sites-administering/ssl-by-default.md).

>[!CAUTION]
>
>Do not configure force SSL on `/etc/map` folder.

## Day CQ Link Externalizer の設定 {#externalizer}

In AEM, the **Externalizer** is an OSGI service that allows you to programmatically transform a resource path (e.g. /path/to/my/page) into an external and absolute URL (for example, https://www.mycompany.com/path/to/my/page) by prefixing the path with a pre-configured DNS. 詳しくは、「[URL の外部化](/help/sites-developing/externalizer.md)」を参照してください。

>[!CAUTION]
>
>SSL で自己署名証明書を使用する場合は、HTTPS URL を外部化しないでください。
>
>また、ローカルサーバーの場合は、サーバーのホスト名ではなく localhost を使用してください。

オーサーインスタンスとパブリッシュインスタンスの両方で、以下の手順を実行します。

1. Go to OSGi Configuration at https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr.
1. Find and tap **Day CQ Link Externalizer** configuration.
設定を編集するための Day CQ Link Externalizer ダイアログが表示されます。
1. Day CQ Link Externalizer ダイアログの「ドメイン」フィールドで、以下の操作を実行します。

   * オーサーインスタンスで、外部システムからアクセス可能な発行 URL を指定します。例えば、ホスト名や発行用の Web サーバーを指定します。
   * パブリッシュインスタンスで、オーサー URL と発行 URL の両方を指定します。

1. オーサーインスタンスとパブリッシュインスタンスの両方で、「ドメイン」フィールドにローカルサーバーの URL が指定されていることを確認します。
1. 「**保存**」をタップします。すべてのサービスが再開されるまで待ちます。

## Day CQ 電子メールサービスの設定 {#cqmail}

リファレンスサイトの実装では、ユーザーがフォームに入力して送信した場合に電子メールをサンプルユーザーに送信する必要があります。Day CQ 電子メールサービスを設定して SMTP サービスの詳細を指定することにより、顧客に対して電子メールを自動的に送信することができます。詳しくは、「[電子メール通知の設定](/help/sites-administering/notification.md)」を参照してください。

パブリッシュインスタンスで以下の手順を実行して、電子メールサービスを設定します。

1. Go to OSGi Configuration at https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr.
1. Find and tap **Day CQ Mail Service** to open it for configuration.
1. SMTP サーバーのホスト名とポートの値を入力します。
1. Tap **Save.**

>[!NOTE]
>
>社内の SMTP サービスを使用することも、Gmail などのパブリックサービスを使用することもできます。SMTP サービスの設定方法については、SMTP サービスのマニュアルを参照してください。

## デフォルトの XSS 設定の上書き {#xss}

We.Finance リファレンスサイトの電子メールテンプレートには、電子メール内で使用するカスタマイズされた各種リンクが用意されています。These links have placeholder as `${placeholder}`. プレースホルダーは、電子メールの送信前に実際の値に置き換えられます。AEM のデフォルトの XSS 保護設定では、HTML コンテンツ内の URL に波括弧（**{ }**）を使用できません。ただし、パブリッシュインスタンスで以下の手順を実行することにより、デフォルトの設定を上書きすることができます。

1. `/libs/cq/xssprotection/config.xml` を `/apps/cq/xssprotection/config.xml` にコピーします。
1. 開く `/apps/cq/xssprotection/config.xml`.
1. In the `common-regexps` section, modify the `onsiteURL` entry as follows and save the file.

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>Curly braces (**{ }**) are included as accepted characters in the URL in HTML content.

SMTP サーバーを設定したら、Sarah Rose のペルソナを使ってフォームに入力し、下書きとして保存します。下書きとして保存する場合、電子メールを使用してその下書きを受信するオプションがあります。「**電子メールを送信**」ボタンをタップして、アプリケーションのドラフトのリンクが記載された電子メールを受信すれば、電子メールが正しく設定されています。Sarah の資格情報を使用してログインし、下書きを参照できることを確認してください。

## AEM DS の設定 {#aemds}

リファレンスサイトの使用例では、電子メール通信用の発行インスタンスでAEM DSサービスの設定が必要です。 発行インスタンスでAEM DSサービスのセットアップを設定する詳細な手順については、AEM DSの [設定を参照してください](../../forms/using/configuring-the-processing-server-url-.md)。

AEM Formsリファレンスサイトの場合、AEM DS Settings Serviceで、処理サーバーのURLではなく、パブリッシュサーバーのURLを指定します。

>[!CAUTION]
>
>Do not put `/lc` in the processing server URL if you are configuring it for AEM Forms OSGi.

## リファレンスサイトパッケージのデプロイメント {#refsite}

Install the reference sites packages using [Software Distribution](https://docs.adobe.com/content/help/en/experience-cloud/software-distribution/home.html).

* [AEM FormsFSIリファレンスサイトパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2FAEM-FORMS-6.5-FSI-REF-SITE)
* [AEM FormsWe.Govデモパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=168&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fwe-gov-forms.pkg.all-2.0.2.zip)

To learn more about how to use packages , see [How to Work With Packages](/help/sites-administering/package-manager.md).

パッケージをインストールして、オーサーインスタンスとパブリッシュインスタンスを開始したら、ブラウザーで以下の URL にアクセスします。

* `https://'[server]:[port]'/wegov`
* `https://'[server]:[port]'/wefinance`

インストールが正常に完了すると、 と We.Finance のリファレンスサイトのランディングページにアクセスできるようになります。

## (Optional) Import sample data into Microsoft Dynamics {#optional-import-sample-data-into-microsoft-dynamics}

住宅ローン申し込みサイトと自動保険申し込みリファレンスサイトは、Microsoft Dynamicsのレコードを使用するように構成されています。 リファレンスサイトパッケージは、Microsoft Dynamicsにインポートできるカスタムエンティティとサンプルレコードをインストールし、リファレンスサイトを実行します。 サンプルデータを移行し、設定するには、次の手順を実行します。

自動保険申込用にカスタムエンティティをインポートする手順は、次のとおりです。

1. Download the **WeFinanceAutoInsurance_1_0.zip** solution package from `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip` on your AEM author instance.
1. In your Microsoft Dynamics instance, go to **Settings > Solutions** and click **Import**. パッケージを選択して読み込みます。

自動保険申込用にカスタムエンティティをインポートする手順は、次のとおりです。

1. AEMFormsFSIRefsite_1_0.zip **パッケージをからダウンロードし** ま `https://[author]:'port'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`す。 パッケージを選択して読み込みます。

1. In your Microsoft Dynamics instance, go to **Settings > Solutions** and click **Import**. パッケージを選択して読み込みます。

顧客および保険証券レコードをインポートする手順は、次のとおりです。

1. Download the **We.Finance Customers.csv, We.Finance Auto Insurance Renewals.csv**, and **home mortgage** data files from the following locations on your AEM author instance:

   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. Microsoft Dynamicsインスタンスで、次の操作を行います。

   * **Sales** / **We.Finance Customers** (Sales **/** We.Financeのお客様)に移動し、「インポート」をクリックします。

   * **Sales** / **We.Finance Auto Insurance** に移動し、「 **インポート**」をクリックします。

   * **Sales** / **We.Finance Home Mortgageに移動し、「** インポート ****」をクリックします。

## OAuth クラウドサービスを Microsoft Dynamics 用に設定する {#configure-oauth-cloud-service-for-microsoft-dynamics}

AEM FormsとMicrosoft Dynamicsの間の通信を有効にするように、AEM FormsでOAuthクラウドサービスを構成します。 次の手順を実行して、AEM作成者インスタンスと発行インスタンスでOAuthCloud Serviceを設定します。

1. On AEM author instance, go to **Tools** > **Cloud Services** > **Data Sources** > **global**. 「 **リファレンスサイトのDynamics統合** 」アイコンをタップし、「プロパティ」をタップします。
1. Microsoft Azure Active Directory のアカウントに移動します。登録済みアプリケーションの「**応答 URL**」設定に、コピーしたクラウドサービス設定の URL を追加します。設定を保存します。
1. In the Authentication Settings tab, specify **Service Root**, **Client Id**, **Client Secret**, and **Resource URL** for your Microsoft Dynamics instance. Click **Connect to OAuth** that redirects to the Microsoft Dynamics login page.
1. ログイン情報を入力します。ログインすると、AEM Formsクラウドサービス設定ページにリダイレクトされます。 「**保存して閉じる**」をクリックします。クラウドサービスの設定が保存されます。
1. **Forms** / **データ統合** / **We.Financeに移動します**。 「自動保険（ダイナミクス）」を選択し、「編集」をクリックします。 Microsoft Dynamicsエンティティは、「データソース」タブに一覧表示されます。 すべてのエンティティがMicrosoft Dynamicsから取得され、「データソース」タブに表示されるまで待ちます。
1. Select the **AutoInsuranceRenewal entity** and click **Test Model Object**. In the input request section, specify the value for customer ID as “900001” and click **Test**. 「出力」セクションには、顧客ID 900001用のMicrosoft Dynamicsから取得したレコードが表示されます。
1. In the input request section, specify the value for customer ID as “900001” and click **Test**. 「出力」セクションには、顧客ID 900001用のMicrosoft Dynamicsから取得したレコードが表示されます。
1. 発行インスタンスで手順1 ～ 6を繰り返します。

## Adobe Sign スケジューラーの設定 {#scheduler}

オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. Go to AEM Web Configuration console at `https://'[server]:[port]'system/console/configMgr`.
1. Find and tap **[!UICONTROL Adobe Sign Configuration Service]** to open it for configuration.
1. 「**[!UICONTROL ステータス更新スケジューラーの式]**」で「**0 0/2 * * * ?**」を指定します。

   >[!NOTE]
   >
   >上記のようにスケジューラーを設定すると、Adobe Sign サービスのステータスが 2 分間隔で確認されます。

1. 「**[!UICONTROL 保存]**」をタップします。

## リファレンスサイトの Adobe Sign クラウドサービスの設定 {#sign-service}

オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. Go to **Tools** > **Cloud Services** > **Adobe Sign** > **global**. 「 **AEM Formsリファレンスサイトの署名** 」を選択し、「プロパティ」をタップします。

   >[!CAUTION]
   >
   >Ensure that the `https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html` URL is added to the redirect URL list of OAuth configuration of Adobe Sign API application.

1. クライアント ID と、Adobe Sign アプリケーション OAuth 設定の秘密鍵を指定します。
1. (Optional) Select the **[!UICONTROL Enable Adobe Sign for attachments also]** option, and tap **[!UICONTROL Connect to Adobe Sign]**. この操作により、アダプティブフォームの添付ファイルが、署名用に送信された対応する Adobe Sign ドキュメントに添付されます。
1. Tap **[!UICONTROL Connect to Adobe Sign]** and log in with your Adobe Sign credentials.

## フォーム共通設定サービスの構成 {#anonymous}

匿名ユーザーによるアクセスを許可するには、パブリッシュインスタンス上で以下の手順を実行します。

1. Go to AEM Web Configuration console at `https://'[server]:[port]'/system/console/configMgr`.
1. Find and tap **[!UICONTROL Forms Common Configuration Service]** to open it for configuration.
1. Configure the **[!UICONTROL Allow]** field for **[!UICONTROL All Users]**.
1. 「**[!UICONTROL 保存]**」をタップします。

## フォームデータモデルに対する REST サービスの修正 {#fdm}

オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. CRXDEに移動し `https://'[server]:[port]'/crx/de/index.jsp`ます。
1. /conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFile **に移動し、swaggerファイルを開きます** 。
1. 環境に応じて、ホストとポートの設定を更新します。
1. 設定を保存します。
1. (**作成者のみ**) **ツール/** Cloud Services **/** データソース/データソース/グローバルインスタンスに移動します。 ********/ 「 **roi-rest** 」を選択し、「 **プロパティ**」をタップします。「Tap Authentication Settings」をタップし、「 ************ Authentication Type」を「Basic Authentication」に設定します。 サービスにアクセスす `admin`るユーザー名/パスワード `admin`に「/」を指定します。 「**保存して閉じる**」をタップします。

## Marketing Cloudとの統合 {#integrate-with-marketing-cloud}

AEM FormsとAdobe AnalyticsとAdobe Targetを統合できます。 Adobe Analyticsはアダプティブフォームのレポートの生成やパフォーマンスの分析に役立ちますが、パーソナライズされたエクスペリエンスの提供や、アダプティブフォームのA/Bテストの実施に役立ちます。

AEM FormsでAdobe AnalyticsとAdobe Targetを設定するには、次の手順を実行します。

### Adobe Analytics の設定 {#configureanalytics}

AEM Forms を Adobe Analytics に統合することで、フォームやドキュメントに顧客がどう対応するか監視および分析できます。問題のある領域を特定して修正し、コンバージョン率を高めるための対策を行うのに役立ちます。

この機能をリファレンスサイトで使用するには、「[分析とレポートの設定](../../forms/using/configure-analytics-forms-documents.md)」の手順に従って、Analytics アカウントを設定します。

レポートを生成するために、シードデータはリファレンスサイトにバンドルされます。 シードデータを使用する前に、次の操作を行います。

1. We.Finance分析設定がAEMクラウドサービスで使用可能であることを確認します。 クラウドサービスは、次のいずれかの方法で検索できます。

   * [ **[!UICONTROL ツール]>[Cloud Services]>[レガシーCloud Services]** ]に移動するか、https://&lt;ホスト>:&lt;ポート>/libs/cq/core/content/tools/cloudservices.htmlを参照します。
   * In the **[!UICONTROL Cloud Services]** page, under **[!UICONTROL Adobe Analytics]** section, click `Show Configurations`. We.Financeの設定が利用できます。 クリックして設定を開きます。設定ページで「**[!UICONTROL 編集]**」をクリックします。有効な会社、ユーザー名、共有暗号鍵(Shared Secret)およびデータセンターを入力し、「Analytics **[!UICONTROL に接続]**」をクリックします。 「接続が成功しました」ダイアログが表示されたら、設定ダイアログで「 **[!UICONTROL OK]** 」をクリックします。 AnalyticsとReportsの [設定の説明に従って、Analyticsの設定でフレームワークを設定します](../../forms/using/configure-analytics-forms-documents.md)。

1. https://&lt;*host*>:&lt;*port*>/system/console/configMgrに移動し、次の操作を行います。

   * In the **[!UICONTROL Web Console Configuration]** page, find and click **[!UICONTROL AEM Forms Analytics Configuration]**.

   * AEM Forms解析設定ダイアログの「 **[!UICONTROL SiteCatalystフレームワーク]** 」フィールドで、「we-finance(we-finance)」または「we-gov(we-gov)」を選択します。
   * 「**[!UICONTROL 保存]**」をクリックして、ページを更新します。

1. https://&lt;host>:&lt;port>/aem/formsにあるforms managerに移動し、次の操作を行います。

   * Web.Financeフォルダーを開き、レポートを表示するフォームを選択します。
   * アクションツールバーの「Analyticsを有効にする」をクリックします。 フォームの分析を有効にしたら、「Analytics レポート」をクリックします。空白のレポートが生成されたことを確認できます。空のレポートが生成された後、デモ用の分析レポートを生成するには、リファレンスサイトパッケージに付属のシードデータを提供する必要があります。

   リファレンスサイトは、クレジットカード、住宅ローン、チャイルドサポートの使用例のシードデータを解析レポートに提供します。

### Target の設定 {#configure-target}

リファレンスサイトでは、アダプティブドキュメントにターゲットを設定し、パーソナライズしたコンテンツを含めるための AEM Forms と Adobe Target の統合を紹介しています。さらに、アダプティブフォームの A/B テストを作成することもできます。

リファレンスサイトで統合を利用するには、AEM で次のように Target を設定します。

1. Start the author quickstart with the jvm argument `-Dabtesting.enabled=true` to enable A/B testing on the server.

   >[!NOTE]
   >
   >AEMインスタンスがJBossで実行され、自動インストールからサービスとして開始される場合は、フ `-Dabtesting.enabled=true``jboss\bin\standalone.conf.bat` ァイルの次のエントリにパラメーターを追加します。
   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. `https://<hostname>:<port>/libs/cq/core/content/tools/cloudservices.html` にアクセスします。

1. In the **[!UICONTROL Adobe Target]** section, click **[!UICONTROL Show Configurations]**. We.Financeターゲット設定が利用可能です。 クリックして設定を開きます。設定ページで「**[!UICONTROL 編集]**」をクリックします。The **[!UICONTROL Edit Component]** dialog for the configuration opens.

1. Target アカウントに関連付けるクライアントコード、電子メール、パスワードを指定します。APIタイプを **[!UICONTROL RESTとして選択します]**。
1. 「**[!UICONTROL Adobe Target に接続]**」をクリックします。ターゲットアカウントが正しく設定されたら、「 **[!UICONTROL OK]**」をクリックします。 パッケージ化された構成にターゲットフレームワークがあることがわかります。

1. `https://<hostname>:<port>/system/console/configMgr` にアクセスします。

1. 「**[!UICONTROL AEM Forms Target の設定]**」をクリックします。
1. ターゲットフレームワークを選択します。
1. 「**[!UICONTROL Target URLs]**」フィールドに、AEM Forms への URL を指定します。例：`https://<hostname>:<port>/`

1. 「**[!UICONTROL 保存]**」をクリックします。

クレジットカード申し込みと住宅ローン申し込みの使用例では、A/Bテストの実行方法とデモ用のレポートの紹介方法を示しています。 チュートリアルについては、 [We.Financeリファレンスサイトのチュートリアルを参照してください](../../forms/using/finance-reference-site-walkthrough.md)。

## 次の手順 {#next-step}

これで、リファレンスサイトを利用するための設定がすべて完了しました。リファレンスサイトのワークフローと手順についての詳細は以下を参照してください。

* [We.Finance リファレンスサイトのチュートリアル](../../forms/using/finance-reference-site-walkthrough.md)
* [従業員セルフサービスリファレンスサイトのチュートリアル](../../forms/using/employee-self-service-reference-site.md)

