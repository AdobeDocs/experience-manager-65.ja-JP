---
title: AEM Forms のアセットとドキュメントの移行
description: 移行ユーティリティを使用すると、Adobe Experience Manager(AEM)FormsのアセットとドキュメントをAEM 6.3 Forms以前のバージョンからAEM 6.4 Formsに移行できます。
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
docset: aem65
role: Admin
exl-id: 0f9aab7d-8e41-449a-804b-7e1bfa90befd
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 42%

---

# AEM Forms のアセットとドキュメントの移行 {#migrate-aem-forms-assets-and-documents}

移行ユーティリティは、 [アダプティブFormsアセット](../../forms/using/introduction-forms-authoring.md), [クラウド設定](/help/sites-developing/extending-cloud-config.md)、および [Correspondence Management アセット](/help/forms/using/cm-overview.md) 以前のバージョンで使用されていた形式から、Adobe Experience Manager(AEM)6.5 Formsで使用されていた形式に変換します。 移行ユーティリティを実行すると、次の項目が移行されます。

* アダプティブフォームのカスタムコンポーネント
* アダプティブフォームと Correspondence Management テンプレート
* クラウドの設定情報
* Correspondence Management とアダプティブフォームのアセット

>[!NOTE]
>
>アウトオブプレースアップグレードがある場合、Correspondence Management アセットの場合、アセットを読み込むたびに移行を実行できます。 Correspondence Management を移行するには、Forms互換性パッケージをインストールする必要があります。

## 移行のアプローチ {#approach-to-migration}

以下が可能です。 [アップグレード](../../forms/using/upgrade.md) AEM Forms 6.4、6.3、6.2 または 6.2 からAEM Forms 6.5 の最新バージョンにアップグレードするか、新しいインストールに移行します。 以前のインストールをアップグレードしたか、新規インストールを実行したかに応じて、次のいずれかを実行する必要があります。

**インプレースアップグレードがある場合**

インプレースアップグレードを実行した場合、アップグレードされたインスタンスには既にアセットとドキュメントが含まれています。 ただし、アセットとドキュメントを使用する前に、 [AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) （Correspondence Management 互換性パッケージを含む）

