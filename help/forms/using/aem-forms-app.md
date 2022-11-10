---
title: AEM Forms アプリケーション
seo-title: AEM Forms app
description: AEM Forms アプリケーションにより、フィールドワーカーがモバイルデバイスでアダプティブフォームを使用できるようになります。
seo-description: AEM Forms app enables your field workers to use adaptive forms on their mobile devices.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '2450'
ht-degree: 100%

---

# AEM Forms アプリケーションの概要 {#aem-forms-app}

## 概要 {#overview}

AEM Forms アプリケーションでは、アダプティブフォーム、モバイルフォーム、およびモバイルデバイスのフォームセットをサーバーに基づいて同期することができます。[OSGi 上の Forms 中心ワークフロー](/help/forms/using/aem-forms-workflow.md)または JEE 上の Forms ワークフローを定義することができます。例えば、金融関係の会社を経営していて、顧客の申請と問い合わせの管理に AEM Forms を使用するとします。顧客はフォームを記入し、それを送信して承認を求めます。モバイルデバイスのフォームを有効にしている場合、顧客はフォームを AEM Forms アプリケーションで記入することができます。また、会社側も、モバイルデバイス上でのフォームの認証を有効にすることで、承認のワークフローを管理することができます。フィールドワーカーはモバイルデバイスを顧客のところに持参し、詳細を検証して、フォームを送信します。AEM Forms アプリケーションは AEM Forms サーバーと同期して、モバイルデバイス用に有効化されたフォームを取得します。アプリケーションがオフラインの場合、データはローカルに保存されます。

AEM Forms アプリケーションのソースコードは、ソフトウェアディストリビューションにより、使用することができます。ソフトウエア配布のソースコードパッケージは、`adobe-aemfd-forms-app-src-pkg-<version>.zip` として入手できます。

