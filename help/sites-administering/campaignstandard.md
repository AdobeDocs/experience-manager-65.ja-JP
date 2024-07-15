---
title: AEM 6.5 と Adobe Campaign Standard の統合
description: AEM 6.5 を Adobe Campaign Standard と統合する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 100%

---


# AEM 6.5 と Adobe Campaign Standard の統合 {#integrating-with-adobe-campaign-standard}

AEM 6.5 を Adobe Campaign Standard（ACS）と統合すると、メール配信、コンテンツ、フォームを AEM で直接管理できます。ソリューション間の双方向通信を有効にするには、Adobe Campaign Standard と AEM の両方で設定手順が必要です。

この統合により、AEM と Adobe Campaign Standard を個別に使用できます。マーケターは Adobe Campaign でキャンペーンを作成してターゲティングを使用できますが、コンテンツ作成者は並行して AEM でコンテンツのデザインに取り組むことができます。この統合により、AEM 内に作成されたキャンペーンのコンテンツとデザインを、Adobe Campaign でターゲットにして配信できるようになります。

>[!INFO]
>
>このドキュメントでは、Adobe Campaign Standard を AEM 6.5 と統合する方法について詳しく説明します。その他の Campaign 統合については、[AEM 6.5 と Adobe Campaign の統合](campaign.md)のドキュメントを参照してください。

## 統合手順 {#integration-steps}

AEM と Adobe Campaign Standard 間の統合を設定するには、両方のソリューションでいくつかの手順が必要です。

