---
title: アプリを管理タイル
description: アプリケーションに関する詳細を編集できるアプリダッシュボードの「アプリを管理」タイルについて詳しく説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 5%

---

# アプリを管理タイル{#manage-app-tile}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

アプリダッシュボードの **`Manage App`** タイルでは、アプリケーションに関する詳細を編集できます。 詳細ページを開くには、**`Manage App`** タイルの詳細リンクをクリックします。 **`Manage App`** ページ内から、PhoneGap Application Configuration （config.xml）設定を編集し、様々なアプリケーションストアに送信するためのアプリケーションを準備できます。

![chlimage_1-116](assets/chlimage_1-116.png)

## `Manage App` タイルについて {#understanding-the-manage-app-tile}

**`Manage App`** タイル内の各タイルにドリルダウンし、右下隅の「。..」をクリックして詳細を表示または編集できます。

### 「基本」タブ {#the-basic-tab}

このタブから、アプリの **名前**、**作成者**、**簡単な説明**、および **説明** を編集できます。

![chlimage_1-117](assets/chlimage_1-117.png)

### 「詳細」タブ {#the-advanced-tab}

各モバイルアプリケーションプラットフォームは、収集するデータを記述し、各アプリケーションストアを具体的にターゲットにします。

表示されるプラットフォームは、PhoneGap config.xml コンテンツによって決まります。

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Apple App StoreやGoogle Play ストアなどの各ベンダーアプリケーションストアには、顧客にアプリケーションの詳細を表示するために、モバイルアプリケーションのスクリーンショットが 1 つ以上必要です。 これらのスクリーンショットには、ディメンションとコンテンツに関する厳密な要件がある場合があります（基本的には、真にアプリケーションを表す必要があります）。 AEM Apps では、サポート対象のプラットフォームに関するこれらのスクリーンショットの選択と管理、および各ベンダーのアプリケーションストアの要件に応じたポートディメンションの表示をサポートしています。

>[!NOTE]
>
>AEM Verify アプリを使用すると、スクリーンショットをAEMのアプリ詳細に直接送信できます。
>
>詳しくは、[AEM Verify 用のモバイルクイックスタート ](/help/mobile/phonegap-mobile-quickstart.md) を参照してください。

![chlimage_1-118](assets/chlimage_1-118.png)

### メタデータ {#metadata}

>[!NOTE]
>
>**`Manage App`** タイルについて詳しくは、[ アプリのメタデータの編集 ](/help/mobile/phonegap-editmetadata.md) を参照して、メタデータを表示および編集してください。

#### 共通メタデータ {#common-metadata}

各アプリケーションには、アプリケーションの様々な側面の設定を支援する関連メタデータが必要です。 アプリを管理ページは、メタデータ収集に関連する 2 つの異なる領域に分かれています。 プラットフォーム固有のメタデータと共通のメタデータ。

すべてのプラットフォームに共通の設定とメタデータがあります。

このセクションでは、Content Update Server の URL、モバイルアプリケーションのランディングページ、コンパイル用の PhoneGap バージョン、アプリケーションのバージョン、名前、説明などを定義します。

**アプリのバージョン** は、アプリケーションの作業用バージョンです。 一般的なベストプラクティスは、10 進数の 3 表記を使用し、最初のリリースの前に 1.0.0 未満から開始することです。

**PhoneGap Version** は、PhoneGap を使用してアプリケーションをコンパイルするバージョンです。 ベストプラクティスは、最新のバージョンを常に把握し、最新かつ最大限の機能とバグ修正を確実に入手することです。

**Content Update Server URL** は、アプリケーションが ContentSync 更新を呼び出すために使用する URL です。 アプリケーションに対してコンテンツ同期の更新を提供するために使用するパブリッシュインスタンスの 1 つに、Dispatcher URL または（Dispatcherを使用していない場合）に設定されている必要があります。

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>フィールドに入力するデータがない限り、このセクションは空に見える場合があります。
>
>詳細ビューの上部には、アプリケーションのバージョン、PhoneGap のバージョン、更新 URL が表示され、これらの各値は「共通のメタデータ」セクションで設定できます。 ただし、アプリケーション ID は編集できません。

#### Platform メタデータ {#platform-metadata}

PhoneGap config.xml で定義されるすべてのプラットフォームには、カスタムプラットフォームプロパティを含めることができます。 AEM開発者は、これらのプロパティを取得するためにコンテンツ構造に関与する必要があります。 プラットフォーム固有のプロパティの一例については、iOSを参照してください。

すべての設定済みプラットフォームのメタデータが、`Manage App` ータタイルの「詳細」タブに同時に表示されるようになりました。

>[!NOTE]
>
>プラットフォームのメタデータセクションは、リモート PhoneGap の CLI またはビルド中に PhoneGap によって使用されません。 代わりに、AEMは、後でターゲットベンダーのアプリケーションストアに送信する際に使用できるように、プラットフォームのメタデータの取得を試みます。

