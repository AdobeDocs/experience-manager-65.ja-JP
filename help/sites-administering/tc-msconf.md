---
title: Microsoft Translator への接続
seo-title: Connecting to Microsoft Translator
description: AEM を Microsoft Translator に接続する方法について説明します。
seo-description: Learn how to connect AEM to Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 100%

---

# Microsoft Translator への接続{#connecting-to-microsoft-translator}

Microsoft Translation アカウントを使用して AEM ページのコンテンツ、コミュニティのコンテンツまたはアセットを翻訳するには、Microsoft Translator クラウドサービス用の設定を作成します。

| プロパティ | 説明 |
|---|---|
| 翻訳ラベル | 翻訳サービスの表示名。 |
| 翻訳の帰属 | （オプション）ユーザー生成コンテンツの場合に、翻訳済みのテキストの横に表示される帰属情報（例：「`Translations by Microsoft`」）。 |
| ワークスペース ID | （オプション）使用するカスタム Microsoft Translator エンジンの ID。 |
| サブスクリプションキー | Microsoft Translator の Microsoft サブスクリプションキー。 |

設定を作成したら、その[設定をアクティベートする](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations)必要があります。

次の手順では、タッチ操作向け UI を使用して Microsoft Translator の設定を作成します。

1. パネルで、ツール／クラウドサービスをクリックまたはタップします。
1. 「Microsoft Translator」領域で、「設定を表示」をクリックまたはタップします。
1. 「利用可能な設定」の横にある + リンクをクリックします。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 設定のタイトルを入力します。このタイトルによって、クラウドサービスコンソールおよびページプロパティのドロップダウンリストで設定が識別されます。デフォルト名はタイトルに基づいて指定されます。オプションとして、設定を格納するリポジトリノードに使用する名前を入力します。リポジトリノードのパスである「親設定」プロパティにはデフォルト値を使用する必要があります。
1. 「作成」をクリックします。
1. 表示されるダイアログボックスで、プロパティの値を入力して「OK」をクリックします。

## Microsoft Translator クラウドサービスのサンプル設定 {#sample-microsoft-translator-cloud-service-configurations}

以下に示す Microsoft Translator クラウドサービスの設定が Geometrixx のサンプルと共にインストールされます。一部のサンプル設定では、Microsoft Translation の試用版アカウントを使用します。このアカウントを使用すると、1 か月に最大 200 万文字の翻訳を無料で行うことができます。

### Microsoft Translator 試用版ライセンス {#microsoft-translator-trial-license}

Microsoft Translator 試用版ライセンス設定は、Geometrixx Outdoors サンプルパッケージと共にインストールされるサンプル設定です。この設定では、1 か月に 200 万文字の翻訳を行うことができる無料サブスクリプションが付属する Microsoft Translator アカウントを使用します。

### Microsoft Translator 試用版ライセンス - Geometrixx-outdoors {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft Translator 試用版ライセンス - Geometrixx-outdoors 設定は、Geometrixx Outdoors サンプルパッケージと共にインストールされるサンプル設定です。この設定では、Microsoft Translator 試用版ライセンス設定と同じ無料の Microsoft Translator アカウントを使用します。アカウントには、1 か月に 200 万文字の翻訳を行うことができる無料サブスクリプションが付属します。

この Microsoft Translator 設定は、Geometrixx Outdoors サンプルサイトのコンテンツのタイプで使用するために最適化されます。

### Microsoft Translator 体験版ライセンス設定のアップグレード {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft Translation 設定ページには、実稼動システムに適したアカウントのサブスクリプションを取得する場合に役立つ、Microsoft web サイトへのリンクが表示されます。

1. レールで、ツール／操作／クラウド／クラウドサービスをクリックまたはタップします。
1. 「Microsoft Translator」領域で、「設定を表示」をクリックまたはタップして、「Microsoft Translator 試用版ライセンス (Microsoft Translation の設定)」をクリックまたはタップします。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 設定ページで、「購読をアップグレード」をクリックします。表示された Microsoft の Web ページを使用して、アカウントを設定します。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Microsoft Translator エンジンのカスタマイズ {#customizing-your-microsoft-translator-engine}

Microsoft Translation 設定ページには、Microsoft Translator エンジンをカスタマイズする場合に役立つ、Microsoft web サイトへのリンクが表示されます。（[https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/)）

1. レールで、ツール／操作／クラウド／クラウドサービスをクリックまたはタップします。
1. 「Microsoft Translator」領域で、「設定を表示」をクリックまたはタップして、カスタマイズする設定をクリックまたはタップします。
1. 設定ページで、「トランスレーターをカスタマイズ」をクリックします。表示された Microsoft の Web ページを使用して、サービスをカスタマイズします。

## 翻訳サービス設定のアクティベート {#activating-the-translator-service-configurations}

パブリッシュインスタンスでレプリケートされる翻訳コンテンツをサポートするには、クラウドサービス設定をアクティベートする必要があります。[セクション全体（ツリー）のアクティベート](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree)方法を使用して、Microsoft Translator またはサードパーティのクラウドサービスの設定を格納するリポジトリノードをアクティベートします。このノードは以下に示す親ノードの下にあります。

* Microsoft Translation サービス：/libs/settings/cloudconfigs/translation/msft-translation
* サードパーティ翻訳：/etc/cloudservices/machine-translation
