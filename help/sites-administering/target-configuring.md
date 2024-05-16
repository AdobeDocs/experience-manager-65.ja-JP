---
title: 手動での Adobe Target との統合の設定
description: Adobe Target との統合を手動で設定する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 0f710685-dc4f-4333-9847-d002b2637d08
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: ht
source-wordcount: '2122'
ht-degree: 100%

---

# 手動での Adobe Target との統合の設定 {#manually-configuring-the-integration-with-adobe-target}

ウィザードを使用するときに作成したオプトインウィザードの設定を変更するか、ウィザードを使用しないで手動で Adobe Target と統合できます。

## オプトインウィザードの設定の変更 {#modifying-the-opt-in-wizard-configurations}

[AEM を Adobe Target と統合](/help/sites-administering/target.md)する[オプトインウィザード](/help/sites-administering/opt-in.md)では、プロビジョニングされた Target 設定という名前の Target クラウド設定が自動的に作成されます。また、ウィザードではプロビジョニングされた Target フレームワークという名前のクラウド設定の Target フレームワークも作成されます。クラウド設定とフレームワークのプロパティは、必要に応じて変更できます。

また、コンテンツをターゲット化するときに、A4T Analytics クラウド設定を変更して、Adobe Analytics をレポートソースとして使用するように Adobe Target を設定できます。

クラウド設定とフレームワークの場所を特定するには、**ツール**／**デプロイメントt**／**クラウド**&#x200B;の **クラウドサービス**&#x200B;に移動します。（[http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)）
Adobe Target の下で、「**設定を表示**」をクリックします。

### プロビジョニングされた Target 設定のプロパティ {#provisioned-target-configuration-properties}

次のプロパティ値は、オプトインウィザードで作成されるプロビジョニングされた Target 設定のクラウド設定で使用されます。

* **クライアントコード：**&#x200B;オプトインウィザードに入力されているとおりです。
* **メール：**&#x200B;オプトインウィザードに入力されているとおりです。
* **パスワード：**&#x200B;オプトインウィザードに入力されているとおりです。
* **API のタイプ：** REST
* **Adobe Target からセグメントを同期：** 選択されています。

* **クライアントライブラリ：** mbox.js
* **DTM を使用してクライアントライブラリを提供：**&#x200B;選択されていません。[DTM](/help/sites-administering/dtm.md)または別のタグ管理システムを使用して mbox.js または AT.js ファイルをホストする場合は、このオプションを選択します。ライブラリの配信には AEM ではなく DTM を使用することをお勧めします。

* **カスタム mbox.js**：何も指定されておらず、デフォルトの mbox.js ファイルが使用されます。必要に応じて、使用するカスタム mbox.js を指定します。mbox.js を選択した場合にのみ表示されます。
* **カスタム AT.js：**&#x200B;何も指定されておらず、デフォルトの AT.js ファイルが使用されます。必要に応じて、使用するカスタム AT.js を指定します。AT.js を選択した場合にのみ表示されます。

>[!NOTE]
>
>AEM 6.3 では、Target ライブラリファイル [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/) を選択できます。このファイルは、Adobe Target 用の新しい実装ライブラリであり、通常の web 実装と単一ページアプリケーションの両方に使用できるように設計されています。
>
>AT.js は mbox.js ライブラリよりも、次のような強化点を提供します。
>
>* Web 実装のページ読み込み時間の向上
>* セキュリティの向上
>* 単一ページアプリケーション向けの実装オプションの改善
>* target.js に含まれていたコンポーネントが AT.js にも含まれているので、ターゲットへの呼び出しがなくなりました。

<!-- OLD URL WHICH IS 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### プロビジョニングされた Target フレームワークのプロパティ {#provisioned-target-framework-properties}

オプトインウィザードで作成されるプロビジョニングされた Target フレームワークはプロファイルデータストアからコンテキストデータを送信するように設定されています。ストアの年齢と性別のデータ項目はデフォルトで Target に送信されます。お使いのソリューションでは追加のパラメーターを送信する必要があります。

![プロビジョニングされた Target フレームワーク](assets/chlimage_1-158.png)