AEM Forms アプリケーションは、iOS、Android、および Windows デバイスでサポートされます。Android 向けの AEM Forms アプリケーションは Google Play から、iOS 向けの AEM Forms アプリケーションは App Store から、Windows 向けの AEM Forms アプリケーションは Windows ストアからインストールできます。

    [ ! [google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms&amp;hl=ja)
    
    [ ! [app_store](assets/app_store.png)](https://itunes.apple.com/jp/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ! [microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

iOS、Android、または Windows デバイスに AEM Forms アプリケーションをインストール、カスタマイズ、配布する方法については、「[AEM Forms アプリケーションのカスタマイズ、構築、配布](#customize-build-distribute)」を参照してください。

## 前提条件 {#prerequisites}

AEM Forms アプリケーションには、AEM Forms サーバーが必要です。ユーザーは、AEM Forms サーバーで作成したフォームのレンダリングを行い、フォームに記入して、ドラフトとして保存し、送信します。アプリケーションはサーバーに接続して、有効になっているフォームを取得します。AEM Forms アプリケーションは、サーバーと同期し、アプリケーションにフォームが読み込まれるとすぐに、ユーザーはオフラインで作業できるようになります。アプリケーションがオフラインの場合、データはデバイスに保存され、アプリケーションがオンラインの場合にデータを同期します。

### AEM Forms ワークフローを使用したサーバーのある AEM Forms アプリケーション {#aem-forms-app-with-servers-using-aem-forms-workflow}

AEM Forms Workflow サーバーをお持ちの場合、フォームを AEM Forms アプリケーションのタスクとしてレンダリングすることができます。例えば、金融関係の会社を経営していて、顧客がサービスを利用するために申込書を記入するとします。申込書はアダプティブフォームで、顧客からの情報を受け付け、レビューのサブミッションとして保存することができます。管理者は申込書をレビューし、検証リクエストをフィールドワーカーに転送します。転送された申込書により、フィールドワーカーのアプリケーションで検証フォームがタスクとして有効になります。フィールドワーカーはモバイルデバイスを顧客まで持参し、詳細を検証します。

### OSGi 上の Forms 中心ワークフローを使用したサーバーのある AEM Forms アプリケーション {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

AEM Forms サーバーをお持ちの場合、アダプティブフォームを AEM インボックスアプリケーションとして、また AEM Forms アプリケーションのタスクとしてレンダリングすることができます。例えば、金融関係の会社を経営していて、顧客がサービスを利用するために申込書を記入するとします。申込書は、顧客からの情報を受け付けてレビュー用の提出物として保存することができるアダプティブフォームに関連付けられています。管理者はタスクをレビューし、フィールドワーカーへの検証リクエストを承認します。フィールドワーカーはモバイルデバイスを顧客まで持参し、詳細を検証します。

### スタンドアロンのフォームまたは AEM Forms ワークフローを使用しないサーバーのある AEM Forms アプリケーション {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

AEM Forms ワークフローを使用しない AEM Forms サーバーは、OSGi 上の AEM Forms またはスタンドアロンのモバイルフォームもしくはアダプティブフォームです。AEM Forms アプリケーションは、[OSGi](/help/sites-deploying/configuring-osgi.md) に AEM Forms を実装して機能します。AEM Forms アプリケーション用に有効にして公開するフォームは、アプリケーション内で利用できます。

フォームをアプリケーションにダウンロードして、オフラインで使用することができます。例えば、金融関係の会社を経営していて、顧客がサイト上で申込書を記入するとします。申込書はアダプティブフォームで、顧客からの情報を受け付け、レビュー用に保存します。管理者はフォームをレビューし、AEM オーサーインスタンスで検証フォームを作成します。管理者は AEM Forms アプリケーションによる同期を有効にして、発行します。検証フォームが AEM Forms アプリケーションで使用できる場合、フィールドエージェントは顧客の詳細の検証にモバイルデバイスを使用することができます。モバイルデバイスはサーバーと同期し、検証フォームがアプリケーションにロードされます。フィールドエージェントは顧客を訪問し、詳細を検証した上で、データをドラフトとして保存、または検証フォームとして提出します。アプリケーションがオンラインになるたびに、フォームはサーバーと同期されます。

AEM Forms アプリケーションでは、次のようにフォームを同期します。

1. オーサーインスタンスでは、フォームを選択し、**[!UICONTROL 「プロパティの表示」]**&#x200B;をクリックします。

1. プロパティページで、「**[!UICONTROL 詳細]**」をクリックします。
1. 「詳細」で「**[!UICONTROL AEM Forms アプリと同期]**」オプションを有効にし、「**[!UICONTROL 保存]**」をタップします。

フォームが発行されると、アプリケーションはサーバーと同期してフォームを取得します。複数のフォームを同期するには、オーサーインスタンスで、フォームマネージャーから複数のフォームを選択して、「**[!UICONTROL AEM Forms アプリケーションと同期]**」をタップします。

## モバイルデバイスのサポート {#mobile-device-support}

[AEM Forms アプリケーション（旧称 Mobile Workspace）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)を参照してください。

## AEM Forms アプリケーションの主な機能 {#key-features-of-aem-forms-app}

### AEM Forms サーバーのある AEM Forms アプリケーション {#aem-forms-app-with-aem-forms-servers}

AEM Forms サーバーでアプリケーションを同期して、モバイルデバイスでフォームを使用した作業をすることができます。

AEM Forms Workflow サーバーでは、フォームをワークベンチプロセスおよび AEM インボックスアプリケーションのスタートポイントに関連付けることができます。AEM インボックスアプリケーションには、アダプティブフォームを関連付けることができます。スタートポイントにはアダプティブフォーム、HTML5 フォーム、または関連するフォームセットを設定することができます。スタートポイントはタスクとして送信したり、ドラフトとしてそのタスクを保存したりできます。AEM インボックスアプリケーションとスタートポイントとの違いについて詳しくは、[OSGi 上の Forms ベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能](capabilities-osgi-jee-workflows.md)を参照してください。

AEM Forms ワークフローを使用しない AEM Forms Server がある場合、アプリケーション内で同期が有効にされているフォームは AEM Forms アプリケーション内でレンダリングされます。フォームは、アプリケーションの「フォーム」タブで使用することができ、ドラフトとして送信または保存することができます。アプリケーションでは、アダプティブフォームおよびモバイルフォームがサポートされています。

1. **タスクまたはフォームをドラフトとして保存する**

   「ドラフトとして保存」オプションでは、記入済みのデータまたは関連フォームに添付されたファイルとともに、タスクまたはフォームのスナップショットを保存します。ドラフトはモバイルデバイスに保存され、今後取得できるようにするために AEM Forms サーバーと同期されます。

   [タスクまたはフォームをドラフトとして保存する](/help/forms/using/save-as-draft.md)を参照してください。

1. **フォームをテンプレートとして保存**

   時々、ユーザーがフォームを記入するときに、いくつかのフィールドへの入力が同じことがあります。そのような場合は、毎回同じ値を入力するフィールドに必要な値を入力し、そのフォームまたはドラフトをテンプレートとして保存することができます。これにより、テンプレートのインスタンスを作成するたびに、指定のフィールドをテンプレートに入力した値で事前入力することができます。これは、フォームを記入する時間と手間を省くのに役立ちます。

   「[フォームをテンプレートとして保存](/help/forms/using/save-forms-and-start-points-as-templates.md)」を参照。

### タスクとフォームを使用する {#working-with-tasks-and-forms}

アプリケーションを AEM Forms ワークフローサーバーと同期して、モバイルデバイスでタスクやフォームを使用できます。

モバイルデバイスのタスクには、アダプティブフォーム、HTML5 フォームまたはフォームセットが含まれ、さらに添付ファイルおよび[サマリー URL](/help/forms/using/getting-task-variables-summary-url.md) を含めることもできます。デフォルトでは、自分に割り当てられたタスクが **[!UICONTROL Tasks]** フォルダーに保存されます。タスクで作業する場合、タスクを変更して、そのタスクのドラフトコピーを AEM Forms サーバーに保存できます。

モバイルデバイスのフォームは、アダプティブフォームまたはモバイルフォームになります。Foms アプリケーションで同期可能なフォームは、Forms フォルダーにあります。AEM Forms ワークフローを使用しない AEM Forms Server（OSGi での AEM Forms）で有効にされているフォームを同期することができます。

次のページを参照してください。

* [タスクを開く](/help/forms/using/open-task.md)
* [フォームの操作](/help/forms/using/working-with-form.md)

### オフライン作業 {#working-offline}

オフラインモードであっても、モバイルデバイス上で作業ができます。ネットワークに接続していない場合でも、アプリケーションにログインできます。また、最後に同期したすべてのフォームを実行できます。フォームを同期する方法について詳しくは、「[アプリケーションの同期](/help/forms/using/sync-app.md)」を参照してください。フォームに関連付けられた添付ファイルを同期する場合、オフラインモードでその添付ファイルを開くこともできます。オフラインモードでは、フォームの編集、注釈の追加、およびフォームの送信と保存が可能です。フォームは次にオンラインになったときに AEM Forms サーバーと同期します。

詳細については、「[オフラインモードの使用](/help/forms/using/work-offline-mode.md)」を参照してください。

### 注釈の追加 {#adding-annotations}

モバイルデバイス上のフォームに以下を添付できます。

* **メモ** - メモ機能を使用して、手書きメモまたはテキストメモを追加できます。詳しくは、「[メモの追加](/help/forms/using/add-attachments.md#adding-a-note)」を参照してください。

* **写真** - AEM Forms アプリケーションには、モバイルデバイスのカメラ機能またはギャラリーを使用する機能があります。写真注釈を使用すると、写真を関連するフォームに追加することができます。詳しくは、「[写真の追加](/help/forms/using/add-attachments.md#adding-a-photograph)」を参照してください。

### 自動保存 {#autosave}

AEM Forms アプリケーションでユーザーがデータを入力すると、自動保存の機能により一定の間隔でデータが保存されます。AEM Forms アプリケーションの自動保存の機能は、電池切れなどが原因でアプリケーションが終了した場合にデータの損失を防ぐことができます。

「[AEM Forms アプリケーションで自動保存を使用](/help/forms/using/autosave-data-app.md)」を参照。

## AEM インボックスの機能と AEM Forms アプリケーションの機能との違い {#differences-between-aem-inbox-and-aem-forms-app-features}

Forms 中心のワークフローを起動するには、[AEM インボックス](/help/forms/using/manage-applications-inbox.md)と AEM Forms アプリケーションの 2 つの方法があります。ただし、AEM インボックスの機能と AEM Forms アプリケーションの機能は異なっています。AEM インボックスは [Forms 中心のワークフロー](/help/forms/using/aem-forms-workflow.md)でのみ機能するのに対して、AEM Forms アプリケーションは Forms 中心のワークフローとプロセス管理の両方で機能します。AEM インボックスアプリケーションと AEM Forms アプリケーションの機能の違いについて詳しくは、[OSGi 上の Forms ベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能](capabilities-osgi-jee-workflows.md)を参照してください。

## サポートされているフォーム {#supported-forms}

AEM Forms アプリケーションでサポートされているフォームのタイプは、次のとおりです。

### アダプティブフォーム {#adaptive-form}

AEM Forms アプリケーションでは、ユーザーの入力を動的に反映するアダプティブフォームがサポートされています。遅延読み込みアダプティブフォームもサポートされています。

### モバイルフォーム {#mobile-form}

AEM Forms では、モバイルデバイス用のフォームを作成することができます。モバイルフォームは、モバイルデバイスの HTML フォームとして、ディスプレイデバイスに応じてレンダリングされます。

### フォームセット {#formset}

フォームセットでは、サービスやプロセスに関連する複数のフォームをグループ化し、ビジネス上のプロセスを自動化するとともにエンドユーザーに表示します。このようなシナリオでは、ユーザーはセット全体を 1 つとして記入し、個々のフォームやプロセスをファイル、送信、追跡する必要はありません。

>[!NOTE]
>
>AEM Forms Workflow（JEE 上の AEM Forms）が必要です。

## AEM Forms アプリケーションの仕組み {#how-aem-forms-app-works}

AEM Forms アプリケーションは、フィールドワーカーが各自に割り当てられたフォームで作業するためのモバイルソリューションを提供します。アプリケーションはサーバーから完全なデータをキャッシュし、すべての作業をローカルに保存することによって、十分なユーザーエクスペリエンスを提供します。ディスクからのデータは適時の同期更新によってサーバーに送信されます。

AEM Forms アプリケーションは、モデルに保存されたデータをビューで表示するために Backbone モデルが効果的に使用される PhoneGap 5.0 ベースのアプリケーションです。すべてのネイティブ操作は、PhoneGap プラグインによって実行されます。

## AEM Forms アプリケーションのカスタマイズ、構築、配布 {#customize-build-distribute}

>[!NOTE]
>
>AEM Forms アプリケーションソースコードを使用してアプリを構築する場合にのみ適用可能です。

AEM Forms アプリケーションは、組織特有のニーズに合わせて簡単にカスタマイズできます。アプリケーションのソースコードは AEM Forms とともに提供されます。ソースコードに変更を加え、独自に作業員向けモバイルソリューションを構築できます。アプリケーションへのサインには、会社独自のキーを使用することもできます。

### カスタマイズ {#customize}

アプリケーションをカスタマイズして次のことができます。

**ブランディング**：アプリケーションのアイコン、アプリケーション名、起動の画像、AEM Forms アプリケーション内のページを変更します。テキストを特定の地域のローカライズアプリケーションに変更することもできます。AEM Forms アプリケーションのブランディングについて詳しくは、「[ブランディングのカスタマイズ](/help/forms/using/branding-customization.md)」を参照してください。

**テーマ**：AEM Forms アプリケーションユーザーインターフェイスでのカラー、フォント、間隔などのスタイルを変更します。詳しくは、「[テーマのカスタマイズ](/help/forms/using/theme-customization.md)」を参照してください。

**ジェスチャー**：AEM Forms アプリケーションユーザーインターフェイスでの右にスワイプ、左にスワイプなどのジェスチャーを変更します。詳しくは、「[ジェスチャーのカスタマイズ](/help/forms/using/gesture-customization.md)」を参照してください。

AEM Forms アプリケーションプロジェクトをカスタマイズ用にセットアップする方法について、詳細は次のリンクを参照してください。

* [AEM Forms アプリケーションの環境設定](/help/forms/using/setup-environment-mobile-workspace.md)
* [Visual Studio プロジェクトの設定と Windows アプリケーションの構築](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Xcode プロジェクトの設定と iOS アプリケーションの構築](/help/forms/using/setup-xcode-project-build-installer.md)
* [Eclipse プロジェクトの設定と Android アプリケーションの構築](/help/forms/using/setup-eclipse-project-build-installer.md)

### 構築と配布 {#build-and-distribute}

AEM Forms アプリケーションのソースコードは、ソフトウエア配布で AEM Forms アプリケーションソースパッケージの一部として入手可能な `adobe-lc-mobileworkspace-src.zip` から抽出できます。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/jp/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージの名前をタップし、「**[!UICONTROL EULA 利用規約に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

**iOS の場合**：

iOS アプリケーション（.ipa）の作成方法について、詳しくは「[Xcode プロジェクトの設定と iOS アプリの構築](/help/forms/using/setup-xcode-project-build-installer.md)」を参照してください。

プロビジョニングプロファイルを使用した AEM Forms アプリケーションへの署名方法について詳しくは、[iOS コード署名の設定、処理、トラブルシューティング](https://developer.apple.com/support/code-signing/)を参照してください。

**Android の場合**：

Android アプリケーション（.apk）の作成方法について詳しくは、[Eclipse プロジェクトの設定と Android アプリケーションの構築](/help/forms/using/setup-eclipse-project-build-installer.md)を参照してください。

AEM Forms アプリケーションへの署名方法について詳しくは、[アプリケーションへの署名](https://developer.android.com/tools/publishing/app-signing.html)を参照してください。

**Windows の場合**：

Windows アプリケーション（.appx）の作成方法について詳しくは、[Visual Studio プロジェクトの設定と Windows アプリケーションの構築](/help/forms/using/setup-visual-studio-project-build-installer.md)を参照してください。

MDM を介したアプリケーションの配布方法について詳しくは、「[AEM Forms アプリケーションの配布](/help/forms/using/distribute-mobile-workspace-app.md)」を参照してください。MDM を介したアプリ配信は、iOS および Android にのみ対応しています。

## Mobile Workspace を AEM Forms アプリケーションにアップグレードするための推奨事項 {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

最新バージョンの AEM Forms アプリケーションにアップグレードする場合は、以下のポイントを通読してください。

* **Android に Play ストアから以前のバージョンのアプリケーションをインストールした場合** アプリケーションを Play ストアから直接アップグレードできます。

* **以前のバージョンのアプリケーションがソースコードを使用してビルドおよびインストールされている場合（iOS および Android に適用）**：

   新しいアプリケーションをインストールする前に、すべてのデータを AEM Forms サーバーと同期します。データが同期されたら、以前のバージョンのアプリケーションをアンインストールし、新しいアプリケーションをインストールします。
