---
title: Microsoft&reg; Translator への接続
description: AEM を Microsoft® Translator に接続する方法について説明します。
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: ht
source-wordcount: '606'
ht-degree: 100%

---

# Microsoft® Translator への接続{#connecting-to-microsoft-translator}

Microsoft® Translator クラウドサービスの設定を作成すると、Microsoft® 翻訳のアカウントを使用して AEM のページのコンテンツ、コミュニティのコンテンツ、アセットを翻訳することができます。

| プロパティ | 説明 |
|---|---|
| 翻訳ラベル | 翻訳サービスの表示名。 |
| 翻訳の帰属 | （オプション）ユーザー生成コンテンツの場合に、翻訳済みのテキストの横に表示される帰属情報（例：「`Translations by Microsoft`」）。 |
| ワークスペース ID | （オプション）カスタマイズされた Microsoft® Translator エンジンの利用 ID。 |
| サブスクリプションキー | Microsoft® Translator の Microsoft サブスクリプションキー。 |

設定を作成したら、その[設定をアクティベートする](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations)必要があります。

次の手順では、タッチ操作向け UI を使用して Microsoft® Translator の設定を作成します。

1. パネルで、ツール／クラウドサービスをクリックまたはタップします。
1. Microsoft® Translator エリアで「設定を表示」を選択します。
1. 「利用可能な設定」の横にある + リンクをクリックします。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 設定のタイトルを入力します。このタイトルによって、クラウドサービスコンソールおよびページプロパティのドロップダウンリストで設定が識別されます。デフォルト名はタイトルに基づいて指定されます。オプションとして、設定を格納するリポジトリノードに使用する名前を入力します。リポジトリノードのパスである「親設定」プロパティにはデフォルト値を使用する必要があります。
1. 「作成」をクリックします。
1. 表示されるダイアログボックスで、プロパティの値を入力して「OK」をクリックします。

## Microsoft® Translator クラウドサービスの設定例 {#sample-microsoft-translator-cloud-service-configurations}

以下に示す Microsoft® Translator クラウドサービスの設定が Geometrixx のサンプルと共にインストールされます。一部のサンプル設定では、Microsoft® 翻訳の体験版アカウントを使用します。このアカウントを使用すると、1 か月に最大 200 万文字の翻訳を無料で行うことができます。

### Microsoft® Translator 体験版ライセンス {#microsoft-translator-trial-license}

Microsoft® Translator 体験版ライセンス設定は、Geometrixx Outdoors サンプルパッケージと共にインストールされるサンプル設定です。この設定では、1 か月に 200 万文字の翻訳を行うことができる無料サブスクリプションが付属する Microsoft® Translator アカウントを使用します。

### Microsoft® Translator 体験版ライセンス - Geometrixx-outdoors {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft® Translator 体験版ライセンス - Geometrixx-outdoors 設定は、Geometrixx Outdoors サンプルパッケージと共にインストールされるサンプル設定です。この設定では、Microsoft® Translator 体験版ライセンス設定と同じ無料の Microsoft® Translator アカウントを使用します。アカウントには、1 か月に 200 万文字の翻訳を行うことができる無料サブスクリプションが付属します。

この Microsoft® Translator 設定は、Geometrixx Outdoors サンプルサイトのコンテンツのタイプで使用するために最適化されます。

### Microsoft® Translator 体験版ライセンス設定のアップグレード {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft® 翻訳の設定ページには、Microsoft® web サイトへのリンクがあり、実稼動システムに適したアカウントサブスクリプションを取得できます。

1. パネルで、ツール／操作／クラウド／クラウドサービスをクリックまたはタップします。
1. Microsoft® Translator エリアで「設定を表示」をクリックまたはタップし、「Microsoft® Translator 体験版ライセンス (Microsoft® 翻訳設定 )」をクリックまたはタップします。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 設定ページで「サブスクリプションをアップグレード」をクリックします。表示された Microsoft® web ページを使用して、アカウントを設定します。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Microsoft® Translator エンジンのカスタマイズ {#customizing-your-microsoft-translator-engine}

Microsoft® 翻訳の設定ページには、Microsoft® web サイトへのリンクがあり、Microsoft® Translator エンジンをカスタマイズすることができます。（[https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/ja-jp/research/project/microsoft-translator-hub/)）

1. パネルで、ツール／操作／クラウド／クラウドサービスをクリックまたはタップします。
1. Microsoft® Translator エリアで「設定を表示」をクリックまたはタップし、カスタマイズする設定をクリックまたはタップします。
1. 設定ページで「Translator をカスタマイズ」をクリックします。表示された Microsoft® web ページを使用して、サービスをカスタマイズします。

## Translator サービス設定のアクティベート {#activating-the-translator-service-configurations}

パブリッシュインスタンスにレプリケートされた翻訳済みコンテンツをサポートするには、クラウドサービス設定をアクティベートします。Microsoft® Translator またはサードパーティのクラウドサービス設定を保存するリポジトリノードをアクティベートするには、「[セクション全体（ツリー）のアクティブ化](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree)」の方法を使用します。このノードは以下に示す親ノードの下にあります。

* Microsoft® 翻訳サービス：/libs/settings/cloudconfigs/translation/msft-translation
* サードパーティ翻訳：/etc/cloudservices/machine-translation
