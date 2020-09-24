---
title: フォーム管理の概要
seo-title: フォーム管理の概要
description: AEM Forms は、アダプティブフォームおよび関連アセットを管理するためのツールを提供します。本記事では、主なフォーム管理機能およびユーザーインターフェイス要素を紹介します。
seo-description: AEM Forms は、アダプティブフォームおよび関連アセットを管理するためのツールを提供します。本記事では、主なフォーム管理機能およびユーザーインターフェイス要素を紹介します。
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 66%

---


# フォームの管理の概要 {#introduction-to-managing-forms}

AEM [!DNL Forms] provides simplified yet powerful user interface to create and manage forms, documents, themes, letters, document fragments, data dictionaries, and related assets. 開発者のデスクトップから、ポータルサーバーでのエンドユーザーへの提供まで、フォーム、ドキュメントおよび関連アセットのライフサイクル全体を管理するために役立ちます。You can use the AEM [!DNL Forms] user interface to:

* Access AEM [!DNL Forms] components
* AEM [!DNL Forms] 設定へのアクセス

>[!NOTE]
>
>その他のAEMツールおよびオプションについて詳しくは、「 [オーサリング](/help/sites-authoring/author.md)」を参照してください。

## AEM Forms コンポーネントへのアクセス {#access-aem-forms-components}

AEM には、フォーム、ドキュメントおよび関連アセットを作成するためのオプションに加えて、サイトの作成、アセットの作成、AEM インスタンスの管理などのオプションが用意されています。You can click the ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Experience Manager logo to navigate to all the available tools. Along with links to the consoles of other components, it also contains links for AEM [!DNL Forms]. To navigate to AEM [!DNL Forms], click the Experience Manager logo ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > navigation ![compass](assets/compass.png) > **[!UICONTROL Forms]**. 以下のコンソールのリンクが表示されます。

* フォームとドキュメント
* テーマ
* レター
* ドキュメントフラグメント
* データディクショナリ

   ![AEM Formsコンソール](assets/aem_forms_console_new.png)

### フォームとドキュメント  {#forms-documents}

フォームとドキュメントには、インタラクティブ通信、アダプティブフォーム、アダプティブフォームフラグメント、フォームセットを作成するためのオプションが用意されています。Only for AEM [!DNL Forms] on JEE, Forms &amp; Documents provides an option to import files from local storage and sync AEM [!DNL Forms] assets with Workbench.

The create button is the starting point of the process of creating or uploading AEM [!DNL Forms] asset. 次のオプションを使用して、作成できます。

* **対話型通信**:インタラクティブコミュニケーションは、HTMLベースのデジタル通信、ステートメント、ドキュメントに対応した、パーソナライズされたインタラクティブなデバイス向けの通信です。 インタラクティブ通信はレスポンシブな特性を持っているため、使用するデバイスや設定に応じて、レイアウトとデザインが自動的に変わります。For detailed information, see [Interactive Communications Overview](/help/forms/using/interactive-communications-overview.md)

* **アダプティブフォーム：**&#x200B;アダプティブフォームは、魅力的でレスポンシブなフォームです。アダプティブフォームを作成し、ユーザーの応答、デバイス、または作業環境に基づいてフォームのセクションを追加または削除することで、ユーザーの入力に動的に対応することができます。 アダプティブフォームについて詳しくは、「[アダプティブフォームの作成について](../../forms/using/introduction-forms-authoring.md)」を参照してください。

* **アダプティブフォームフラグメント：**&#x200B;すべてのフォームは特定の目的のためにデザインされますが、ほとんどのフォームにはいくつかの共通するセグメントがあります。例えば、名前と住所、家族の詳細、収入の詳細などの個人の詳細を入力するためのものなどです。このようなセクションに対して個別のアセットを作成できます。これらの再利用可能なスタンドアロンのセグメントは、アダプティブフォームフラグメントと呼ばれます。 詳しくは、「[アダプティブフォームフラグメント](../../forms/using/adaptive-form-fragments.md)」を参照してください。

* **フォームセット：**&#x200B;フォームセットは HTML5 フォームの集まりであり、エンドユーザーには 1 つのフォームのセットとして提供されます。エンドユーザーがフォームセットへの入力を始めると、フォームはシームレスにその内容を別のフォームにも写します。最終的に、ユーザーは1回のクリックですべてのフォームを単一のエンティティとして送信できます。 詳しくは、「[AEM Forms におけるフォームセット](../../forms/using/formset-in-aem-forms.md)」を参照してください。