その後、次の方法でアセットとドキュメントを更新する必要があります： [移行ユーティリティの実行](#runningmigrationutility).

**アウトオブプレースインストールがある場合**

アセットとドキュメントを使用する前に、（新規の）インストールを行う場合は、 [AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) （Correspondence Management 互換性パッケージを含む）。

次に、新しい設定でアセットパッケージ（zip または cmp）を読み込み、次の方法でアセットとドキュメントを更新する必要があります。 [移行ユーティリティの実行](#runningmigrationutility). Adobeでは、移行ユーティリティを実行した後に、新しい設定でアセットを作成することをお勧めします。

期限 [後方互換性関連](/help/sites-deploying/backward-compatibility.md) を変更すると、crx-repository 内のいくつかのフォルダーの場所が変更されます。 以前の設定から新しい環境に、依存関係（カスタムライブラリとアセット）を手動で書き出して読み込みます。

## 移行を進める前に {#prerequisites}

Correspondence Management のアセットを移行する場合は、以下の点に注意してください。

* 旧バージョンのプラットフォームからインポートしたアセットの場合、「**fd:version=1.0**」というプロパティが追加されます。
* AEM 6.1 Forms 以降、コメントは初期状態では使用できません。以前に追加されたコメントはアセット内で使用できますが、インターフェイスには自動で表示されません。AEM Formsユーザーインターフェイスの extendedProperties プロパティをカスタマイズして、コメントを表示します。
* LiveCycleES4 などの以前のバージョンの一部では、テキストはFlex RichTextEditor を使用して編集されましたが、AEM 6.1 Forms以降はHTMLエディターが使用されます。 このレンダリングとフォントの外観、フォントサイズ、フォントマージンは、作成者ユーザーインターフェイスの以前のバージョンとは異なる場合があります。 ただし、レンダリング時にはレターは同じように見えます。
* テキストモジュール内のリストが改善され、別の方法でレンダリングされるようになりました。 視覚的な違いが生じる場合があります。 Adobeでは、テキストモジュールでリストを使用している場所でレンダリングし、レターを表示することをお勧めします。
* 画像コンテンツモジュールは移行時に DAM アセットおよびレイアウトに変換され、フラグメントはフォームに追加されるので、これらのモジュールの更新者プロパティは管理者に変更されます。
* アセットのバージョン履歴は移行されず、移行後は使用できません。 移行後のバージョン履歴は保持されます。
* AEM 6.1 Forms 以降では、「発行準備完了」の状態は廃止されました。このため、「発行準備完了」の状態にあったすべてのアセットは、変更済みの状態に変更されます。
* AEM Forms 6.3 ではユーザーインターフェイスが更新されたので、カスタマイズを実行する手順も異なります。 6.3 以前のバージョンから移行する場合は、カスタマイズをやり直します。
* レイアウトフラグメントの移動元 `/content/apps/cm/layouts/fragmentlayouts/1001` から `/content/apps/cm/modules/fragmentlayouts`. アセットのデータディクショナリ参照には、名前の代わりにデータディクショナリのパスが表示されます。
* テキストモジュールでの配置に使用するタブスペースは、すべて再調整する必要があります。 詳しくは、 [Correspondence Management — タブ間隔を使用したテキストの配置](https://helpx.adobe.com/jp/aem-forms/kb/cm-tab-spacing-limitations.html).
* Asset Composer の設定は、Correspondence Management 設定に変更されました。
* アセットは、「Existing Text」や「Existing List」などの名前のフォルダーに移動されます。

## 移行ユーティリティの使用 {#using-the-migration-utility}

### 移行ユーティリティの実行 {#runningmigrationutility}

アセットで変更するかアセットを作成する前に、移行ユーティリティを実行します。 Adobeでは、アセットを変更または作成した後は、ユーティリティを実行しないことをお勧めします。 移行プロセスの実行中は、Correspondence Management アセットまたはアダプティブフォームアセットのユーザーインターフェイスが開いていないことを確認してください。

移行ユーティリティをはじめて実行する場合、`\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log` というパスと名前でログが作成されます。このログは、アセットの移動など、Correspondence Management および Adaptive Formsの移行情報で更新され続けます。

>[!NOTE]
>
>移行ユーティリティを実行する前に、crx リポジトリのバックアップを作成していることを確認します。

1. ブラウザーセッションで、AEMオーサーインスタンスに管理者としてログインします。

1. ブラウザーで次の URL を開きます。

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   ブラウザーに、以下に示す 4 つのオプションが表示されます。

   * AEM Forms アセットの移行
   * アダプティブフォームカスタムコンポーネントの移行
   * アダプティブフォームテンプレートの移行
   * AEM Forms クラウド設定の移行

1. 移行を実行するには、以下の手順を実行します。

   * **アセット**&#x200B;を移行する場合は、「AEM Forms アセットの移行」をタップし、次の画面で「**移行を開始**」をタップします。次のものが移行されます。

      * アダプティブフォーム
      * ドキュメントフラグメント
      * テーマ
      * レター
      * データディクショナリ

   >[!NOTE]
   >
   >アセットの移行中、「競合が見つかりました」のような警告メッセージが表示される場合があります。このようなメッセージは、アダプティブフォームのコンポーネントのいくつかのルールを移行できなかったことを示します。例えば、コンポーネントにルールとスクリプトの両方がある場合、スクリプトの後にルールが発生した場合はそのコンポーネントのルールは移行されません。アダプティブフォームのオーサリングで[ルールエディターを開いて、このようなルールを移行](#migrate-rules)できます。

   * アダプティブフォームのカスタムコンポーネントを移行する場合は、「**アダプティブフォームカスタムコンポーネントの移行**」をタップし、カスタムコンポーネントの移行ページで「**移行を開始**」をタップします。次のものが移行されます。

      * アダプティブForms用に作成されたカスタムコンポーネント
      * コンポーネントオーバーレイ（存在する場合）。

   * アダプティブフォームのテンプレートを移行する場合は、「**アダプティブフォームテンプレートの移行**」をタップし、カスタムコンポーネントの移行ページで「**移行を開始**」をタップします。次のものが移行されます。

      * AEM テンプレートエディターを使用して `/apps` フォルダーまたは `/conf` フォルダー内に作成されたアダプティブフォームテンプレート。

   * AEM Forms Cloud Configuration Services を移行して、新しいコンテキスト対応クラウドサービスパラダイムを使用します。これには、タッチ操作対応 UI( `/conf`) をクリックします。 AEM Forms クラウド設定サービスを移行すると、`/etc` 内のクラウドサービスが `/conf` に移動します。従来のパス (`/etc`) の場合、Adobeでは、6.5 にアップグレードした後に移行ユーティリティを実行することをお勧めします。その後の作業には、クラウド設定のタッチ UI を使用します。 既存のクラウドサービスがカスタマイズされている場合は、移行後のパス（`/conf` フォルダー）に合わせてカスタマイズ内容を更新するまでは、アップグレード後のセットアップ環境で既存の UI を使用してください。カスタマイズ内容の更新が完了したら、移行ユーティリティを実行してください。

   移行する **AEM Forms cloud services**&#x200B;以下を含む「 AEM Forms Cloud Configuration Migration 」をタップします（クラウド設定の移行は AEMFD 互換性パッケージとは独立しておこなわれます）。「 AEM Formsクラウド設定の移行」をタップし、設定の移行ページでをタップします。 **移行を開始**:

   * フォームデータモデルのクラウドサービス

      * ソースパス：`/etc/cloudservices/fdm`
      * ターゲットパス：`/conf/global/settings/cloudconfigs/fdm`

   * reCAPTCHA

      * ソースパス：`/etc/cloudservices/recaptcha`
      * ターゲットパス：`/conf/global/settings/cloudconfigs/recaptcha`

   * Adobe Sign

      * ソースパス：`/etc/cloudservices/echosign`
      * ターゲットパス：`/conf/global/settings/cloudconfigs/echosign`

   * Typekit クラウドサービス

      * ソースパス：`/etc/cloudservices/typekit`
      * ターゲットパス：`/conf/global/settings/cloudconfigs/typekit`

   移行プロセスの実行時は、ブラウザーウィンドウにそれぞれ以下が表示されます。

   * アセットが更新されると、アセットが正常に更新されます。
   * 移行が完了したら：アセットの移行が完了しました。

   実行時に、移行ユーティリティは次の操作を実行します。

   * **タグをアセットに追加**：タグ「Correspondence Management：移行済みアセット」または「アダプティブフォーム：移行済みアセット」を移行済みのアセットに追加します。これにより、ユーザーは移行済みアセットを識別できます。移行ユーティリティを実行するときは、システム内の既存のアセットはすべて移行済みとしてマークされます。
   * **タグを生成**：以前のシステムに存在するカテゴリおよびサブカテゴリはタグとして作成され、これらのタグは AEM 内で関連する Correspondence Management アセットに関連付けられます。例えば、レターテンプレートのカテゴリ（要求）およびサブカテゴリ（要求）は、タグとして生成されます。

1. 移行ユーティリティが実行を終了した後、[ハウスキーピングタスク](#housekeepingtasks)に進みます。

#### ルールエディターを使用したルールの移行 {#migrate-rules}

これらのコンポーネントは、アダプティブFormsエディターのルールエディターで開くことで移行できます。

* カスタムコンポーネントのルールとスクリプトを移行する場合は、「アダプティブフォームカスタムコンポーネントの移行」をタップし、次の画面で「移行を開始」をタップします（バージョン 6.3 をアップグレードする場合は、この移行手順を実行する必要はありません）。次のものが移行されます。

   * ルールエディターで作成されたルールとスクリプト（6.1 FP1 以降）

   * 6.1 以前の UI の「スクリプト」タブで作成されたスクリプト

* テンプレートを移行する場合は、「アダプティブフォームテンプレートの移行」をタップし、次の画面で「移行を開始」をタップします（バージョン 6.3 および 6.4 をアップグレードする場合は、この移行手順を実行する必要はありません）。次のものが移行されます。

   * 古いテンプレート - AEM 6.1 Forms 以前を使用して /apps に作成されたアダプティブフォームテンプレート。これには、テンプレートコンポーネントに定義されたスクリプトも含まれます。

   * 新しいテンプレート — テンプレートエディターを使用して作成されたアダプティブフォームテンプレートが `/conf`. これには、ルールエディターで作成されたルールとスクリプトが含まれます。

### 移行ユーティリティ実行後のハウスキーピングタスク {#housekeepingtasks}

移行ユーティリティを実行した後、次のハウスキーピングタスクを実行します。

1. レイアウトおよびフラグメントレイアウトの XFA バージョンが 3.3 以降であることを確認します。 旧バージョンのレイアウトおよびフラグメントレイアウトを使用している場合、レターのレンダリングで問題が発生する可能性があります。古い XFA のバージョンを最新のバージョンに更新するには、次の手順を実行します。

   1. Forms ユーザーインターフェイスから [XFA を zip ファイルとしてダウンロード](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p)します。
   1.  ファイルを解凍します。
   1. 最新の Designer で XFA ファイルを開き、保存します。 XFA のバージョンが最新のバージョンに更新されます。
   1. Formsユーザーインターフェイスで XFA をアップロードします。

1. 移行前に以前のシステムで公開されたすべてのアセットを公開します。 移行ユーティリティは、オーサーインスタンス上でのみアセットを更新し、パブリッシュインスタンス上でアセットを更新するには、アセットを公開する必要があります。

1. AEM Forms 6.4 および 6.5 では、フォームユーザーグループの権限が一部変更されています。任意のユーザーが XDP やスクリプトを含むアダプティブFormsをアップロードしたり、コードエディターを使用したりできるようにするには、それらのユーザーを forms-power-users グループに追加する必要があります。 同様に、 template-authors は、ルールエディターでコードエディターを使用できなくなりました。 ユーザーがコードエディターを使用できるようにするには、ユーザーを af-template-script-writers グループに追加します。 ユーザーをグループに追加する方法については、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。
