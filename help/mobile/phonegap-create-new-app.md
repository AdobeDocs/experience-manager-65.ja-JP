---
title: 作成ウィザードを使用したAEM Mobile アプリケーションの作成
description: AEM Mobile アプリは、ページ構造とプロパティを定義するブループリントに基づいています。 このページでは、アプリテンプレートに基づいてアプリを作成する方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 7%

---

# 作成ウィザードを使用したAEM Mobile アプリケーションの作成{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

AEM Mobile アプリは、ページ構造とプロパティを定義するブループリントに基づいています。 次のアプリケーションプロパティを設定できます。

* **タイトル：** アプリケーションのタイトル。
* **宛先のパス：** アプリケーションが格納されるリポジトリ内の場所。 デフォルトのままにすると、アプリ名に基づいてパスが作成されます。

* **名前：** デフォルト値は、スペース文字が削除されたタイトルプロパティの値です。 この名前は、AEM内でアプリケーションを参照するために使用されます。例えば、アプリケーションを表すリポジトリーノード用として使用します。
* **説明：** アプリケーションの説明。
* **サーバー URL:** アプリケーションに Over-the-Air （OTA）コンテンツのアップデートを提供する URL。 デフォルト値は、アプリケーションの作成に使用されるインスタンスのパブリッシュサーバー URL （Externalizer サービスから取得される）です。 注意：認証が必要なオーサーインスタンスではなく、パブリッシュサーバーインスタンスを指定する必要があります。

また、アプリケーションのサムネールとして使用する画像ファイルを指定し、使用するPhoneGap Build設定を選択し、使用する Mobile App Analytics 設定を選択することもできます。 この画像は、Experience Managerのモバイルアプリコンソール内でモバイルアプリケーションを表すサムネールとしてのみ使用されています。

Cloud Service を構築し、AdobeMobile Services SDK プラグインをアプリに統合するための追加の（およびオプションの） タブが存在します。

* ビルド：ここで、「設定を管理」をクリックしてbuild.phonegap.com ビルドサービスをセットアップします。 次に、ドロップダウンから、新しく作成された PhoneGap ビルドクラウドサービスを選択できます。
* Analytics:「設定を管理」をクリックして、 [Mobile Services SDK のAdobe](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) クラウドサービス。 次に、ドロップダウンから、新しく作成した Mobile Service を選択して、モバイルアプリに統合できます。

## アプリテンプレートの使用 {#using-app-templates}

アプリテンプレートを使用すると、開発者が作成し、AEM内で新しいアプリを作成する際に使用される既存のデザインを、簡単に使用できます。

アプリテンプレートとは これは、アプリのベースラインまたは基盤を表すページテンプレートおよびコンポーネントのコレクションと考えることができます。
別のアプリのテンプレートに基づいてアプリを作成すると、そのアプリが作成された元のアプリを表す出発点を持つアプリが取得されます。

この機能を使用するには、既存のモバイルアプリテンプレート（またはアプリテンプレートがインストールされたアプリ）が必要です。

最新のAEM アプリのサンプルパッケージには、アプリテンプレートを含んだ最新バージョンのGeometrixxアプリが含まれています。 または、 [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) テンプレートも提供します。

アプリテンプレートに基づいてアプリを作成する手順：

1. AEM Mobile アプリカタログ（&lt;）に移動します。*server-url*>aem/apps.html/content/mobileapps
1. を選択 **作成** を選択してから、 **アプリ** 下図のように

![chlimage_1-158](assets/chlimage_1-158.png)

AEM開発者によって使用可能になったアプリテンプレートを選択します。 参照： [AEM Mobile アプリケーションの構造](/help/mobile/phonegap-structure-an-app.md) 開発者向けサポート。

![chlimage_1-159](assets/chlimage_1-159.png)

必要に応じて、新しいアプリの詳細（オプションでサムネール画像を変更するなど）を入力します。 これらの値は、後でフォームから編集できます **アプリの管理** タイル。

![chlimage_1-160](assets/chlimage_1-160.png)

## 次の手順 {#the-next-steps}

他のオーサリングの役割について詳しくは、次のリソースを参照してください。

* [アプリを管理タイル](/help/mobile/phonegap-app-details-tile.md)
* [アプリのメタデータの編集](/help/mobile/phonegap-editmetadata.md)
* [アプリの定義](/help/mobile/phonegap-app-definitions.md)
* [既存のハイブリッドアプリを読み込む](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [コンテンツサービス](/help/mobile/develop-content-as-a-service.md)

## その他のリソース {#additional-resources}

管理者と開発者の役割と責任については、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けの開発](/help/mobile/developing-in-phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
