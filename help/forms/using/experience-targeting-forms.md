---
title: AEM Forms でターゲット設定されたエクスペリエンスを作成する
seo-title: AEM Forms でターゲット設定されたエクスペリエンスを作成する
description: AEM Forms の Target を使用して、対象となる顧客向けにカスタマイズされたエクスペリエンスを作成します。
seo-description: AEM Forms の Target を使用して、対象となる顧客向けにカスタマイズされたエクスペリエンスを作成します。
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 31%

---


# AEM Forms でターゲット設定されたエクスペリエンスを作成する {#create-targeted-experiences-in-aem-forms}

## Integrate Adobe Target with AEM Forms {#integrate-adobe-target-with-aem-forms}

Adobe Target は AEM と統合されて、対象オーディエンスに向けてカスタマイズされたエクスペリエンスを作成することが可能になりました。Adobe Target では、対象ユーザーに向けて A/B テストを作成し、ユーザーの反応を評価し、カスタマイズされた Web コンテンツを生成します。Adobe TargetとAEM Formsを、アダプティブフォームのターゲット画像コンポーネントやインタラクティブコミュニケーションに統合できます。

AEMでAdobe Targetを設定し、アダプティブフォームとインタラクティブな通信で使用するようにします。「AEMでの [ターゲット設定の作成](/help/sites-administering/target.md) 」と「フレームワーク [](/help/sites-administering/target.md)」を参照してください。

>[!NOTE]
>
>ターゲット設定は、アダプティブフォームまたはインタラクティブな通信がホスト名またはIPアドレスを使用してレンダリングされる場合に機能します。 アダプティブフォームまたはインタラクティブな通信がローカルホストを使用してレンダリングされると、失敗します。

## Target アクティビティを作成する {#creating-a-target-activity}

1. **Adobe Experience Manager/パーソナライゼーション/アクティビティ**&#x200B;をタップします。

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. In the Activities page, tap **Create > Create Brand**.
1. テンプレートを選択し、プロパティを入力します。

   Select a template, tap **Next.** 「プロパティ」セクションにブランドのタイトルを入力し、「 **作成」をタップします。**
ブランドがアクティビティページに表示されます。

1. アクティビティページのブランドをタップします。
1. In Master Area of your brand, tap **Create** > **Create Activity**.

   アクティビティを作成したら、その詳細、対象、および設定を指定します。

   詳細セクションには、名前、対象のエンジン、および目的が含まれます。対象のエンジンとして Adobe Target を選択した場合、Target のクラウド設定オプションが有効になります。Choose your Target cloud configuration, choose Activity type, provide the objective of the activity, and tap **Next**. Interactive Communicationは、エクスペリエンスのターゲット設定のアクティビティタイプのみをサポートします。

   Target セクションでは、オーディエンスのエクスペリエンスを追加し、名前を付けることができます。Click **Add Experience** to enable the **Select Audience** and **Name Experience** options. Tap **Select Audience** to see a list of audiences and their source. オーディエンス名のリストからオーディエンスを選択します。Tap **Add Experience** to name the experience, and tap **Next**.

   「目標と設定」セクションでは、アクティビティのスケジュールと優先度の設定ができます。Set the start date, end date, and priority of the activity, goal metric, additional metric and tap **Save**.

   アクティビティが、ブランドページのリストに表示されました。

   >[!NOTE]
   >
   >「アクティビティは保存されましたが、ターゲットに同期されていません。 理由：「次のエクスペリエンスにはオファーがありません」というエラーが発生した場合は、アクティビティを保存する際にエラーが発生します。

1. ターゲットを有効にするには、.jspファイルを編集し、アダプティブフォームテンプレートで使用するクライアントライブラリを含めます。

   For example, in the out-of-the-box implementation, click **Tools** >  **CRXDE Lite**.

   CRXDE Liteのアドレスバーに/libs/fd/af/components/page/base/head.jspと入力し、head.jspファイルを編集します。

   この実装では、simpleEnrollmentテンプレートを使用します。 この実装では、head.jspファイルを変更して次のクライアントライブラリを含めます。

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. アダプティブフォームのターゲットフレームワークを有効にするには、フォームまたはインタラクティブな通信に移動し、編集モードで開きます。

   To open a form or interactive communication in edit mode, tap **Select** and then tap **Open**.

   または、フォームまたはインタラクティブなコミュニケーションアイコンを選択せずにポインターをフォーム上に移動すると、4つのボタンが表示されます。 You can tap the **Edit** button that appears, to open the form in edit mode.

1. In the page toolbar, tap **Page Information** ![theme-options](assets/theme-options.png) > **Open Properties**.
1. 「一般」タブで、 **Adobe Target** フィールドの設定を選択します。 「**保存して閉じる**」をタップします。

## 作成したアクティビティをアダプティブフォームの画像またはインタラクティブな通信画像に適用する {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. アダプティブフォームとインタラクティブな通信を開いて編集します。 対話型の通信を開く場合は、Webチャネルを開きます。

1. インタラクティブな通信またはアダプティブフォームのオーサリングモードで、ターゲットにする画像を追加します。

   >[!NOTE]
   >
   >AEM Formsは、画像コンポーネントのターゲット設定のみをサポートしています。 画像コンポーネントをホストするパネルに他のコンポーネントが含まれていないこと、およびパネルの列数が1に設定されていることを確認します。

1. 「 **編集** 」から「 **ターゲット** 」モードに切り替えます。 モードを切り替えるオプションは、右上隅付近にあります。
1. ブ **ランドを選択し、「**&#x200B;アクティビティ **」を選択して、「**&#x200B;開始のターゲット設定 ****」をタップします。 エディターの右側に **オーディエンス** (Editors)メニューが表示されます。

   ![ターゲットメニュー](assets/targeting-menu.png)

1. オーディエンスメニューからオーディエンスを選択し、 **** ・ターゲットをタップします。 メニューが表示されます。 メニューで、「 **ターゲット**」をタップします。 画像をタップし、「 **設定**」をタップします。 プロパティウィンドウで、選択したオーディエンスに対して表示する画像を選択します。 すべてのオーディエンスに対して手順を繰り返します。 エクスペリエンスのターゲット設定は、インタラクティブな通信またはアダプティブフォームの画像に対して有効になります。

## 作成したアクティビティと Target サーバーとの同期を確認する {#check-if-the-created-activity-syncs-with-the-target-server}

ターゲット設定に使用したアクティビティは、Target サーバーと同期します。アクティビティが Target サーバーと同期しているか確認するには、ブランドページでアクティビティのステータスを確認します。

アクティビティのステータスが同期していることを確認してください。

## Target の動作を検証する {#validate-target-behavior}

Target の動作は次のように検証します。

* Use targeting with `wcmmode preview` in the author mode
* Use targeting with `wcmmode preview` and `wcmmode disabled` in the publish mode

## 画像コンポーネントのターゲット設定を監視する {#monitor-targeting-for-the-image-component}

フォームの画像コンポーネントのターゲット設定を監視するには、画像、アクティビティ、アダプティブフォームを発行します。

## 未解決の問題 {#open-issues}

表示式のフォーカスの設定は、アダプティブフォームでターゲット設定された画像では機能しません。
