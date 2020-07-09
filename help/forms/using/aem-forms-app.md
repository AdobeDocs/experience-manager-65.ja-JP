---
title: AEM Forms アプリケーション
seo-title: AEM Forms アプリケーション
description: AEM Forms アプリケーションにより、フィールドワーカーがモバイルデバイスでアダプティブフォームを使用できるようになります。
seo-description: AEM Forms アプリケーションにより、フィールドワーカーがモバイルデバイスでアダプティブフォームを使用できるようになります。
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: aaedec7314b0fa8551df560eef2574a53c20d1c5
workflow-type: tm+mt
source-wordcount: '2418'
ht-degree: 75%

---


# Introduction to AEM Forms app {#aem-forms-app}

## 概要 {#overview}

AEM Forms アプリケーションでは、アダプティブフォーム、モバイルフォーム、およびモバイルデバイスのフォームセットをサーバーに基づいて同期することができます。[OSGi 上の Forms 中心ワークフロー](/help/forms/using/aem-forms-workflow.md)または [JEE 上の Forms ワークフロー](/help/forms/using/finance-reference-site-walkthrough.md#approving-the-application)を定義することができます。例えば、金融関係の会社を経営していて、顧客の申請と問い合わせの管理に AEM Forms を使用するとします。顧客はフォームを記入し、それを送信して承認を求めます。モバイルデバイスのフォームを有効にしている場合、顧客はフォームを AEM Forms アプリケーションで記入することができます。また、会社側も、モバイルデバイス上でのフォームの認証を有効にすることで、承認のワークフローを管理することができます。フィールドワーカーはモバイルデバイスを顧客のところに持参し、詳細を検証して、フォームを送信します。AEM Forms アプリケーションは AEM Forms サーバーと同期して、モバイルデバイス用に有効化されたフォームを取得します。アプリがオフラインの場合、データはローカルに保存されます。

AEM Forms アプリケーションのソースコードは、パッケージ共有により、使用することができます。The source code package in package share is available as: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

AEM Forms アプリケーションは、iOS、Android、および Windows デバイスでサポートされます。Android向けのAEM Formsアプリは、Google Playから、iOSはApp Storeから、Windowsストアからインストールできます。

    [ ![google_play](assets/google_play.png)
    
    [ ![app_store](assets/app_store.png)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

iOS、Android、または Windows デバイスに AEM Forms アプリケーションをインストール、カスタマイズ、配布する方法については、「[AEM Forms アプリケーションのカスタマイズ、構築、配布](#customize-build-distribute)」を参照してください。

## 前提条件 {#prerequisites}

AEM Forms アプリケーションには、AEM Forms サーバーが必要です。ユーザーは、AEM Forms サーバーで作成したフォームのレンダリングを行い、フォームに記入して、ドラフトとして保存し、送信します。アプリケーションはサーバーに接続して、有効になっているフォームを取得します。AEM Forms アプリケーションは、サーバーと同期し、アプリケーションにフォームが読み込まれるとすぐに、ユーザーはオフラインで作業できるようになります。アプリケーションがオフラインの場合、データはデバイスに保存され、アプリケーションがオンラインの場合にデータを同期します。

### AEM Forms ワークフローを使用したサーバーのある AEM Forms アプリケーション {#aem-forms-app-with-servers-using-aem-forms-workflow}

AEM Forms Workflow サーバーをお持ちの場合、フォームを AEM Forms アプリケーションのタスクとしてレンダリングすることができます。例えば、金融関係の会社を経営していて、顧客がサービスを利用するために申込書を記入するとします。申込書はアダプティブフォームで、顧客からの情報を受け付け、レビューのサブミッションとして保存することができます。管理者は申込書をレビューし、検証リクエストをフィールドワーカーに転送します。転送された申込書により、フィールドワーカーのアプリケーションで検証フォームがタスクとして有効になります。フィールドワーカーはモバイルデバイスを顧客まで持参し、詳細を検証します。

### OSGi 上の Forms 中心ワークフローを使用したサーバーのある AEM Forms アプリケーション {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

AEM Forms サーバーをお持ちの場合、アダプティブフォームを AEM インボックスアプリケーションとして、また AEM Forms アプリケーションのタスクとしてレンダリングすることができます。例えば、金融関係の会社を経営していて、顧客がサービスを利用するために申込書を記入するとします。申込書は、顧客からの情報を受け付けてレビュー用の提出物として保存することができるアダプティブフォームに関連付けられています。管理者はタスクをレビューし、フィールドワーカーへの検証リクエストを承認します。フィールドワーカーはモバイルデバイスを顧客まで持参し、詳細を検証します。

### スタンドアロンのフォームまたは AEM Forms ワークフローを使用しないサーバーのある AEM Forms アプリケーション {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

AEM Forms ワークフローを使用しない AEM Forms サーバーは、OSGi 上の AEM Forms またはスタンドアロンのモバイルフォームもしくはアダプティブフォームです。AEM Forms アプリケーションは、[OSGi](/help/sites-deploying/configuring-osgi.md) に AEM Forms を実装して機能します。AEM Forms版アプリケーションで有効にして発行するフォームは、アプリケーションで使用できます。

フォームをアプリケーションにダウンロードして、オフラインで使用することができます。例えば、金融関係の会社を経営していて、顧客がサイトで申込書を記入したとします。 申込書はアダプティブフォームで、顧客からの情報を受け付け、レビュー用に保存します。管理者はフォームをレビューし、AEM オーサーインスタンスで検証フォームを作成します。管理者は AEM Forms アプリケーションによる同期を有効にして、発行します。検証フォームが AEM Forms アプリケーションで使用できる場合、フィールドエージェントは顧客の詳細の検証にモバイルデバイスを使用することができます。モバイルデバイスはサーバーと同期し、検証フォームがアプリケーションにロードされます。フィールドエージェントは顧客を訪問し、詳細を検証した上で、データをドラフトとして保存、または検証フォームとして提出します。アプリケーションがオンラインになるたびに、フォームはサーバーと同期されます。

AEM Forms アプリケーションでは、次のようにフォームを同期します。

1. オーサーインスタンスでは、フォームを選択し、**[!UICONTROL 「プロパティの表示」]**&#x200B;をクリックします。

1. In the properties page, click **[!UICONTROL Advanced]**.
1. Under Advanced, enable option: **[!UICONTROL Sync with AEM Forms App]** and tap **[!UICONTROL Save]**.

フォームが発行されると、アプリケーションはサーバーと同期してフォームを取得します。複数のフォームを同期するには、オーサーインスタンスで、フォームマネージャーから複数のフォームを選択して、「**[!UICONTROL AEM Forms アプリケーションと同期]**」をタップします。

## モバイルデバイスのサポート {#mobile-device-support}

[AEM Forms アプリケーション（旧称 Mobile Workspace）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)を参照してください。

## AEM Forms アプリケーションの主な機能 {#key-features-of-aem-forms-app}

### AEM Forms サーバーのある AEM Forms アプリケーション {#aem-forms-app-with-aem-forms-servers}

AEM Forms サーバーでアプリケーションを同期して、モバイルデバイスでフォームを使用した作業をすることができます。

AEM Forms Workflow サーバーでは、フォームをワークベンチプロセスおよび AEM インボックスアプリケーションのスタートポイントに関連付けることができます。AEM インボックスアプリケーションには、アダプティブフォームを関連付けることができます。スタートポイントにはアダプティブフォーム、HTML5 フォーム、または関連するフォームセットを設定することができます。スタートポイントはタスクとして送信したり、ドラフトとしてそのタスクを保存したりできます。For more information on differences between an AEM Inbox application and a startpoint see [Actions and capabilities of Form-centric AEM Workflows on OSGi and AEM Forms JEE workflows](capabilities-osgi-jee-workflows.md).

AEM Forms ワークフローを使用しない AEM Forms Server がある場合、アプリケーション内で同期が有効にされているフォームは AEM Forms アプリケーション内でレンダリングされます。フォームは、アプリケーションの「フォーム」タブで使用することができ、ドラフトとして送信または保存することができます。アプリケーションでは、アダプティブフォームおよびモバイルフォームがサポートされています。

1. **タスクまたはフォームをドラフトとして保存する**

   「ドラフトとして保存」オプションでは、記入済みのデータまたは関連フォームに添付されたファイルとともに、タスクまたはフォームのスナップショットを保存します。ドラフトはモバイルデバイスに保存され、今後取得できるようにするために AEM Forms サーバーと同期されます。

   [タスクまたはフォームをドラフトとして保存する](/help/forms/using/save-as-draft.md)を参照してください。

1. **フォームをテンプレートとして保存**

   時々、ユーザーがフォームを記入するときに、いくつかのフィールドへの入力が同じことがあります。そのような場合は、毎回同じ値を入力するフィールドに必要な値を入力し、そのフォームまたはドラフトをテンプレートとして保存することができます。これにより、テンプレートのインスタンスを作成するたびに、指定のフィールドをテンプレートに入力した値で事前入力することができます。これは、フォームを記入する時間と手間を省くのに役立ちます。

   「[フォームをテンプレートとして保存](/help/forms/using/save-forms-and-start-points-as-templates.md)」を参照。

### タスクとフォームを使用する {#working-with-tasks-and-forms}

アプリケーションを AEM Forms ワークフローサーバーと同期して、モバイルデバイスでタスクやフォームを使用できます。

A task on the mobile device contains an adaptive form, HTML5 form, or a form set and can also contain attachments and [summary URL](/help/forms/using/getting-task-variables-summary-url.md). デフォルトでは、自分に割り当てられたタスクが **[!UICONTROL Tasks]** フォルダーに保存されます。タスクで作業する場合、タスクを変更し、タスクのドラフトコピーをAEM Formsサーバーに保存できます。

モバイルデバイスのフォームは、アダプティブフォームまたはモバイルフォームになります。Foms アプリケーションで同期可能なフォームは、Forms フォルダーにあります。AEM Forms ワークフローを使用しない AEM Forms Server（OSGi での AEM Forms）で有効にされているフォームを同期することができます。

次のページを参照してください。

* [タスクを開く](/help/forms/using/open-task.md)
* [フォームの操作](/help/forms/using/working-with-form.md)

### オフライン作業 {#working-offline}

オフラインモードであっても、モバイルデバイス上で作業ができます。ネットワークに接続していない場合でも、アプリケーションにログインできます。また、最後に同期したすべてのフォームを実行できます。フォームを同期する方法について詳しくは、「[アプリケーションの同期](/help/forms/using/sync-app.md)」を参照してください。フォームに関連付けられた添付ファイルを同期する場合は、オフラインモードでその添付ファイルを開くこともできます。 オフラインモードでは、フォームの編集、注釈の追加、およびフォームの送信と保存が可能です。フォームは次にオンラインになったときに AEM Forms サーバーと同期します。

詳細については、「[オフラインモードの使用](/help/forms/using/work-offline-mode.md)」を参照してください。

### 注釈の追加 {#adding-annotations}

モバイルデバイス上のフォームに以下を添付できます。

* **メモ**— メモ機能を使用して、手書きメモやテキストメモをフォームに追加できます。 詳しくは、「[メモの追加](/help/forms/using/add-attachments.md#adding-a-note)」を参照してください。

* **画像**-AEM Formsアプリには、モバイルデバイスのカメラ機能やギャラリーを使用する機能が含まれています。 写真注釈を使用すると、写真を関連するフォームに追加することができます。詳しくは、「[写真の追加](/help/forms/using/add-attachments.md#adding-a-photograph)」を参照してください。

### 自動保存 {#autosave}

AEM Forms アプリケーションでユーザーがデータを入力すると、自動保存の機能により一定の間隔でデータが保存されます。AEM Forms アプリケーションの自動保存の機能は、電池切れなどが原因でアプリケーションが終了した場合にデータの損失を防ぐことができます。

「[AEM Forms アプリケーションで自動保存を使用](/help/forms/using/autosave-data-app.md)」を参照。

## AEM インボックスと AEM Forms アプリケーションの機能の違い {#differences-between-aem-inbox-and-aem-forms-app-features}

Two of the prominent ways to launch a Forms-centric workflow are using [AEM Inbox](/help/forms/using/manage-applications-inbox.md) and AEM Forms app. ただし、AEM インボックスの機能と AEM Forms アプリケーションの機能は異なっています。AEM Inbox works only with [Forms-centric workflows](/help/forms/using/aem-forms-workflow.md) while the AEM Forms app works with both Forms-centric workflows as well as process management. For more information on differences between AEM Inbox and AEM Forms app capabilities, see [Actions and capabilities of Form-centric AEM Workflows on OSGi and AEM Forms JEE workflows](capabilities-osgi-jee-workflows.md).

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

AEM Formsアプリは、フィールドワーカーが割り当てられたフォームを使用できるモバイルソリューションを提供します。 アプリケーションはサーバーから完全なデータをキャッシュし、すべての作業をローカルに保存することによって、十分なユーザーエクスペリエンスを提供します。ディスクからのデータは適時の同期更新によってサーバーに送信されます。

AEM Formsアプリは、Backboneモデルを効率的に使用し、モデルに保存されたデータを表示で表示するPhoneGap 5.0ベースのアプリケーションです。 すべてのネイティブ操作は、PhoneGap プラグインによって実行されます。

## AEM Forms アプリケーションのカスタマイズ、構築、配布 {#customize-build-distribute}

>[!NOTE]
>
>AEM Forms アプリケーションソースコードを使用してアプリを構築する場合にのみ適用可能です。

AEM Formsアプリは、組織固有のニーズに合わせて簡単にカスタマイズできます。 アプリケーションのソースコードは AEM Forms とともに提供されます。ソースコードに変更を加え、独自に作業員向けモバイルソリューションを構築できます。アプリケーションへのサインには、会社独自のキーを使用することもできます。

### カスタマイズ {#customize}

アプリケーションをカスタマイズして次のことができます。

**ブランディング**：アプリケーションのアイコン、アプリケーション名、起動の画像、AEM Forms アプリケーション内のページを変更します。テキストを特定の地域のローカライズアプリケーションに変更することもできます。AEM Forms アプリケーションのブランディングについて詳しくは、「[ブランディングのカスタマイズ](/help/forms/using/branding-customization.md)」を参照してください。

**テーマ**: AEM Formsアプリユーザーインターフェイスで、色、フォント、間隔などのスタイルを変更します。 詳しくは、「[テーマのカスタマイズ](/help/forms/using/theme-customization.md)」を参照してください。

**ジェスチャ**: AEM Formsアプリユーザーインターフェイスでの右にスワイプ、左にスワイプなどのジェスチャーを変更します。 詳しくは、「[ジェスチャーのカスタマイズ](/help/forms/using/gesture-customization.md)」を参照してください。

AEM Forms アプリケーションプロジェクトをカスタマイズ用にセットアップする方法について、詳細は次のリンクを参照してください。

* [AEM Forms アプリケーションの環境設定](/help/forms/using/setup-environment-mobile-workspace.md)
* [Visual Studio プロジェクトの設定と Windows アプリケーションの構築](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Xcode プロジェクトの設定と iOS アプリケーションの構築](/help/forms/using/setup-xcode-project-build-installer.md)
* [Eclipse プロジェクトの設定と Android アプリケーションの構築](/help/forms/using/setup-eclipse-project-build-installer.md)

### 構築と配布 {#build-and-distribute}

AEM Forms版アプリのソースコードは、パッケージ共有のAEM Forms版アプリソースパッケージの一部として入手できるadobe-lc-mobileworkspace-src.zipから抽出できます。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. パッケージ共有に移動します

   URL: `https://<server>:<port>/crx/packageshare`.

1. ソースパッケージをダウンロードします。パッケージをダウンロードすると、AEM Forms パッケージマネージャーに追加されます。
1. ダウンロード後、次の場所に移動します。 `https://<server>:<port>/crx/packmgr/index.jsp`、およびinstall `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

1. パッケージをダウンロードするには、ブラウザ `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` ーで開きます。

   ソースパッケージがデバイスにダウンロードされます。

**iOS の場合**：

iOS アプリケーション（.ipa）の作成方法について、詳しくは「[Xcode プロジェクトの設定と iOS アプリの構築](/help/forms/using/setup-xcode-project-build-installer.md)」を参照してください。

For details on how to sign the AEM Forms app with your provisioning profile, see [iOS Code Signing Setup, Process, and Troubleshooting](https://developer.apple.com/support/code-signing/).

**Android の場合**：

For details on how to create an Android app (.apk), refer [Set up the Eclipse project and build the Android app](/help/forms/using/setup-eclipse-project-build-installer.md).

For details on how to sign the AEM Forms app, see [Signing Your Applications](https://developer.android.com/tools/publishing/app-signing.html).

**Windows の場合**：

For details on how to create a Windows app (.appx), refer [Set up the Visual Studio project and build the Windows app](/help/forms/using/setup-visual-studio-project-build-installer.md).

MDM を介したアプリケーションの配布方法について詳しくは、「[AEM Forms アプリケーションの配布](/help/forms/using/distribute-mobile-workspace-app.md)」を参照してください。MDMを介したアプリの配布は、iOSとAndroidにのみ適用できます。

## Mobile Workspace を AEM Forms アプリケーションにアップグレードするための推奨事項 {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

最新バージョンの AEM Forms アプリケーションにアップグレードする場合は、以下のポイントを通読してください。

* **Android に Play ストアから以前のバージョンのアプリケーションをインストールした場合** アプリケーションを Play ストアから直接アップグレードできます。

* **以前のバージョンのアプリケーションがソースコードを使用して構築およびインストールされる場合（iOSとAndroidに適用）**:

   新しいアプリをインストールする前に、すべてのデータをAEM Formsサーバーと同期します。 データが同期されたら、以前のバージョンのアプリケーションをアンインストールし、新しいアプリケーションをインストールします。