[Target フレームワークの追加](/help/sites-administering/target-configuring.md#adding-a-target-framework)で説明されている通り、追加のコンテキスト情報を Target に送信するようにフレームワークを設定できます。

### A4T Analytics クラウド設定の設定 {#configuring-a-t-analytics-cloud-configuration}

コンテンツをターゲット化するときに、Adobe Analytics をレポートソースとして使用するように Adobe Target を設定できます。

>[!NOTE]
>
>ユーザー資格情報認証（レガシー）は、A4T（Target と Analytics の両方）では機能しません。そのため、ユーザー資格情報認証の代わりに IMS 認証を使用する必要があります。

これを行うには、Adobe Target クラウド設定を接続する A4T クラウド設定を指定します。

1. **AEM のロゴ**／**ツール**／**デプロイメント**／**クラウドサービス**&#x200B;の順に移動して&#x200B;**クラウドサービス**&#x200B;にアクセスします。
1. 「**Adobe Target**」セクションで、「**今すぐ設定**」をクリックします。
1. Adobe Target 設定に再接続します。
1. **A4T Analytics クラウド設定**&#x200B;ドロップダウンメニューで、フレームワークを選択します。

   >[!NOTE]
   >
   >A4T に対して有効化されている Analytics 設定のみを使用できます。
   >
   >AEM で A4T を設定する際には、「設定の参照が欠落しています」というエントリが表示される場合があります。分析フレームワークを選択できるようにするには、次の操作を行います。
   >
   >1. **ツール**／**一般**／**CRXDE Lite** に移動します。
   >1. [A4T Analytics 設定ダイアログ](#a4t-analytics-config-dialog)に移動します（以下を参照）。
   >1. プロパティ **無効化** を **false** に設定します。
   >1. 「**すべて保存**」をクリックします。

#### A4T Analytics 設定ダイアログ {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

「**OK**」をクリックします。Adobe Target でコンテンツのターゲットに設定すると、[レポートソースを選択](/help/sites-authoring/content-targeting-touch.md)できるようになります。

## 手動での Adobe Target との統合 {#manually-integrating-with-adobe-target}

オプトインウィザードを使用せずに手動で Adobe Target と統合します。

>[!NOTE]
>
>Target ライブラリファイル [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/) は、Adobe Target 用の新しい実装ライブラリであり、通常の ｗeb 実装と単一ページアプリケーションの両方に使用できるように設計されています。アドビは、クライアントライブラリとして mbox.js ではなく AT.js を使用することをお勧めします。
>
>AT.js は mbox.js ライブラリよりも、次のような強化点を提供します。
>
>* Web 実装のページ読み込み時間の向上
>* セキュリティの向上
>* 単一ページアプリケーション向けの実装オプションの改善
>* AT.js は、target.js に含まれていたコンポーネントを含むので、target.js を呼び出す必要がなくなりました
>
>**クライアントライブラリ**&#x200B;ドロップダウンメニューでは、AT.js または mbox.js を選択できます。

<!-- OLD URL from above was 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Target クラウド設定の作成 {#creating-a-target-cloud-configuration}

AEM が Adobe Target とやり取りできるようにするには、Target クラウド設定を作成します。設定を作成するには、Adobe Target のクライアントコードとユーザーの資格情報を指定します。

複数の AEM キャンペーンに設定を関連付けることができるので、Target クラウド設定を作成するのは 1 回のみです。複数の Adobe Target クライアントコードがある場合、各クライアントコードに対して 1 つの設定を作成します。

クラウド設定を設定して、Adobe Target からセグメントを同期することができます。同期を有効にした場合は、クラウド設定が保存されるとすぐに、バックグラウンドでセグメントが Target から読み込まれます。

AEMで Target クラウド設定を作成するには、以下の手順を実行します。

1. **AEM ロゴ**／**ツール**／**クラウドサービス**／**従来のクラウドサービス**&#x200B;を使用して、**クラウドサービス**&#x200B;に移動します。（[http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)）

   **クラウドサービス**&#x200B;概要ページが開きます。

1. 「**Adobe Target**」セクションで、「**今すぐ設定**」をクリックします。
1. **設定を作成**&#x200B;ダイアログで、次の操作を実行します。

   1. 設定の「**タイトル**」を入力します。
   1. 「**Adobe Target 設定**」テンプレートを選択します。
   1. 「**作成**」をクリックします。

   編集ダイアログが開きます。

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   >
   >AEM で A4T を設定する際には、「設定の参照が欠落しています」というエントリが表示される場合があります。分析フレームワークを選択できるようにするには、次の操作を行います。
   >
   >1. **ツール**／**一般**／**CRXDE Lite** に移動します。
   >1. **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig** に移動します。
   >1. プロパティ **無効化** を **false** に設定します。
   >1. 「**すべて保存**」をクリックします。

1. ダイアログで、次のプロパティの値を入力します。

   * **クライアントコード**：Target アカウントのクライアントコード
   * **メール**：Target アカウントのメール
   * **パスワード**：Target アカウントのパスワード
   * **API のタイプ**：REST または XML
   * **A4T Analytics クラウド設定**：ターゲットアクティビティの目標と指標に使用する Analytics クラウド設定を選択します。この設定は、コンテンツをターゲティングするときに、Adobe Analytics をレポートソースとして使用している場合に必要です。クラウド設定が表示されない場合は、[A4T Analytics クラウドの設定](#configuring-a-t-analytics-cloud-configuration)のメモを参照してください。

   * **正確なターゲット設定を使用**：デフォルトでは、このチェックボックスはオンになっています。選択した場合、クラウドサービス設定は、コンテキストの読み込みを待ってからコンテンツを読み込みます。次のメモを参照してください。
   * **Adobe Target からセグメントを同期：** Target で定義されているセグメントをダウンロードして AEM で使用するには、このオプションをオンにします。API Type プロパティが REST の場合は、このオプションを選択する必要があります。インラインセグメントはサポートされず、Target のセグメントを使用する必要があるからです。（AEM の用語「セグメント」は、Target の「オーディエンス」と同じです。）
   * **クライアントライブラリ：**&#x200B;クライアントライブラリとして mbox.js と AT.js のいずれを使用するかを選択します。
   * **DTM を使用してクライアントライブラリを提供** - AT.js または mbox.js を DTM または別のタグ管理システムから使用する場合は、このオプションを選択します。このオプションを使用するには、[DTM 統合](/help/sites-administering/dtm.md)を設定します。ライブラリの配信には AEM ではなく DTM を使用することをお勧めします。
   * **カスタム mbox.js**：DTM ボックスをオンにした場合またはデフォルトの mbox.js を使用する場合は空にします。それ以外の場合は、カスタム mbox.js をアップロードします。mbox.js を選択した場合にのみ表示されます。
   * **カスタム AT.js**：DTM ボックスをオンにした場合またはデフォルトの AT.js を使用する場合は空にします。それ以外の場合は、カスタム AT.js をアップロードします。AT.js を選択した場合にのみ表示されます。

   >[!NOTE]
   >
   >デフォルトでは、Adobe Target 設定ウィザードをオプトインすると、正確なターゲット設定が有効になります。
   >
   >正確なターゲティングとは、クラウドサービスの設定が、コンテキストの読み込みを待ってからコンテンツを読み込むことを意味します。その結果、パフォーマンスに関しては、正確なターゲティングによって、コンテンツを読み込む前に数ミリ秒の遅延が生じる場合があります。
   >
   >正確なターゲティングは、オーサーインスタンスで常に有効になっています。ただし、パブリッシュインスタンスでは、クラウドサービス設定（**http://localhost:4502/etc/cloudservices.html**）の「正確なターゲティング」の横にあるチェックマークをオフにすることで、正確なターゲティングをグローバルにオフにできますまた、クラウドサービス設定での設定に関係なく、個々のコンポーネントに対して正確なターゲティングのオン／オフを切り替えることもできます。
   >
   >この設定を変更しても、作成済みの対象コンポーネントには影響しません&#x200B;***。***&#x200B;これらのコンポーネントを直接変更します。

1. 「**Target に接続**」をクリックして、Target との接続を開始します。接続に成功すると、「**接続に成功しました**」というメッセージが表示されます。メッセージの「**OK**」をクリックして、ダイアログの「**OK**」をクリックします。

   Target に接続できない場合は、[トラブルシューティング](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems)の節を参照してください。

### Target フレームワークの追加 {#adding-a-target-framework}

Target クラウド設定を設定したら、Target フレームワークを追加します。このフレームワークは、使用可能な [Client Context](/help/sites-administering/client-context.md) コンポーネントまたは [ContextHub](/help/sites-developing/ch-configuring.md) コンポーネントから Adobe Target に送信されるデフォルトのパラメーターを識別します。Target は、パラメーターを使用して、現在のコンテキストに適用されるセグメントを決定します。

1 つの Target 設定に対して複数のフレームワークを作成できます。Web サイトのセクションごとに異なるパラメーターセットを Target に送信する必要がある場合は、複数のフレームワークが便利です。送信するパラメーターのセットごとにフレームワークを作成します。Web サイトの各セクションを適切なフレームワークに関連付けます。1 つの web ページは一度に 1 つのフレームワークしか使用できません。

1. Target 設定ページで、「使用できるフレームワーク」の横の「**+**」（プラス符号）をクリックします。
1. フレームワークを作成ダイアログで、「**タイトル**」を指定し、「**Adobe Target フレームワーク**」を選択して、「**作成**」をクリックします。

   ![フレームワークを作成ダイアログ](assets/chlimage_1-161.png)

   フレームワークページが表示されます。サイドキックに、マッピングできる [ClientContext](/help/sites-administering/client-context.md) または [ContextHub](/help/sites-developing/ch-configuring.md) の情報を表すコンポーネントが表示されます。

   ![フレームワークのコンポーネント](assets/chlimage_1-162.png)

1. マッピングに使用するデータを表す ClientContext コンポーネントをドロップターゲットにドラッグします。または、**ContextHub ストア**&#x200B;コンポーネントをフレームワークにドラッグします。

   >[!NOTE]
   >
   >マッピング時に、パラメーターは単純な文字列を使用して mbox に渡されます。ContextHub から配列をマッピングすることはできません。

   例えば、サイト訪問者に関する&#x200B;**プロファイルデータ**&#x200B;を使用して Target キャンペーンを管理するには、**プロファイルデータ**&#x200B;コンポーネントをページにドラッグします。Target パラメーターへのマッピングに使用できるプロファイルデータ変数が表示されます。

   ![プロファイルデータ](assets/chlimage_1-163.png)

1. 該当する列の「**共有**」チェックボックスをオンにして、Adobe Target システムで表示する変数を選択します。

   ![共有](assets/chlimage_1-164.png)

   >[!NOTE]
   >
   >パラメーターの同期は、AEM から Adobe Target への一方向のみです。

フレームワークが作成されました。フレームワークをパブリッシュインスタンスにレプリケートするには、サイドキックの「**フレームワークをアクティベート**」オプションを使用します。

### アクティビティと Target クラウド設定の関連付け  {#associating-activities-with-the-target-cloud-configuration}

[AEM アクティビティ](/help/sites-authoring/activitylib.md)を Target クラウド設定に関連付け、アクティビティを [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=ja) にミラーリングできるようにします。

>[!NOTE]
>
>使用可能なアクティビティの種類は、次のオプションによって決まります。
>
>
>* Adobe Target の接続に AEM 側で使用される Adobe Target テナント（clientcode）で **xt_only** オプションがオンになっている場合は、XT アクティビティ&#x200B;**のみ**&#x200B;を AEM で作成できます。
>
>* Adobe Target テナント（clientcode）で **xt_only** オプションが&#x200B;**オフ**&#x200B;になっている場合は、XT アクティビティと A/B アクティビティの&#x200B;**両方**&#x200B;を AEM で作成できます。
>
>**追加のメモ：****xt_only** オプションは、特定の Target テナント（クライアントコード）に対して適用される設定であり、Adobe Target 内でのみ直接変更できます。このオプションは AEM で有効および無効にすることはできません。

### Target フレームワークとサイトの関連付け {#associating-the-target-framework-with-your-site}

AEM で Target フレームワークを作成した後、web ページをフレームワークに関連付けます。ページ上のターゲットコンポーネントは、フレームワークで定義されたデータをトラッキングするために Adobe Target に送信します。（[コンテンツのターゲティング](/help/sites-authoring/content-targeting-touch.md)を参照）。

ページをフレームワークに関連付けると、子ページが関連付けを継承します。

1. **Sites** コンソールで、設定するサイトに移動します。
1. [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)または[選択モード](/help/sites-authoring/basic-handling.md)を使用して、「**プロパティを表示**」を選択します。
1. 「**クラウドサービス**」タブを選択します。
1. 「**編集**」をクリックします。
1. 「**クラウドサービス設定**」で「**設定を追加**」をクリックして、「**Adobe Target**」を選択します。

   ![設定を追加](assets/chlimage_1-165.png)

1. 「**設定の参照**」で必要なフレームワークを選択します。

   >[!NOTE]
   >
   >作成の基になった Target クラウド設定ではなく、作成した固有の&#x200B;**フレームワーク**&#x200B;を選択してください。

1. 「**完了**」をクリックします。
1. Web サイトのルートページをアクティベートして、公開サーバーにレプリケーションします。（[ページを公開する方法](/help/sites-authoring/publishing-pages.md)を参照）

   >[!NOTE]
   >
   >ページにアタッチしたフレームワークがまだアクティベートされていなかった場合は、ウィザードが開き、フレームワークを公開することもできます。

## Target の接続に関する問題のトラブルシューティング {#troubleshooting-target-connection-problems}

Target に接続する際に発生する問題のトラブルシューティングを行うには、次のタスクを実行します。

* 入力したユーザー資格情報が正しいことを確認します。
* AEM インスタンスが Target サーバーに接続できることを確認します。例えば、ファイアウォールのルールが AEM のアウトバウンド接続をブロックしていないこと、または AEM が必要なプロキシを使用するように設定されていることを確認します。
* AEM のエラーログで参考になるメッセージを探します。error.log ファイルは、AEM がインストールされている **crx-quickstart/logs** ディレクトリにあります。
* Adobe Target でアクティビティを編集すると、URL は localhost を指します。この問題を回避するには、AEM Externalizer を正しい URL に設定してください。
