---
title: AEM Forms のアセットとドキュメントの移行
seo-title: AEM Forms のアセットとドキュメントの移行
description: 移行ユーティリティにより、AEM Forms のアセットとドキュメントを AEM 6.3 Forms またはそれ以前のバージョンから AEM 6.4 forms に移行できます。
seo-description: 移行ユーティリティにより、AEM Forms のアセットとドキュメントを AEM 6.3 Forms またはそれ以前のバージョンから AEM 6.4 forms に移行できます。
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 66%

---


# AEM Forms のアセットとドキュメントの移行{#migrate-aem-forms-assets-and-documents}

The Migration utility converts the [Adaptive Forms assets](../../forms/using/introduction-forms-authoring.md), [cloud configrurations](/help/sites-developing/extending-cloud-config.md), and [Correspondence Management assets](/help/forms/using/cm-overview.md) from the format used in the earlier versions to the format used in AEM 6.5 Forms. 移行ユーティリティを実行すると、次の項目が移行されます。

* アダプティブフォームのカスタムコンポーネント
* アダプティブフォームと Correspondence Management のテンプレート
* クラウドの設定情報
* Correspondence Managementとアダプティブフォームアセット

>[!NOTE]
>
>アウトオブプレースアップグレードを実行する場合（Correspondence Management のアセットを移行する場合）は、アセットをインポートするたびに、移行ユーティリティを実行することができます。Correspondence Management を移行する場合は、Forms 互換性パッケージがインストールされている必要があります。

## 移行の方法 {#approach-to-migration}

You can [upgrade](../../forms/using/upgrade.md) to the latest version of AEM Forms 6.5 from AEM Forms 6.4, 6.3, or 6.2 or perform a fresh installation. 以前のインストール環境をアップグレードしたのか、新規インストールを実行したのかに応じて、以下に示すいずれかの手順を実行してください。

**インプレースアップグレードを実行した場合**

インプレースアップグレードを実行した場合、アップグレードインスタンスにはすでにアセットやドキュメントが存在します。ただし、これらのアセットやドキュメントを使用する前に、[AEMFD 互換性パッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)（Correspondence Management 互換性パッケージが含まれています）をインストールする必要があります。