* **フォルダー：**[!DNL Forms]AEM ユーザーインターフェイスは、フォルダーを利用してアセットを整理します。サポートされているフォルダーは 2 種類あります。

   * **一般フォルダー：**[!DNL Forms]これらのフォルダーは、AEM ユーザーインターフェイスで作成されたアセットに対して使用されます。これらのフォルダーには、厳密なフォルダー構造はありません。これらのフォルダーでは、フォルダー名の変更とサブフォルダーの作成を行うことができます。また、アダプティブフォーム、インタラクティブ通信、アダプティブフォームフラグメント、フォームテンプレート（XDP）、PDF フォーム、ドキュメント、関連アセットを、これらのフォルダーに保存することができます。
   * **フォームワークフローフォルダー：**[!DNL Forms]フォームワークフローフォルダーは、AEM ユーザーインターフェイスで Workbench プロセス（LiveCycle アーカイブ）が移行および同期されるときに作成されます。このフォルダーの名前を変更することはできません。また、このフォルダー内に、サブフォルダー、インタラクティブ通信、アダプティブフォームフラグメントを作成することはできません。また、バージョンフォルダーを削除したり、アダプティブフォーム、アダプティブフォームフラグメント、またはインタラクティブコミュニケーションをversionフォルダーと並行して作成およびアップロードすることはできません。

   ![フォルダ](assets/folders.png)

   **A.** General folder **B.** Forms Workflowフォルダ

フォームとドキュメントパネルには、以下のオプションも用意されています。

* **ローカルストレージからのファイルの読み込み：** PDF フォームとドキュメント、フォームテンプレート（XFA フォーム）およびその他のリソース（画像や XSD の XML スキーマ）を読み込むことができます。詳しい手順については、「[AEM Forms におけるアセットの読み込みと書き出し](../../forms/using/import-export-forms-templates.md)」を参照してください。
* **AEM Forms アセットの Workbench との同期：**「Workbench のファイル」オプションを使用して、AEM Forms ユーザーインターフェイスと Workbench の間でアセットを同期することができます。It ensures all the assets are available in AEM [!DNL Forms] user interface and Workbench&#39;s crx-repository assets selection.

### テーマ  {#themes}

テーマには、コンポーネントやパネルのスタイル設定の詳細が含まれています。テーマには個別の ID があります。このため、1 つのテーマを複数のアダプティブフォームで再利用できます。コンポーネントに対してスタイルを指定したり、複数のフォームで使用されている様々なコンポーネントの CSS プロパティを変更したりできます。スタイルには、背景色、状態色、透明度、およびサイズなどのプロパティが含まれます。テーマのカスタマイズを保存し、プリセットとしてフォームのコンポーネントにそれらを移植することができます。テーマをフォームに追加すると、指定されたスタイルがフォームの対応コンポーネントに反映されます。With AEM 6.2 [!DNL Forms], you can create themes and apply them to your forms.

テーマの作成と使用について詳しくは、「[AEM Forms のテーマ](../../forms/using/themes.md)」を参照してください。

### レター  {#letters}

An AEM [!DNL Forms] letter is a secure, personalized, and interactive correspondence. You can use AEM [!DNL Forms] to quickly assemble letters (also known as correspondences) from both pre-approved and custom-authored content in a streamlined process.

レターの作成と使用について詳しくは、「[レターの作成](../../forms/using/create-letter.md)」を参照してください。

### ドキュメントフラグメント {#document-fragments}

ドキュメントフラグメントは、レターの作成時に使用する再利用可能な通信のパーツやコンポーネントです。ドキュメントフラグメントのタイプとして、テキスト、リスト、条件およびレイアウトフラグメントがあります。ドキュメントフラグメントの作成と使用について詳しくは、「[ドキュメントフラグメントの作成](/help/forms/using/document-fragments.md)」を参照してください。

### データディクショナリ {#data-dictionaries}

一般のビジネスユーザーにとって、XSD（xml スキーマ）や Java クラスといった、メタデータ表現に関する知識は必要ありません。しかし、通常はソリューションを構築するために、これらのデータ構造や属性の利用が必要となります。AEM [!DNL Forms] uses data dictionary that enables business users to use information from back-end data sources without knowing technical details about their underlying data models.

データディクショナリの作成と使用について詳しくは、[データディクショナリに関する記事](../../forms/using/data-dictionary.md)を参照してください。

## Accessing AEM [!DNL Forms] Configurations {#accessing-aem-forms-configurations}

AEM ツールパネルには、様々なコンポーネント用のツールが含まれています。To navigate to AEM Forms-specific tools, click the Experience Manager logo ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > tools ![hammer](assets/hammer.png) > **[!UICONTROL Forms]**. 以下の機能を実行するためのツールが表示されます。