AEMで認識されないプラットフォームの場合でも、AEM開発者が UI を拡張して、このメタデータを取得し、後で書き出して、アプリケーション送信プロセス中に使用できます。

#### iOS メタデータ {#ios-metadata}

Apple AppStore では、配布用にアプリを送信するために追加のメタデータが必要です。 「iOS メタデータ」セクションでは、Appleの iTMSTransporter ツールが関連するApple開発者アカウントにメタデータを公開するために使用できる必須情報の収集を試みます。

Apple固有のメタデータを取得するには、[https://itunesconnect.apple.com](https://itunesconnect.apple.com/) でアプリケーションを作成します。 アプリケーションを作成すると、Appleによってメタデータが生成されます。このメタデータは、iOS iTMSTransporter ツールを使用してメタデータを検証し、itunesconnect.apple.comにアップロードする場合に、Apple メタデータセクションで要求されます。 収集するメタデータを取得する場合、iOS固有のメタデータを入力する必要はありません。 iOSと共通のメタデータを結合したメタデータを書き出し、すべてのスクリーンショットを zip ファイルに収集して、いつでもダウンロードできます。

ダウンロードした zip ファイルには、metadata.xml を調べることができる itmsp ファイルが含まれています。 itmsp ファイルには、エクスポートされたメタデータ（metadata.xml ファイル内）と、関連するすべてのスクリーンショットが含まれています。

エクスポート機能は、ベンダー固有のアプリケーションストアに入力するためにアプリケーションパブリッシャーに渡すことができるスクリーンショットおよびメタデータを収集する便利な方法を提供するために使用されます。

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android™ メタデータ {#android-metadata}

Android™ プラットフォームを選択する場合、この時点で設定できるカスタムメタデータはありません。 「ダウンロード」ボタンをクリックすると、すべてのメタデータと関連するスクリーンショットを含むプロパティファイルの zip ファイルが生成されます。

エクスポート機能は、ベンダー固有のアプリケーションストアに入力するためにアプリケーションパブリッシャーに渡すことができるスクリーンショットおよびメタデータを収集する便利な方法を提供するために使用されます。

![chlimage_1-121](assets/chlimage_1-121.png)

### コンテンツ更新サーバーの URL {#content-update-server-url}

AEM Apps の主な機能の 1 つは、ContentSync を使用してモバイルアプリケーションに新しいコンテンツをリクエストさせる機能です。この機能では、コンテンツとして、HTML リソース、ページ、ビデオ、画像、テキストなどを使用できます。 コンテンツ作成者がコンテンツを更新してそのコンテンツを公開した後、サーバーによってコンテンツ更新がモバイルアプリケーションでダウンロードできるようになります。

Content Update Server URL プロパティは、直接またはDispatcherや CDN を介してパブリッシュインスタンスを指す必要がある URL です。 URL の形式は次のとおりです。

`https://[hostname]:[port]`

>[!NOTE]
>
>オーサーサーバーインスタンスが多数のパブリッシュサーバーインスタンスにレプリケーションしている場合（AEMの共通アーキテクチャ）、各パブリッシュサーバーの更新コンテンツは同じになります。 アップデートがオーサーインスタンスで作成され、すべてのパブリッシュインスタンスにレプリケートされるからです。 基本的に、ロード・バランシングとフェイルオーバーが完全にサポートされます。

### 「プラグイン」タブ {#the-plugins-tab}

「**プラグイン**」タブには、アプリに関連付けられたプラグインが表示されます。 この情報は、ビルド時に適切なプラグインを取得するために使用されます。

![chlimage_1-122](assets/chlimage_1-122.png)

### 「スクリーンショット」タブ {#the-screenshots-tab}

「**スクリーンショット**」タブには、サポートされているスクリーンショット解像度が様々なプラットフォームで表示されます。

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>スクリーンショットの追加と削除については、[ アプリのメタデータの編集 ](/help/mobile/phonegap-editmetadata.md) を参照してください。

### 「認証」タブ {#the-authentication-tab}

「**認証**」タブでは、アプリケーションに関連付ける OAuth クライアントを選択でき、開発者はAdobe Experience Managerを OAuth 認証を使用できます。

![chlimage_1-124](assets/chlimage_1-124.png)

### 次の手順 {#the-next-steps}

アプリケーションダッシュボードでのアプリタイルの管理を理解したら、他のオーサリングの役割について、次のリソースを参照してください。

* [アプリのメタデータの編集](/help/mobile/phonegap-editmetadata.md)
* [アプリの定義](/help/mobile/phonegap-app-definitions.md)
* [アプリの作成ウィザードを使用した新しいアプリの作成](/help/mobile/phonegap-create-new-app.md)
* [既存のハイブリッドアプリを読み込む](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [コンテンツサービス](/help/mobile/develop-content-as-a-service.md)

### その他のリソース {#additional-resources}

管理者と開発者の役割と責任については、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けの開発](/help/mobile/developing-in-phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
