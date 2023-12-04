---
title: Microsoft Translator への接続
description: AEM を Microsoft Translator に接続して翻訳ワークフローを自動化する方法を説明します。
feature: Language Copy
role: Admin
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 80%

---

# Microsoft Translator への接続 {#connecting-to-microsoft-translator}

AEM ページのコンテンツまたはアセットの翻訳に Microsoft Translation アカウントを使用するには、[Microsoft Translator](https://www.microsoft.com/ja-jp/translator/business/) クラウドサービスの設定を作成します。

>[!NOTE]
>
>AEM には、毎月最大 2,000,000 文字の無料翻訳を利用できる体験版の Microsoft Translation アカウントが用意されています。実稼動システムに適したアカウントサブスクリプションを取得するには、[Microsoft Translator 体験版ライセンス設定のアップグレード](#upgrading-the-microsoft-translator-trial-license-configuration)を参照してください。

| プロパティ | 説明 |
|---|---|
| 翻訳ラベル | 翻訳サービスの表示名 |
| 翻訳の帰属 | （オプション）ユーザー生成コンテンツの場合、翻訳されたテキストの横に表示されるアトリビューション。例： `Translations by Microsoft` |
| ワークスペース ID | （オプション）使用するカスタム Microsoft Translator エンジンの ID |
| サブスクリプションキー | Microsoft Translator の Microsoft サブスクリプションキー |

設定を作成したら、その[設定をアクティベートする](#activating-the-translator-service-configurations)必要があります。

Microsoft Translator 設定を作成するには、次の手順に従います。

1. Adobe Analytics の [ナビゲーションパネル](/help/sites-authoring/basic-handling.md#first-steps) click **ツール** > **Cloud Service** > **翻訳Cloud Service**.
1. 設定を作成する場所に移動します。通常は、これはサイトのルートにあります。また、グローバルなデフォルト設定にすることもできます。
1. 次をクリック： **作成** 」ボタンをクリックします。
1. 設定を定義します。
   1. ドロップダウンで **Microsoft Translator** を選択します。
   1. 設定のタイトルを入力します。このタイトルによって、クラウドサービスコンソールおよびページプロパティのドロップダウンリストで設定が識別されます。
   1. オプションとして、設定を格納するリポジトリーノードに使用する名前を入力します。

   ![翻訳設定の作成](assets/create-translation-config.png)

1. 「**作成**」をクリックします。
1. **設定を編集**&#x200B;ウィンドウで、前述の表で説明した翻訳サービスの値を指定します。

   ![翻訳設定の編集](assets/edit-translation-config.png)

1. クリック **接続** 接続を確認します。
1. 「**保存して閉じる**」をクリックします。

## Microsoft Translator 体験版ライセンス設定のアップグレード {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft Translation 設定ページには、実稼動システムに適したアカウントのサブスクリプションを取得する場合に役立つ、Microsoft web サイトへのリンクが表示されます。

1. Adobe Analytics の [ナビゲーションパネル](/help/sites-authoring/basic-handling.md#first-steps) click **ツール** > **Cloud Service** > **翻訳Cloud Service**.
1. 既存のMicrosoft Translator 設定をクリックします。
1. クリック **編集**.
1. Adobe Analytics の **設定を編集** ウィンドウ、クリック **配信登録のアップグレード**. サービスの詳細を表示する Microsoft Web ページが開きます。

## Microsoft Translator エンジンのカスタマイズ {#customizing-your-microsoft-translator-engine}

Microsoft Translation 設定ページには、Microsoft Translator エンジンをカスタマイズする場合に役立つ、Microsoft Web サイトへのリンクが表示されます

1. Adobe Analytics の [ナビゲーションパネル](/help/sites-authoring/basic-handling.md#first-steps) click **ツール** > **Cloud Service** > **翻訳Cloud Service**.
1. 既存のMicrosoft Translator 設定をクリックします。
1. クリック **編集**.
1. Adobe Analytics の **設定を編集** ウィンドウ、クリック **Translator をカスタマイズ**. 表示された Microsoft の web ページを使用して、サービスをカスタマイズします。

## Translator サービス設定のアクティベート {#activating-the-translator-service-configurations}

パブリッシュインスタンスでレプリケートされる翻訳コンテンツをサポートするには、クラウドサービス設定をアクティベートする必要があります。[ツリーの公開](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree)方法を使用して、Microsoft Translator 設定を格納するリポジトリーノードをアクティベートします。このノードは以下に示す親ノードの下にあります。

* `/libs/settings/cloudconfigs/translation/msft-translation`