* **監視フォルダーを設定：**&#x200B;管理者は、監視フォルダーと呼ばれるネットワークフォルダーを設定できます。ユーザーがファイル（PDF ファイルなど）を監視フォルダーに配置すると、設定済みの操作が開始され、ファイルが操作されます。詳しくは、「[監視フォルダーの作成と設定](/help/forms/using/creating-configure-watched-folder.md)」を参照してください。
* **Formsアプリのオフラインサービスの設定：** AEM [!DNL Forms] App Offlineサービスは、フォームで使用されるリソースのパスまたはURLをキャッシュに保存します。 フォームで使用されるリソースのパスや URL をキャッシュに保存することで、サーバー側のパフォーマンスが向上します。To configure the server-side offline component of AEM Forms app, see [Working in the offline mode](/help/forms/using/work-offline-mode.md).

   ![AEM Formsツール](assets/aem_forms_tools_new.png)

* **PDF Generator を設定：**[!DNL Forms]管理者は、AEM PDF Generator の設定、ユーザーアカウントの追加、PDF Generator 設定の読み込みまたは書き出しを行うことができます。
* **Correspondence Management アセットを発行：**[!DNL Forms]AEM では、作成者インスタンスからすべてのレター、ドキュメントフラグメント、データディクショナリおよび関連する依存関係を同時に発行できます。発行済みのアセットには、すべての Correspondence Management アセットと関連する依存性が含まれます。For detailed information, see [Publishing and unpublishing forms &amp; documents](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **Correspondence Management アセットを書き出し：**[!DNL Forms]すべての Correspondence Management アセットおよび関連する依存関係を、AEM インスタンスからパッケージとしてダウンロードできます。手順について詳しくは、「[AEM Forms におけるアセットの読み込みと書き出し](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)」を参照してください。

## 共通のユーザーインターフェイス要素 {#commonelements}

* **左側のレール：** 左側のレールアイコンの ![railleftpngをクリックすると](assets/railleftpng.png) 、AEMのタイムライン機能とリファレンス機能が表示され [!DNL Forms]ます。

   * **タイムライン：**&#x200B;アセットに対するコメントをタイムラインに追加して表示し、レビューとして使用できます。手順について詳しくは、「[フォームのアセットのレビューの作成と管理](../../forms/using/create-reviews-forms.md)」を参照してください。
   * **参照：**[!DNL Forms]1 つの AEM アセットを複数の AEM アセットで使用できます。[!DNL Forms]例えば、1 つのドキュメントフラグメントを複数のレターで使用できます。参照とは、選択したアセットが使用されるアセット（その他のフォームまたはリソース）のリストです。また、選択したアセットが使用している他のアセットのリストも指します。

* **パンくず：**&#x200B;パンくずは、現在のコンソールまたはフォルダーのタイトルを表します。「パンくず」オプションをクリックすると、フォルダー階層の上位のフォルダーに移動することができます。
* **表示切り替え：** 表示切り替えアイコン ![viewlist](assets/viewlist.png) 、またはviewcard ![](assets/viewcard.png) (viewcard)をクリックすると、リストとカードの表示をすばやく切り替えることができます。 一般的なユーザーインターフェイスコンポーネントについて詳しくは、「 [オーサリング](/help/sites-authoring/author.md)」を参照してください。
* **検索：** 検索オプション ![検索](assets/search.png) は、必要なコンテンツやツールをすばやく見つけて移動する機能を提供します。 Type the name of content or product capability and select from the suggestions, for example, type &quot;Documents&quot; to quickly find and navigate to **[!UICONTROL Forms &amp; Documents]** or Document Fragments console. 検索について詳しくは、AEM 6.2 の[検索](/help/sites-authoring/search.md)に関する記事を参照してください。

* **アクションツールバー**：アセットを選択すると、アセット一覧の上にアクションツールバーが表示されます。このツールバーには、選択したアセットに対応するすべての管理ツールが表示されます。ツールアイコンの上にマウスを移動すると、その機能を説明するツールヒントが表示されます。

>[!NOTE]
>
>ユーザーがフォームとドキュメントのコンソールを検索すると、「**フィルターおよびオプション**」のみがレールに表示されます。「フィルターおよびオプション」を使用して、高度な検索を実行できます。

* **アクションツールバー**：アセットを選択すると、アセット一覧の上にアクションツールバーが表示されます。このツールバーには、選択したアセットに対応するすべての管理ツールが表示されます。ツールアイコンの上にマウスを移動すると、その機能を説明するツールヒントが表示されます。

   ![アダプティブフォームのアクションツールバー](assets/action_toolbar_new.png)

   アダプティブフォームのアクションツールバー
