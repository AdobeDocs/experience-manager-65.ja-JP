---
title: Microsoft&reg；に接続中翻訳者
description: AEMをMicrosoft&reg；に接続する方法を説明します。翻訳者。
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 13%

---

# Microsoft® Translator への接続{#connecting-to-microsoft-translator}

Microsoft® Translator クラウドサービスの設定を作成し、Microsoft® Translation アカウントを使用してAEMページのコンテンツ、コミュニティのコンテンツまたはアセットを翻訳します。

| プロパティ | 説明 |
|---|---|
| 翻訳ラベル | 翻訳サービスの表示名。 |
| 翻訳の帰属 | （オプション）ユーザー生成コンテンツの場合に、翻訳済みのテキストの横に表示される帰属情報（例：「`Translations by Microsoft`」）。 |
| ワークスペース ID | （オプション）使用するカスタマイズされたMicrosoft® Translator エンジンの ID。 |
| サブスクリプションキー | Microsoft® Translator のMicrosoft®購読キー。 |

設定を作成した後、次の操作を行う必要があります。 [有効化](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

次の手順では、タッチ操作向け UI を使用して、Microsoft® Translator 設定を作成します。

1. レールで、ツール/Cloud Servicesをクリックまたはタップします。
1. 「Microsoft®トランスレーター」領域で、「設定を表示」を選択します。
1. 「利用可能な設定」の横の「 + 」リンクをクリックします。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 設定のタイトルを入力します。タイトルは、設定コンソールおよびページプロパティのCloud Servicesドロップダウンリストでの設定を識別します。 デフォルトの名前はタイトルに基づいています。 オプションとして、設定を格納するリポジトリノードに使用する名前を入力します。リポジトリノードのパスである Parent Configuration プロパティのデフォルト値を使用します。
1. 「作成」をクリックします。
1. 表示されるダイアログボックスで、プロパティの値を入力し、「OK」をクリックします。

## Microsoft® TranslatorCloud Service設定の例 {#sample-microsoft-translator-cloud-service-configurations}

次のMicrosoft® Translator クラウドサービス設定が、Geometrixxサンプルと共にインストールされています。一部の設定例では、1 ヶ月あたり最大 2,000,000 個の無料翻訳文字を使用できる体験版Microsoft®翻訳アカウントを使用しています。

### Microsoft® Translator 体験版ライセンス {#microsoft-translator-trial-license}

Microsoft® Translator 体験版ライセンス設定は、Geometrixx Outdoorsサンプルパッケージと共にインストールされるサンプル設定です。この設定では、1 ヶ月に 2000,000 文字の翻訳が可能な無料のサブスクリプションを持つMicrosoft® Translator アカウントを使用します。

### Microsoft® Translator 体験版ライセンス —Geometrixxアウトドア {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft® Translator 体験版ライセンス —Geometrixxアウトドア設定は、Geometrixx Outdoorsと共にインストールされるサンプル設定です。 この設定では、Microsoft® Translator 体験版ライセンス設定と同じ無料のMicrosoft® Translator アカウントが使用されます。 アカウントには、1 か月に 200 万文字の翻訳を行うことができる無料サブスクリプションが付属します。

このMicrosoft® Translator 設定は、Geometrixx Outdoorsサンプルサイトのコンテンツのタイプに合わせて最適化されています。

### Microsoft® Translator 体験版ライセンス設定のアップグレード {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft®翻訳設定ページには、実稼動システムに適したアカウントのサブスクリプションを取得するための、Microsoft® Web サイトへの便利なリンクが用意されています。

1. レールで、ツール/操作/クラウド/Cloud Servicesをクリックまたはタップします。
1. 「Microsoft® Translator」領域で、「設定を表示」をクリックまたはタップし、「Microsoft® Translator 体験版ライセンス (Microsoft®翻訳設定 )」をクリックまたはタップします。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 設定ページで、「購読をアップグレード」をクリックします。 開いたMicrosoft® Web ページを使用して、アカウントを設定します。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Microsoft® Translator Engine のカスタマイズ {#customizing-your-microsoft-translator-engine}

Microsoft®翻訳設定ページには、Microsoft® Translator エンジンをカスタマイズするための、Microsoft® Web サイトへの便利なリンクが表示されます。 ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. レールで、ツール/操作/クラウド/Cloud Servicesをクリックまたはタップします。
1. Microsoft® Translator 領域で、「設定を表示」をクリックまたはタップし、カスタマイズする設定をクリックまたはタップします。
1. 設定ページで、「トランスレータをカスタマイズ」(Customize Translator) をクリックします。 開いたMicrosoft® Web ページを使用して、サービスをカスタマイズします。

## Translator サービス設定のアクティベート {#activating-the-translator-service-configurations}

パブリッシュインスタンスにレプリケートされた翻訳済みコンテンツをサポートするには、クラウドサービス設定をアクティベートします。 Microsoft® Translator またはサードパーティのクラウドサービス設定を保存するリポジトリノードをアクティベートするには、次の方法を使用します。 [セクション全体（ツリー）のアクティブ化](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). このノードは以下に示す親ノードの下にあります。

* Microsoft®翻訳サービス：/libs/settings/cloudconfigs/translation/msft-translation
* サードパーティ翻訳：/etc/cloudservices/machine-translation
