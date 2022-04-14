---
title: AEM Forms でターゲット設定されたエクスペリエンスを作成する
seo-title: Create targeted experiences in AEM Forms
description: AEM Forms の Target を使用して、対象となる顧客向けにカスタマイズされたエクスペリエンスを作成します。
seo-description: Use Target in AEM Forms to create customized experiences for targeted customers.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '838'
ht-degree: 100%

---

# AEM Forms でターゲット設定されたエクスペリエンスを作成する {#create-targeted-experiences-in-aem-forms}

## Adobe Target を AEM Forms に統合する {#integrate-adobe-target-with-aem-forms}

Adobe Target は AEM と統合されて、対象オーディエンスに向けてカスタマイズされたエクスペリエンスを作成することが可能になりました。Adobe Target を使用して、対象ユーザーに向けて A/B テストの作成、ユーザーの反応の評価、カスタマイズされた web コンテンツの生成が可能です。Adobe Target を AEM Forms と統合して、アダプティブフォームやインタラクティブ通信の画像コンポーネントをターゲットに設定することができます。

AEM で Adobe Target を設定してアダプティブフォームやインタラクティブ通信で使用する場合は、 [AEM での Target 設定の作成](/help/sites-administering/target.md)および[フレームワークの追加](/help/sites-administering/target.md)を参照してください。

>[!NOTE]
>
>ターゲティングは、ホスト名または IP アドレスを使用してアダプティブフォームまたはインタラクティブ通信がレンダリングされたときに機能します。アダプティブフォームまたはインタラクティブ通信がローカルホストを使用してレンダリングされた場合は失敗します。

## Target アクティビティを作成する {#creating-a-target-activity}

1. **Adobe Experience Manager／パーソナライズ機能／アクティビティ**&#x200B;をタップします。

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. アクティビティページでは、**作成／ブランドを作成**&#x200B;をタップします。
1. テンプレートを選択し、プロパティを入力します。

   テンプレートを選択し、**次へをタップします。**「プロパティ」セクションでブランドのタイトルを入力し、「**作成」をタップします。**
ブランドがアクティビティページにリストされました。

1. アクティビティページのブランドをタップします。
1. ブランドのマスター領域で、**作成**／**アクティビティを作成**&#x200B;をタップします。

   アクティビティを作成したら、その詳細、対象、および設定を指定します。

   詳細セクションには、名前、対象のエンジン、および目的が含まれます。対象のエンジンとして Adobe Target を選択した場合、Target のクラウド設定オプションが有効になります。Target クラウド設定を選択し、アクティビティタイプを選択し、アクティビティの目的を入力してから、「**次へ**」をタップします。インタラクティブ通信は、エクスペリエンスのターゲット設定アクティビティタイプのみをサポートします。

   「Target」セクションでは、オーディエンスのエクスペリエンスを追加し、名前を付けることができます。「**エクスペリエンスを追加**」をクリックして、「**オーディエンスを選択**」および「**エクスペリエンスに名前を付ける**」オプションを有効にします。「**オーディエンスを選択**」をタップして、ソースのオーディエンスのリストを表示します。オーディエンス名のリストからオーディエンスを選択します。**エクスペリエンスを追加**&#x200B;をタップして、エクスペリエンスに名前を付け、**次へ**&#x200B;をタップします。

   「目標と設定」セクションでは、アクティビティのスケジュールと優先度の設定ができます。開始日、終了日、アクティビティの優先度、目標指標および追加の指標を設定し、「**保存**」をタップします。

   アクティビティが、ブランドページのリストに表示されました。

   >[!NOTE]
   >
   >アクティビティの保存時、次のエラーを無視することができます。「アクティビティは保存されましたが、Target に同期されませんでした。理由：次のエクスペリエンスにはオファーがありません」

1. ターゲットを有効にするには、.jsp ファイルを編集して、アダプティブフォームテンプレートで使用しているクライアントライブラリが組み込まれるようにします。

   例えば、標準の実装では、**ツール**／**CRXDE Lite** をクリックします。

   CRXDE Lite のアドレスバーで、/libs/fd/af/components/page/base/head.jsp と入力し、head.jsp ファイルの編集を行います。

   この実装では、simpleEnrollment テンプレートを使用します。この実装で、head.jsp ファイルを修正して以下のクライアントライブラリが組み込まれるようにします。

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. アダプティブフォームのターゲットフレームワークを有効にするには、フォームまたはインタラクティブ通信に移動し、編集モードで開きます。

   フォームまたはインタラクティブ通信を編集モードで開くには、**選択**&#x200B;をタップしてから、**開く**&#x200B;をタップします。

   または、フォームまたはインタラクティブ通信のアイコンを選択していない状態で、ポインターをその上に移動すると、4 つのボタンが表示されます。表示された「**編集**」ボタンをタップすると、フォームが編集モードで開きます。

1. ページツールバーで、**ページ情報** ![theme-options](assets/theme-options.png)／**プロパティを開く**&#x200B;をタップします。
1. 「一般」タブで、 「**Adobe Target**」フィールドの設定を選択します。 **保存して閉じる**&#x200B;をタップします。

## 作成したアクティビティをアダプティブフォームの画像またはインタラクティブ通信の画像に適用する {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. アダプティブフォームとインタラクティブ通信を編集用に開きます。 インタラクティブ通信を開く場合は、web チャネルを開きます。

1. インタラクティブ通信またはアダプティブフォームのオーサリングモードで、対象にする画像を追加します。

   >[!NOTE]
   >
   >AEM Forms は、画像コンポーネントのターゲティングのみをサポートしています。画像コンポーネントをホストするパネルに他のコンポーネントが含まれていないこと、およびパネルの列数が 1 に設定されていることを確認します。

1. **編集**&#x200B;モードから&#x200B;**ターゲティング**&#x200B;モードに切り替えます。モードを切り替えるオプションは、右上隅付近にあります。
1. 「**ブランド**」、「**アクティビティ**」の順に選択し、「**ターゲティングを開始**」をタップします。**オーディエンス**&#x200B;メニューがエディターの右側に表示されます。

   ![ターゲティングメニュー](assets/targeting-menu.png)

1. オーディエンスを&#x200B;**オーディエンス**&#x200B;メニューから選択し、ターゲットにする画像をタップします。メニューが表示されます。メニューで、「**ターゲット**」をタップします。画像をタップし、「**設定**」をタップします。プロパティウィンドウで、選択したオーディエンスに対して表示する画像を選択します。すべてのオーディエンスに対してこの手順を繰り返します。エクスペリエンスのターゲット設定は、インタラクティブ通信またはアダプティブフォーム内の画像に対して有効になります。

## 作成したアクティビティと Target サーバーとの同期を確認する {#check-if-the-created-activity-syncs-with-the-target-server}

ターゲット設定に使用したアクティビティは、Target サーバーと同期します。アクティビティが Target サーバーと同期しているか確認するには、ブランドページでアクティビティのステータスを確認します。

アクティビティのステータスが同期していることを確認してください。

## Target の動作を検証する {#validate-target-behavior}

Target の動作は次のように検証します。

* オーサーモードで `wcmmode preview` によるターゲティングを使用
* パブリッシュモードで `wcmmode preview` および `wcmmode disabled` によるターゲティングを使用

## 画像コンポーネントのターゲティングを監視する {#monitor-targeting-for-the-image-component}

フォームの画像コンポーネントのターゲティングを監視するには、画像、アクティビティ、アダプティブフォームを発行します。

## 未解決の問題 {#open-issues}

表示式のフォーカスの設定は、アダプティブフォームでターゲット設定された画像では機能しません。