Then you need to update the assets and documents by [running the Migration utility](#runningmigrationutility).

**新規インストールを実行した場合**

If it is an out of place (fresh) installation, before you can use the assets and documents, you will need to install [AEMFD Compatibility package](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) (includes the Correspondence Management Compatibility package).

Then you need to import your asset package (zip or cmp) on the new setup and then update the assets and documents by [running the Migration utility](#runningmigrationutility). Adobeでは、移行ユーティリティを実行した後にのみ、新しいセットアップで新しいアセットを作成することをお勧めします。

[後方互換性に関する要件](/help/sites-deploying/backward-compatibility.md)が変更されたことに伴い、CRX リポジトリ内のいくつかのフォルダーの場所が変更されています。以前の設定から新規環境に対して、依存関係（カスタムライブラリおよびアセット）を手動で書き出し、読み込みます。

## Read before you proceed with the migration {#prerequisites}

Correspondence Management のアセットを移行する場合は、以下の点に注意してください。

* For the assets that are imported from the previous platform, a property gets added: **fd:version=1.0**.
* AEM 6.1 Forms 以降、コメントは初期状態では使用できません。以前に追加したコメントはアセット内で使用できますが、インターフェイスには自動的に表示されません。 コメントを表示させるには、AEM Forms のユーザーインターフェイスで extendedProperties プロパティをカスタマイズする必要があります。
* LiveCycle ES4 など、旧バージョンの一部では Flex RichTextEditor を使用してテキストを編集しましたが、AEM 6.1 Forms 以降では HTML エディターを使用します。このレンダリングにより、フォント、フォントサイズ、フォントマージンの外観は以前のバージョンの作成者ユーザーインターフェイスでの外観と異なる可能性があります。ただし、レターは同じように表示されます。
* テキストモジュールのリストが改善され、別々にレンダリングされるようになりました。外観や表示が今までと異なるところがあります。テキストモジュールのリストを使用している場所で、レターのレンダリングや表示を行うことをお勧めします。
* 移行中に画像コンテンツモジュールは DAM アセットおよびレイアウトに変換され、フラグメントはフォームに追加されるため、これらのモジュールの更新者プロパティは管理者に変更されます。
* アセットのバージョン履歴は移行されず、移行後は使用できなくなります。移行後のバージョン履歴は保持されます。
* AEM 6.1 Forms 以降では、「発行準備完了」の状態は廃止されました。このため、「発行準備完了」の状態にあったすべてのアセットは、変更済みの状態に変更されます。
* AEM Forms 6.3 ではユーザーインターフェイスが更新されているため、カスタマイズを行うための手順も異なります。6.3 よりも前のバージョンのアセットを移行する場合は、カスタマイズをやり直す必要があります。
* レイアウトフラグメントは、/content/apps/cm/layouts/fragmentlayouts/1001 から /content/apps/cm/modules/fragmentlayouts に移動しました。アセットのデータディクショナリ参照には、名前の代わりにデータディクショナリのパスが表示されます。
* タブスペースを使用してテキストモジュールを調整した場合は、再調整する必要があります。詳しくは、「[Correspondence Management - タブスペースを使用したテキスト調整の詳細](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html)」を参照してください。
* Asset Composerの設定がCorrespondence Managementの設定に変更されました。
* アセットは、「Existing Text」や「Existing List」などの名前のフォルダーに移動されます。

## 移行ユーティリティの使用 {#using-the-migration-utility}

### 移行ユーティリティの実行 {#runningmigrationutility}

移行ユーティリティを実行した後で、アセットに変更を加えたり、アセットを作成したりします。移行ユーティリティは、アセットの変更や作成後に実行しないことをお勧めします。移行プロセスの実行中は、Correspondence ManagementまたはAdaptiveFormsアセットのユーザーインターフェイスが開いていないことを確認してください。

移行ユーティリティを初めて実行すると、\[aem-installation-directory]\cq-quickstart\logs\ というパスに「aem-forms-migration.log」という名前でログファイルが作成されます。それ以降は、移行ユーティリティを実行するたびに、Correspondence Management とアダプティブフォームの移行に関する情報（アセットの移行に関する情報など）がこのログファイルに記録されます。

>[!NOTE]
>
>移行ユーティリティを実行する前に、必ず CRX リポジトリのバックアップを作成してください。

1. ブラウザーセッションで、AEM オーサーインスタンスに管理者としてログインします。

1. ブラウザーで次の URL を開きます。

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   ブラウザーに、以下に示す 4 つのオプションが表示されます。

   * AEM Forms アセットの移行
   * アダプティブフォームカスタムコンポーネントの移行
   * アダプティブフォームテンプレートの移行
   * AEM Forms クラウド設定の移行

1. 移行するには、次の手順を実行します。

   * **アセット**&#x200B;を移行する場合は、「AEM Forms アセットの移行」をタップし、次の画面で「**移行を開始**」をタップします。次のものが移行されます。

      * アダプティブフォーム
      * ドキュメントフラグメント
      * テーマ
      * レター
      * データディクショナリ

   >[!NOTE]
   >
   >移行中、「競合が見つかりました...」のような警告メッセージが表示される場合があります。このようなメッセージは、アダプティブフォームの一部のコンポーネントのルールを移行できなかったことを示しています。 例えば、コンポーネントにルールとスクリプトの両方がある場合、スクリプトの後にルールが発生した場合はそのコンポーネントのルールは移行されません。ただし、そのようなルールは、アダプティブフォームのオーサリングでルールエディターを開くことで移行することができます。
   >
   >
   >これらのコンポーネントは、アダプティブフォームのルールエディターで開くことで移行できます。
   >
   >
   >
   >    * カスタムコンポーネントのルールとスクリプト（6.3からアップグレードした場合は不要）を移行するには、「アダプティブFormsカスタムコンポーネントの移行」をタップし、次の画面で「開始の移行」をタップします。 次の移行が行われます。   >
      >
      >
      >        

      * ルールエディターで作成されたルールとスクリプト（6.1 FP1 以降）
      >        * 6.1 以前の UI の「スクリプト」タブで作成されたスクリプト
   >
   >
   >    * テンプレートを移行する（6.3および6.4からアップグレードする場合は不要）には、「Formsテンプレートの適応移行」をタップし、次の画面で「開始の移行」をタップします。 次のものが移行されます。

      >
      >
      >
      >        


      * 古いテンプレート — AEM 6.1Forms以前を使用して/appsの下に作成されたアダプティブフォームテンプレート。 これには、テンプレートコンポーネントに定義されたスクリプトも含まれます。
      >        * 新しいテンプレート — /confの下のテンプレートエディターを使用して作成されたアダプティブフォームテンプレート。 これには、ルールエディターで作成されたルールとスクリプトが含まれます。


   * To migrate adaptive form custom components, tap **Adaptive Forms Custom Components Migration** and in the Custom Components Migration page, tap **Start Migration**. 次のものが移行されます。

      * アダプティブフォーム用に書き込まれたカスタムコンポーネント
      * コンポーネントのオーバーレイ（存在する場合）
   * To migrate adaptive form templates, tap **Adaptive Forms Template Migration** and in the Custom Components Migration page, tap **Start Migration**. 次のものが移行されます。

      * AEM テンプレートエディターを使用して /apps フォルダーまたは /conf フォルダー内に作成されたアダプティブフォームテンプレート
   * 新しいコンテキスト認識クラウドサービスメカニズムを使用するには、AEM Forms クラウド設定サービスを移行する必要があります。このメカニズムには、タッチ操作が可能な UI が用意されています（/conf フォルダーに保管されています）。AEM Formsクラウド設定サービスを移行すると、/etcのクラウドサービスは/confに移動されます。 レガシーパス(/etc)に依存するクラウドサービスのカスタマイズがない場合は、6.5にアップグレードした直後に移行ユーティリティを実行し、以降の作業にはクラウド設定のタッチUIを使用することをお勧めします。 既存のクラウドサービスがカスタマイズされている場合は、移行後のパス（/conf フォルダー）に合わせてカスタマイズ内容を更新するまでは、アップグレード後のセットアップ環境で既存の UI を使用してください。カスタマイズ内容の更新が完了したら、移行ユーティリティを実行してください。

   To migrate **AEM Forms cloud services**, which include the following, tap AEM Forms Cloud Configuration Migration (cloud config migration is independent of AEMFD Compatibility package), tap AEM Forms Cloud Configurations Migration and then on the Configuration Migration page, tap **Start Migration**:

   * フォームデータモデルのクラウドサービス

      * ソースパス：/etc/cloudservices/fdm
      * ターゲットパス：/conf/global/settings/cloudconfigs/fdm
   * Recaptcha

      * ソースパス：/etc/cloudservices/recaptcha
      * ターゲットパス：/conf/global/settings/cloudconfigs/recaptcha
   * Adobe Sign

      * ソースパス：/etc/cloudservices/echosign
      * ターゲットパス：/conf/global/settings/cloudconfigs/echosign
   * Typekit クラウドサービス

      * ソースパス：/etc/cloudservices/typekit
      * ターゲットパス：/conf/global/settings/cloudconfigs/typekit

   移行プロセスの実行時は、ブラウザーウィンドウにそれぞれ以下が表示されます。

   * アセットを更新したとき：アセットは正しく更新されました。
   * 移行が完了したとき：アセットの移行が完了しました。

   完了後は、移行ユーティリティで以下を実行します。

   * **タグをアセットに追加**：タグ「Correspondence Management：移行済みアセット」または「アダプティブフォーム：移行済みアセット」を移行済みのアセットに追加します。これにより、ユーザーは移行済みアセットを識別できます。移行ユーティリティを実行すると、システム内の既存のアセットはすべて移行済みとしてマークされます。
   * **タグを生成**：以前のシステムに存在するカテゴリおよびサブカテゴリはタグとして作成され、これらのタグは AEM 内で関連する Correspondence Management アセットに関連付けられます。例えば、レターテンプレートのカテゴリ（「要求」）とサブカテゴリ（「要求」）は、タグとして生成されます。

















1. 移行ユーティリティが実行を終了した後、[ハウスキーピングタスク](#housekeepingtasks)に進みます。

### 移行ユーティリティ実行後のハウスキーピングタスク {#housekeepingtasks}

移行ユーティリティを実行した後、次のハウスキーピングタスクを行います。[](../../forms/using/import-export-forms-templates.md)

1. レイアウトおよびフラグメントレイアウトのXFAバージョンが3.3以降であることを確認します。 古いバージョンのレイアウトとフラグメントレイアウトを使用している場合は、レターのレンダリングで問題が発生する可能性があります。 古いXFAのバージョンを最新バージョンに更新するには、次の手順を実行します。

   1. [XFAをzipファイルとしてFormsユーザーインターフェイス](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) からダウンロードします。
   1. ファイルを解凍します。
   1. 最新の Designer で XFA ファイルを開き、保存します。XFA が最新バージョンに更新されます。
   1. XFA を Forms ユーザーインターフェイスでアップロードします。

1. 移行前に以前のシステムで発行されたすべてのアセットを発行します。移行ユーティリティは、オーサーインスタンスでのみアセットを更新して、アセットを発行する必要のあるパブリッシュインスタンスでアセットを更新します。
1. AEM Forms6.4および6.5では、formsユーザーグループの権限の一部が変更されています。 ユーザーが XDP やスクリプトを含むアダプティブフォームをアップロードしたりコードエディターを使用したりできるようにするには、そのユーザーを forms-power-users グループに追加する必要があります。同様に、template-authors グループのユーザーは、ルールエディターのコードエディターを使用できなくなります。ユーザーがコードエディターを使用できるようにするには、そのユーザーを af-template-script-writers グループに追加します。For instructions on adding users to groups, see [Managing Users and User Groups](/help/communities/users.md).