1. [を設定 ](#aemserver-user)
1. [を確認 ](#resource-type-filter)
1. [Campaign で AEM 固有のメール配信テンプレートを作成](#aem-email-delivery-template)
1. [AEM で Campaign 統合を設定](#campaign-integration)
1. [AEM パブリッシュインスタンスへのレプリケーションを設定](#replication)
1. [AEM Externalizer を設定](#externalizer)
1. [を設定 ](#campaign-remote-user)
1. [Campaign で AEM 外部アカウントを設定](#acc-external-user)

このドキュメントでは、これらの各手順を詳しく説明します。

## 前提条件 {#prerequisites}

* Adobe Campaign Standard への管理者アクセス
   * Adobe Campaign Standard のセットアップおよび設定方法について詳しくは、[Adobe Campaign Standard ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html?lang=ja)を参照してください。
* AEM への管理者アクセス

## Campaign で aemserver ユーザーを設定 {#aemserver-user}

Adobe Campaign Standard には、AEM が Adobe Campaign に接続する際に使用する `aemserver` ユーザーが、デフォルトで付属しています。このユーザーに適切なセキュリティグループを割り当て、パスワードを設定します。

1. 管理者として Adobe Campaign にログインします。

1. メニューバーの左上にある Adobe Campaign ロゴをクリックしてグローバルナビゲーションを開き、ナビゲーションメニューから、**管理**／**ユーザーとセキュリティ**／**ユーザー**&#x200B;を選択します。

1. コンソールの `aemserver` ユーザーをクリックします。

1. `aemserver` ユーザーが、少なくとも、役割 `deliveryPrepare` が割り当てられたセキュリティグループに割り当てられていることを確認します。デフォルトでは、`Standard Users` グループはこの役割を持っています。

   ![Adobe Campaign の aemserver ユーザー](assets/acs-aemserver-user.png)

1. 「**保存**」をクリックして、変更を保存します。

`aemserver` ユーザーに、AEM が Adobe Campaign と通信するために必要な権限が付与されました。

ただし、AEMが `aemserver` ユーザーを使用する前に、そのパスワードを設定する必要があります。 これは、Adobe Campaign では実行することができません。この作業は、アドビのサポートエンジニアが行う必要があります。[アドビカスタマーケアでチケットを発行](https://experienceleague.adobe.com/?lang=ja&amp;support-tab=home#support)して、`aemserver` パスワードのリセットをリクエストします。パスワードをアドビカスタマーケアから取得したら、安全な場所に保管します。

## Campaign の AEMResourceTypeFilter を確認 {#resource-type-filter}

`AEMResourceTypeFilter` は、Adobe Campaign で使用できる AEM リソースのフィルタリングに使用する、Adobe Campaign のオプションです。 AEM には多くのコンテンツが含まれているため、このオプションは、Adobe Campaign で使用するために特別に設計されたタイプの AEM コンテンツのみを Adobe Campaign が取得できるようにするフィルターとして機能します。

このオプションは事前設定済みです。 ただし、AEM の Campaign コンポーネントをカスタマイズしている場合は、アップデートが必要になる場合があります。 `AEMResourceTypeFilter` オプションが設定されていることを確認するには、次の手順に従います。

1. 管理者として Adobe Campaign にログインします。

1. メニューバーの左上にある Adobe Campaign ロゴをクリックしてグローバルナビゲーションを開き、ナビゲーションメニューから、**管理**／**アプリケーション設定**／**オプション**&#x200B;を選択します。

1. オプションコンソールで「`AEMResourceTypeFilter`」をクリックします。

1. `AEMResourceTypeFilter` の設定を確認します。パスはコンマで区切られ、デフォルトでは次の値が含まれます。

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMResourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. 「**保存**」をクリックして、変更を保存します。

これで `AEMResourceTypeFilter` は、AEM から正しいコンテンツを取得するように設定されました。

## Campaign で AEM 固有のメール配信テンプレートを作成 {#aem-email-delivery-template}

デフォルトでは、AEM 機能は、Adobe Campaign のメールテンプレートでは有効になっていません。AEM コンテンツを使用したメール作成に使用できる、新しいメール配信テンプレートを設定します。AEM 固有のメール配信テンプレートを作成するには、次の手順に従います。

1. 管理者として Adobe Campaign にログインします。

1. メニューバーの左上にある Adobe Campaign ロゴをクリックしてグローバルナビゲーションを開き、ナビゲーションメニューで、**リソース**／**テンプレート**／**配信テンプレート**&#x200B;を選択します。

1. 配信テンプレートコンソールで、デフォルトのメールテンプレートである&#x200B;**電子メール（メール）で送信**&#x200B;を探し、そのカード（または行）の上にマウスを置いてオプションを表示します。「**要素を複製**」をクリックします。

   ![要素を複製](assets/acs-copy-template.png)

1. **確認**&#x200B;ダイアログで、「**確認**」をクリックしてテンプレートを複製します。

   ![確認ダイアログ](assets/acs-confirmation.png)

1. **電子メール（メール）で送信**&#x200B;テンプレートのコピーを使用して、テンプレートエディターが開きます。ウィンドウの右上にある「**プロパティを編集**」アイコンをクリックします。

   ![テンプレートエディター](assets/acs-template-editor.png)

1. プロパティウィンドウで、新しい AEM テンプレートの内容を説明するよう「**ラベル**」フィールドを変更します。

1. **コンテンツ**&#x200B;見出しをクリックして展開し、「**コンテンツソース**」ドロップダウンで「**Adobe Experience Manager**」を選択します。

1. これにより、「**Adobe Experience Manager アカウント**」フィールドが表示されます。ドロップダウンを使用して、「**Adobe Experience Manager インスタンス (aemInstance)**」ユーザーを選択します。これは、AEM 統合環境用のデフォルトの外部ユーザーです。

![テンプレートのプロパティの設定](assets/acs-template-properties.png)

1. 「**確認**」をクリックして、プロパティへの変更内容を保存します。

1. テンプレートエディターで、「**保存**」をクリックして、AEM で使用するメールテンプレートの変更済みコピーを保存します。

これで、AEM コンテンツを使用できるメールテンプレートが作成されました。

## AEM で Campaign 統合を設定 {#campaign-integration}

AEM は、組み込まれた統合機能と、Adobe Campaign で設定した `aemserver` ユーザーを使用して Adobe Campaign と通信します。この統合を設定するには、次の手順に従います。

1. AEM オーサリングインスタンスに管理者としてログインします。

1. グローバルナビゲーションサイドレールから、**ツール**／**クラウドサービス**／**従来のクラウドサービス**／**Adobe Campaign** を選択し、「**今すぐ設定**」をクリックします。

   ![Adobe Campaign の設定](assets/configure-campaign-service.png)

1. ダイアログで、**タイトル**&#x200B;を入力して Campaign サービス設定を作成し、「**作成**」をクリックします。

   ![Campaign の設定ダイアログ](assets/configure-campaign-dialog.png)

1. 設定を編集するための新しいウィンドウとダイアログが開きます。必要な情報を入力します。

   * **ユーザー名** - これは、[前の手順で設定した、Adobe Campaign の `aemserver` ユーザーです。](#aemserver-user)デフォルトでは `aemserver` です。
   * **パスワード** - これは、[前の手順でアドビカスタマーケアにリクエストした、Adobe Campaign の `aemserver` ユーザーのパスワードです。](#aemserver-user)
   * **API エンドポイント** - これは、Adobe Campaign インスタンス URL です。

   ![AEM での Adobe Campaign の設定](assets/configure-campaign.png)

1. 「**Adobe Campaign に接続**」を選択して接続を確認し、「**OK**」をクリックします。

AEM が Adobe Campaign と通信できるようになりました。

>[!NOTE]
>
>Adobe Campaign サーバーがインターネット経由で到達可能であることを確認してください。AEM はプライベートネットワークにアクセスできません。

## AEM パブリッシュインスタンスへのレプリケーションを設定 {#replication}

キャンペーンのコンテンツは、コンテンツ作成者が AEM オーサリングインスタンスで作成します。このインスタンスは通常、組織内でしか使用できません。画像やアセットなどのコンテンツをキャンペーンの受信者がアクセスできるようにするには、そのコンテンツを公開する必要があります。

レプリケーションエージェントは、AEM オーサーインスタンスからパブリッシュインスタンスにコンテンツを公開する役割を持ち、このエージェントが正しく機能するには統合環境に対して設定されている必要があります。また、この手順は、あるオーサーインスタンス設定をパブリッシュインスタンスにレプリケートするためにも必要です。

AEM オーサーインスタンスからパブリッシュインスタンスへのレプリケーションを設定するには、次の手順を実行します。

1. AEM オーサリングインスタンスに管理者としてログインします。

1. グローバルナビゲーションサイドパネルで、**ツール**／**デプロイメント**／**レプリケーション**／**オーサーのエージェント**&#x200B;を選択し、「**デフォルトエージェント (パブリッシュ)**」をクリックします。

   ![レプリケーションエージェントの設定](assets/acc-replication-config.png)

1. 「**編集**」をクリックして、「**トランスポート**」タブを選択します。

1. デフォルトの `localhost` 値を AEM パブリッシュインスタンスの IP アドレスに置き換えて、「**URI**」フィールドを設定します。

   ![「トランスポート」タブ](assets/acc-transport-tab.png)

1. 「**OK**」をクリックして、エージェント設定の変更内容を保存します。

AEM パブリッシュインスタンスへのレプリケーションを設定したので、キャンペーン受信者がコンテンツにアクセスできるようになりました。

>[!NOTE]
>
>レプリケーション URL を使用せずに、公開 URL を使用する場合は、OSGi を介して、以下の設定で公開 URL を設定することができます
>
>グローバルナビゲーションサイドパネルで、**ツール**／**運用**／**Web コンソール**／**OSGi 設定** を選択し、**AEM Campaign の統合 - 設定**&#x200B;を検索します。設定を編集し、「**公開 URL**（`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`）」フィールドを変更します。

## AEM Externalizer の設定 {#externalizer}

[Externalizer は リソースパスを外部および絶対 URL に変換する AEMの OSGi サービスです。この URL は、AEM が Campaign で使用できるコンテンツを提供するために必要です。](/help/sites-developing/externalizer.md)Campaign の統合が機能するように設定します。

1. AEM オーサリングインスタンスに管理者としてログインします。
1. グローバルナビゲーションサイドパネルで、**ツール**／**運用**／**Web コンソール**／**OSGi 設定**&#x200B;を選択し、**Day CQ Link Externalizer**&#x200B;を検索します。
1. デフォルトでは、「**ドメイン**」フィールドの最新エントリは、公開インスタンスを対象としています。 URL をデフォルトの `http://localhost:4503` から、公開されているパブリッシュインスタンスに変更します。

   ![Externalizer の設定](assets/acc-externalizer-config.png)

1. 「**保存**」をクリックします。

Externalizer が設定され、Adobe Campaign がコンテンツにアクセスできるようになりました。

>[!NOTE]
>
パブリッシュインスタンスは、Adobe Campaign サーバーからアクセス可能である必要があります。`localhost:4503` または Adobe Campaign が到達できない別のサーバーを指している場合、AEM からの画像は Adobe Campaign コンソールに表示されません。

## AEM での campaign-remote ユーザーを設定 {#campaign-remote-user}

AEM が Adobe Campaign と通信する際に使用する Adobe Campaign のユーザーが必要であるのと同様に、Adobe Campaign が AEM と通信するには、AEM のユーザーも必要です。デフォルトでは、Campaign 統合によって AEM に `campaign-remote` ユーザーが作成されます。次の手順に従って、このユーザーを設定します。

1. AEM に管理者としてログインします。
1. メインナビゲーションコンソールで、左側のパネルにある「**ツール**」をクリックします。
1. 次に、**セキュリティ**／**ユーザー**&#x200B;をクリックして、ユーザー管理コンソールを開きます。
1. `campaign-remote` ユーザーを見つけます。
1. `campaign-remote` ユーザーを選択し、「**プロパティ**」をクリックしてユーザーを編集します。
1. **ユーザー設定を編集**&#x200B;ウィンドウで、「**パスワードを変更**」をクリックします。
1. ユーザーの新しいパスワードを入力し、今後の使用のために安全な場所にパスワードをメモします。
1. 「**保存**」をクリックして、パスワードの変更を保存します。
1. 「**保存して閉じる**」をクリックして、変更を `campaign-remote` ユーザーに保存します。

## Campaign で AEM 外部アカウントを設定 {#acc-external-user}

[AEM 固有のメール配信テンプレートを作成](#aem-email-delivery-template)した場合、テンプレートが `aemInstance` 外部アカウントを使用して AEM と通信する必要があると指定したことになります。両方のソリューション間で双方向通信を有効にするには、Adobe Campaign でこのアカウントを設定する必要があります。

1. 管理者として Adobe Campaign にログインします。

1. メニューバーの左上にある Adobe Campaign ロゴをクリックしてグローバルナビゲーションを開き、ナビゲーションメニューから、**管理**／**アプリケーション設定**／**外部アカウント**&#x200B;を選択します。

1. ユーザーコンソールの **Adobe Experience Manager インスタンス（aemInstance）**&#x200B;をクリックします。

1. ユーザーが **Adobe Experience Manager** を&#x200B;**タイプ**&#x200B;として持っていることを確認します。

1. 「**接続**」セクションで、次のフィールドを定義します。

   1. サーバー：これは AEM オーサリングサーバーの URL です。 最後尾をスラッシュにしないでください。
   1. アカウント：これは [AEM で事前に設定した](#campaign-remote-user) `campaign-remote` ユーザーです。
   1. パスワード：これは、[AEM で事前に設定した](#campaign-remote-user) `campaign-remote` ユーザー用のパスワードです。

   ![aemInstance ユーザーの編集](assets/acs-external-acount-editor.png)

1. 「**有効**」チェックボックスが選択されていることを確認したら、「**保存**」をクリックして変更内容を保存します。

おめでとうございます。AEM と Adobe Campaign Standard の統合が完了しました。

## 次のステップ {#next-steps}

Adobe Campaign Classic と AEM の両方が設定されたので、統合は完了です。

Adobe Experience Manager でニュースレターを作成する方法については、[このドキュメント](/help/sites-authoring/campaign.md)の続きで説明します。
