---
title: AEM Forms アプリケーション
seo-title: AEM Forms app
description: AEM Formsアプリを使用すると、フィールドワーカーがモバイルデバイスでアダプティブフォームを使用できるようになります。
seo-description: AEM Forms app enables your field workers to use adaptive forms on their mobile devices.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 37%

---

# AEM Forms アプリケーションの概要 {#aem-forms-app}

## 概要 {#overview}

AEM Forms App では、サーバーに基づいて、モバイルデバイス上のアダプティブフォーム、モバイルフォーム、フォームセットを同期することができます。 [OSGi 上の Forms 中心ワークフロー](/help/forms/using/aem-forms-workflow.md)または JEE 上の Forms ワークフローを定義することができます。例えば、銀行会社を経営し、AEM Formsを使用して顧客のアプリケーションとコミュニケーションを管理するとします。 顧客がフォームに入力し、確認用に送信します。 モバイルデバイスでフォームを有効にした場合、顧客はAEM Formsアプリでフォームに入力できます。 また、モバイルデバイスで検証フォームを有効にすることで、検証ワークフローを管理することもできます。 フィールドワーカーは、モバイルデバイスを顧客に持ち運び、詳細を確認し、フォームを送信できます。 AEM FormsアプリはAEM Formsサーバーと同期し、モバイルデバイス用に有効なフォームを取得します。 アプリケーションがオフラインの場合、データはローカルに保存されます。

AEM Forms アプリケーションのソースコードは、ソフトウェアディストリビューションにより、使用することができます。ソフトウエア配布のソースコードパッケージは、`adobe-aemfd-forms-app-src-pkg-<version>.zip` として入手できます。

