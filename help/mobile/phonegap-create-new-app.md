---
title: 作成ウィザードを使用したAEM Mobileアプリの作成
description: AEM Mobileアプリは、ページ構造とプロパティを定義するブループリントに基づいています。 このページでは、アプリのテンプレートに基づくアプリの作成方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 3%

---

# 作成ウィザードを使用したAEM Mobileアプリの作成{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

AEM Mobileアプリは、ページ構造とプロパティを定義するブループリントに基づいています。 次のアプリケーションプロパティを設定できます。

* **タイトル：** アプリケーションのタイトル。
* **宛先のパス：** リポジトリ内でアプリケーションが保存される場所。 アプリ名に基づいてパスを作成する場合は、デフォルトのままにします。

* **名前：** 既定値は、空白文字が削除された Title プロパティの値です。 この名前は、AEM内でアプリケーションを参照するために使用されます。例えば、アプリケーションを表すリポジトリノードの場合は、このアプリケーションを参照します。
* **説明：** アプリケーションの説明。
* **サーバー URL:** Over-the-Air(OTA) コンテンツを提供する URL が、アプリケーションに対して更新されます。 デフォルト値は、アプリケーションの作成に使用されるインスタンスのパブリッシュサーバー URL です（Externalizer サービスから取得されます）。 これは、認証が必要なオーサーではなく、パブリッシュサーバーインスタンスである必要があります。

また、アプリケーションのサムネールとして使用する画像ファイルを指定し、使用するPhoneGap Build設定を選択し、使用するモバイルアプリ分析設定を選択することもできます。 この画像は、Experience Managerのモバイルアプリコンソール内でモバイルアプリを表すためのサムネールとしてのみ使用されます。

ビルドクラウドサービスや、AdobeMobile Services SDK プラグインをアプリに統合するための追加のタブが存在します（オプション）。

* ビルド：ここで「設定を管理」をクリックし、 build.phonegap.comビルドサービスを設定します。 その後、ドロップダウンから、新しく作成した PhoneGap Build クラウドサービスを選択できます。
* Analytics: 「設定の管理」をクリックし、 [AdobeMobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) クラウドサービス。 次に、ドロップダウンから、新しく作成した Mobile Service を選択して、モバイルアプリに統合できます。

## アプリテンプレートの使用 {#using-app-templates}

アプリテンプレートを使用すると、開発者が作成した既存のデザインを簡単に使用して、AEM内で新しいアプリを作成できます。

アプリテンプレートとは これは、アプリのベースラインまたは基盤を表すページテンプレートおよびコンポーネントの集まりと考えてください。
別のアプリのテンプレートに基づいてアプリを作成する場合、作成元のアプリを表す開始点を持つアプリが表示されます。

この機能を利用するには、既存のモバイルアプリテンプレート（またはアプリテンプレートを持つアプリ）がインストールされている必要があります。

最新のAEM Apps サンプルパッケージには、Geometrixxアプリの更新バージョンとアプリテンプレートが含まれています。 または、 [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) これにはテンプレートも用意されています。

アプリテンプレートに基づいてアプリを作成する手順は次のとおりです。

1. 次のAEM Mobileアプリカタログに移動します。 &lt;*server-url*>aem/apps.html/content/mobileapps
1. 選択 **作成** 次を選択します。 **アプリ** 次に示すように

![chlimage_1-158](assets/chlimage_1-158.png)

AEM開発者が使用可能にしたアプリテンプレートを選択します。 詳しくは、 [AEM Mobileアプリの構造](/help/mobile/phonegap-structure-an-app.md) 開発者支援用。

![chlimage_1-159](assets/chlimage_1-159.png)

必要に応じて、新しいアプリの詳細を入力します。その際には、オプションでサムネール画像を変更します。 これらの値は、後で **アプリを管理** タイル。

![chlimage_1-160](assets/chlimage_1-160.png)

## 次の手順 {#the-next-steps}

他のオーサリングの役割について詳しくは、次のリソースを参照してください。

* [アプリを管理タイル](/help/mobile/phonegap-app-details-tile.md)
* [アプリのメタデータの編集](/help/mobile/phonegap-editmetadata.md)
* [アプリの定義](/help/mobile/phonegap-app-definitions.md)
* [既存のハイブリッドアプリの読み込み](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [コンテンツサービス](/help/mobile/develop-content-as-a-service.md)

## その他のリソース {#additional-resources}

管理者および開発者の役割と責務について詳しくは、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向け開発](/help/mobile/developing-in-phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