AEM Forms アプリケーションは、iOS、Android、および Windows デバイスでサポートされます。Android 向けの AEM Forms アプリケーションは Google Play から、iOS 向けの AEM Forms アプリケーションは App Store から、Windows 向けの AEM Forms アプリケーションは Windows ストアからインストールできます。

    [ ! [google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms&amp;hl=ja)
    
    [ ! [app_store](assets/app_store.png)](https://itunes.apple.com/jp/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ! [microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

iOS、Android または Windows デバイスにアプリをインストール、カスタマイズ、配布するには、 [AEM Formsアプリのカスタマイズ、ビルドおよび配布](#customize-build-distribute).

## 前提条件 {#prerequisites}

AEM FormsアプリにはAEM Formsサーバーが必要です。 ユーザーは、AEM Forms サーバーで作成したフォームのレンダリングを行い、フォームに記入して、ドラフトとして保存し、送信します。デスクトップアプリケーションはサーバーに接続し、サーバーから有効なフォームを取得します。 AEM Formsアプリはサーバーと同期し、フォームがデスクトップアプリケーションに読み込まれるとすぐに、ユーザーはオフラインで作業できます。 アプリがオフラインの場合、データはデバイスに保存され、アプリがオンラインの場合にデータがサーバーと同期されます。

### AEM Forms Workflow を使用したサーバーとのAEM Formsアプリ {#aem-forms-app-with-servers-using-aem-forms-workflow}

AEM Forms Workflow サーバーがある場合は、AEM Formsアプリでフォームをタスクとしてレンダリングできます。 例えば、銀行会社を経営し、顧客がサービスを利用するための申し込みを行ったとします。 申込フォームはアダプティブフォームで、顧客からの情報を受け入れ、レビュー用に送信フォームとして保存します。 管理者は、申し込みをレビューし、検証リクエストをフィールドワーカーに転送します。 転送されたアプリケーションは、フィールドワーカーのアプリ内の検証フォームをタスクとして有効にします。 フィールドワーカーはモバイルデバイスを顧客まで持参し、詳細を検証します。

### OSGi でのForms中心のワークフローを使用する、サーバーとのAEM Formsアプリ {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

AEM Formsサーバーがある場合は、アダプティブフォームをAEM Inbox アプリケーションとして、およびAEM Formsアプリケーションでタスクをレンダリングできます。 例えば、銀行会社を経営し、顧客がサービスを利用するための申し込みを行ったとします。 申込フォームは、顧客からの情報を受け取り、レビュー用の送信として保存するアダプティブフォームに関連付けられています。 管理者は、タスクをレビューし、フィールドワーカーに対する検証リクエストを承認します。 フィールドワーカーはモバイルデバイスを顧客まで持参し、詳細を検証します。

### AEM Forms Workflow を使用しないサーバーを備えたスタンドアロンフォームまたはAEM Formsアプリ {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

AEM Forms Workflow を使用しないAEM Formsサーバーは、OSGi 上のAEM Forms、またはスタンドアロンのモバイルフォームやアダプティブフォームです。 AEM Forms アプリケーションは、[OSGi](/help/sites-deploying/configuring-osgi.md) に AEM Forms を実装して機能します。AEM Forms アプリケーション用に有効にして公開するフォームは、アプリケーション内で利用できます。

フォームをアプリケーションにダウンロードして、オフラインで使用することができます。例えば、金融関係の会社を経営していて、顧客がサイト上で申込書を記入するとします。申込フォームはアダプティブフォームで、顧客からの情報を受け取り、レビュー用に保存します。 管理者は、フォームを確認し、AEMオーサーインスタンスで検証フォームを作成します。 管理者は、AEM Formsアプリとの同期を有効にして、公開します。 検証フォームがAEM Formsアプリで使用可能な場合、フィールドエージェントはモバイルデバイスを使用して、顧客の詳細を検証できます。 モバイルデバイスがサーバーと同期し、検証フォームがアプリに読み込まれます。 フィールドエージェントは顧客を訪問し、詳細を確認し、データをドラフトとして保存したり、検証フォームを送信したりできます。 アプリがオンラインになるたびに、フォームはサーバーと同期されます。

AEM Forms アプリケーションでは、次のようにフォームを同期します。

1. オーサーインスタンスでは、フォームを選択し、**[!UICONTROL 「プロパティの表示」]**&#x200B;をクリックします。

1. プロパティページで、「**[!UICONTROL 詳細]**」をクリックします。
1. 「詳細」で、次のオプションを有効にします。 **[!UICONTROL AEM Forms App と同期]** を選択し、 **[!UICONTROL 保存]**.

フォームが公開されると、アプリケーションはサーバーと同期してフォームを取得します。 複数のフォームを同期するには、オーサーインスタンスで、Forms Manager で複数のフォームを選択し、「 **[!UICONTROL AEM Forms App と同期]**.

## モバイルデバイスのサポート {#mobile-device-support}

詳しくは、 [AEM Formsアプリ（旧称 Mobile Workspace）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Formsアプリの主な機能 {#key-features-of-aem-forms-app}

### AEM FormsサーバーとのAEM Formsアプリ {#aem-forms-app-with-aem-forms-servers}

アプリをAEM Formsサーバーと同期して、モバイルデバイス上でフォームを操作できます。

AEM Forms Workflow サーバーでは、フォームを、Workbench プロセスとAEM Inbox アプリケーションのスタートポイントに関連付けることができます。 AEM Inbox アプリケーションには、アダプティブフォームを関連付けることができます。 スタートポイントには、アダプティブフォーム、HTML5 のフォーム、または関連付けられたフォームセットを含めることができます。 スタートポイントはタスクとして送信することも、タスクをドラフトとして保存することもできます。 AEM インボックスアプリケーションとスタートポイントとの違いについて詳しくは、[OSGi 上の Forms ベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能](capabilities-osgi-jee-workflows.md)を参照してください。

AEM FormsワークフローがないAEM Formsサーバーの場合、アプリで同期が有効になっているフォームがAEM Formsアプリでレンダリングされます。 Formsは、アプリの「 Forms 」タブに表示され、ドラフトとして送信または保存できます。 アダプティブフォームとモバイルフォームは、デスクトップアプリケーションでサポートされています。

1. **タスクまたはフォームをドラフトとして保存する**

   「ドラフトとして保存」オプションでは、入力済みのデータや関連フォームに添付されたファイルと共に、タスクまたはフォームのスナップショットが保存されます。 下書きはモバイルデバイスに保存され、後で取得できるようにAEM Formsサーバーと同期されます。

   詳しくは、 [タスクまたはフォームをドラフトとして保存する](/help/forms/using/save-as-draft.md).

1. **フォームをテンプレートとして保存**

   ユーザーがフォームに入力する際に、いくつかのフィールドへの入力が同じままになる場合があります。 このような場合は、すべてのインスタンスで同じ値を必要とするフィールドに入力し、フォームまたはドラフトをテンプレートとして保存できます。 これで、テンプレートのインスタンスを作成するたびに、指定されたフィールドには、テンプレートで指定された値が既に入力されています。 これにより、フォーム入力に必要な時間と労力を節約できます。

   詳しくは、 [フォームをテンプレートとして保存](/help/forms/using/save-forms-and-start-points-as-templates.md).

### タスクとフォームの使用 {#working-with-tasks-and-forms}

アプリをAEM Forms Workflow サーバーと同期して、モバイルデバイスでタスクやフォームを操作できます。

モバイルデバイスのタスクには、アダプティブフォーム、HTML5 フォームまたはフォームセットが含まれ、さらに添付ファイルおよび[サマリー URL](/help/forms/using/getting-task-variables-summary-url.md) を含めることもできます。デフォルトでは、自分に割り当てられたタスクが **[!UICONTROL Tasks]** フォルダーに保存されます。タスクで作業する場合、タスクを変更して、そのタスクのドラフトコピーを AEM Forms サーバーに保存できます。

モバイルデバイス上のフォームは、アダプティブフォームまたはモバイルフォームにすることができます。 Forms forms アプリで同期が有効になっている場合は、Formsフォルダーで入手できます。 AEM Formsワークフローを使用せずに、AEM Formsサーバーで有効にしたフォームを同期できます (OSGi 上のAEM Forms)。

次のページを参照してください。

* [タスクを開く](/help/forms/using/open-task.md)
* [フォームの操作](/help/forms/using/working-with-form.md)

### オフラインでの作業 {#working-offline}

モバイルデバイスでは、オフラインモードで作業できます。 ネットワークに接続していない場合でも、アプリケーションにログインでき、最後にオンラインになったときにデバイスと同期されたすべてのフォームで作業できます。 フォームを同期する方法について詳しくは、 [アプリの同期](/help/forms/using/sync-app.md). フォームに関連付けられた添付ファイルを同期する場合、オフラインモードでその添付ファイルを開くこともできます。オフラインモードでは、フォームの編集、注釈の追加、フォームの送信または保存をおこなうことができます。 フォームは、次回オンラインになるときにAEM Formsサーバーと同期されます。

詳しくは、 [オフラインモードでの作業](/help/forms/using/work-offline-mode.md).

### 注釈の追加 {#adding-annotations}

モバイルデバイス上のフォームに次の添付ファイルを追加できます

* **メモ** - メモ機能を使用して、手書きメモまたはテキストメモを追加できます。詳しくは、「[メモの追加](/help/forms/using/add-attachments.md#adding-a-note)」を参照してください。

* **写真** - AEM Forms アプリケーションには、モバイルデバイスのカメラ機能またはギャラリーを使用する機能があります。写真注釈を使用すると、写真を関連するフォームに追加することができます。詳しくは、「[写真の追加](/help/forms/using/add-attachments.md#adding-a-photograph)」を参照してください。

### 自動保存 {#autosave}

ユーザーがAEM Formsアプリにデータを入力すると、自動保存機能によって一定の間隔でデータが保存されます。 AEM Formsアプリの自動保存機能を使用すると、バッテリ不足などの状況でアプリが閉じた場合にデータの損失を防ぐことができます。

詳しくは、 [AEM Formsアプリでの自動保存の使用](/help/forms/using/autosave-data-app.md).

## AEM インボックスの機能と AEM Forms アプリケーションの機能との違い {#differences-between-aem-inbox-and-aem-forms-app-features}

Forms 中心のワークフローを起動するには、[AEM インボックス](/help/forms/using/manage-applications-inbox.md)と AEM Forms アプリケーションの 2 つの方法があります。ただし、AEM インボックスの機能と AEM Forms アプリケーションの機能は異なっています。AEM Inbox は、 [Forms中心のワークフロー](/help/forms/using/aem-forms-workflow.md) 一方、AEM Formsアプリは、Forms中心のワークフローとプロセス管理の両方で動作します。 AEM インボックスアプリケーションと AEM Forms アプリケーションの機能の違いについて詳しくは、[OSGi 上の Forms ベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能](capabilities-osgi-jee-workflows.md)を参照してください。

## サポートされるフォーム {#supported-forms}

AEM Formsアプリでサポートされるフォームタイプ：

### アダプティブフォーム {#adaptive-form}

AEM Formsアプリでは、ユーザーの入力に動的に適応するアダプティブフォームがサポートされています。 遅延読み込みアダプティブフォームもサポートされています。

### モバイルフォーム {#mobile-form}

AEM Formsでモバイルデバイス用のフォームを作成できます。 モバイルフォームは、モバイルデバイスでは、HTMLに応じて適応するデバイスフォームとしてレンダリングされます。

### フォームセット {#formset}

フォームセットを使用すると、1 つのサービスまたはプロセスに関連する複数のフォームをグループ化して、ビジネスプロセスを自動化し、エンドユーザーに表示できます。 このシナリオでは、ユーザーはセット全体を 1 つとして入力でき、個々のフォームやプロセスをファイル化、送信、追跡する必要はありません。

>[!NOTE]
>
>AEM Forms Workflow(JEE 上のAEM Forms) が必要です。

## AEM Formsアプリの仕組み {#how-aem-forms-app-works}

AEM Forms アプリケーションは、フィールドワーカーが各自に割り当てられたフォームで作業するためのモバイルソリューションを提供します。アプリケーションは、サーバーから完全なデータをキャッシュし、すべての作業をローカルに保存することで、効率的なユーザーエクスペリエンスを提供します。 ディスクのデータは、適時の同期更新を通じてサーバに送信されます。

AEM Forms アプリケーションは、モデルに保存されたデータをビューで表示するために Backbone モデルが効果的に使用される PhoneGap 5.0 ベースのアプリケーションです。すべてのネイティブ操作は、PhoneGap プラグインを通じて実行されます。

## AEM Formsアプリのカスタマイズ、ビルドおよび配布 {#customize-build-distribute}

>[!NOTE]
>
>AEM Formsアプリのソースコードを使用してアプリを構築する場合にのみ適用できます。

AEM Forms アプリケーションは、組織特有のニーズに合わせて簡単にカスタマイズできます。アプリケーションのソースコードは、AEM Formsと共に提供されます。 ソースコードを変更し、独自のモバイルワーカーソリューションを構築できます。 また、アプリに独自のエンタープライズキーで署名することもできます。

### カスタマイズ {#customize}

以下の目的でアプリをカスタマイズできます。

**ブランディング**:AEM Formsアプリのアプリアイコン、アプリ名、起動画像およびページを変更します。 テキストを変更して、特定の地域のアプリをローカライズすることもできます。 AEM Formsアプリのブランディングについて詳しくは、 [ブランディングのカスタマイズ](/help/forms/using/branding-customization.md).

**テーマ**：AEM Forms アプリケーションユーザーインターフェイスでのカラー、フォント、間隔などのスタイルを変更します。詳しくは、「[テーマのカスタマイズ](/help/forms/using/theme-customization.md)」を参照してください。

**ジェスチャー**：AEM Forms アプリケーションユーザーインターフェイスでの右にスワイプ、左にスワイプなどのジェスチャーを変更します。詳しくは、 [ジェスチャのカスタマイズ](/help/forms/using/gesture-customization.md).

カスタマイズのためのAEM Formsアプリプロジェクトの設定について詳しくは、以下を参照してください。

* [AEM Forms アプリケーションの環境設定](/help/forms/using/setup-environment-mobile-workspace.md)
* [Visual Studio プロジェクトの設定と Windows アプリケーションの構築](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Xcode プロジェクトの設定と iOS アプリケーションの構築](/help/forms/using/setup-xcode-project-build-installer.md)
* [Eclipse プロジェクトの設定と Android アプリケーションの構築](/help/forms/using/setup-eclipse-project-build-installer.md)

### 構築と配布 {#build-and-distribute}

AEM Forms アプリケーションのソースコードは、ソフトウエア配布で AEM Forms アプリケーションソースパッケージの一部として入手可能な `adobe-lc-mobileworkspace-src.zip` から抽出できます。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. 選択 **[!UICONTROL Adobe Experience Manager]** は、ヘッダーメニューで使用できます。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージ名を選択し、「 」を選択します。 **[!UICONTROL 使用許諾契約書に同意する]**&#x200B;をクリックし、次を選択します。 **[!UICONTROL ダウンロード]**.
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

**iOS向け**:

iOSアプリ (.ipa) の作成方法について詳しくは、 [Xcode プロジェクトの設定とiOSアプリの構築](/help/forms/using/setup-xcode-project-build-installer.md).

プロビジョニングプロファイルを使用した AEM Forms アプリケーションへの署名方法について詳しくは、[iOS コード署名の設定、処理、トラブルシューティング](https://developer.apple.com/support/code-signing/)を参照してください。

**Android の場合**：

Android アプリケーション（.apk）の作成方法について詳しくは、[Eclipse プロジェクトの設定と Android アプリケーションの構築](/help/forms/using/setup-eclipse-project-build-installer.md)を参照してください。

AEM Forms アプリケーションへの署名方法について詳しくは、[アプリケーションへの署名](https://developer.android.com/tools/publishing/app-signing.html)を参照してください。

**Windows の場合**：

Windows アプリケーション（.appx）の作成方法について詳しくは、[Visual Studio プロジェクトの設定と Windows アプリケーションの構築](/help/forms/using/setup-visual-studio-project-build-installer.md)を参照してください。

MDM を介したアプリケーションの配布方法について詳しくは、「[AEM Forms アプリケーションの配布](/help/forms/using/distribute-mobile-workspace-app.md)」を参照してください。MDM を介したアプリ配信は、iOS および Android にのみ対応しています。

## Recommendationsを使用して Mobile Workspace をAEM Formsアプリにアップグレード {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

最新バージョンのAEM Formsアプリケーションにアップグレードする場合は、次のポイントを必ずお読みください。

* **Android に Play ストアから以前のバージョンのアプリケーションをインストールした場合** アプリケーションを Play ストアから直接アップグレードできます。

* **以前のバージョンのアプリケーションがソースコードを使用してビルドおよびインストールされている場合（iOS および Android に適用）**：

  新しいアプリケーションをインストールする前に、すべてのデータを AEM Forms サーバーと同期します。データが同期されたら、以前のバージョンのアプリケーションをアンインストールし、新しいアプリケーションをインストールします。
