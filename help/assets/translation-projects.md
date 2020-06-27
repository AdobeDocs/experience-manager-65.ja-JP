---
title: 翻訳プロジェクトの作成
description: Learn how to create translation projects in [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: a61e1e9ffb132b59c725b2078f09641a3c2a479a
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 75%

---


# 翻訳プロジェクトの作成 {#creating-translation-projects}

To create a language copy, trigger one of the following language copy workflows available under the References rail in the [!DNL Experience Manager] user interface.

* **作成と翻訳**: このワークフローでは、翻訳対象のアセットが、翻訳先の言語の言語ルートにコピーされます。 また、選択するオプションによって異なりますが、アセットに対応する翻訳プロジェクトがプロジェクトコンソールで作成されます。設定によっては、翻訳プロジェクトを手動で開始することも、翻訳プロジェクトの作成後すぐに自動的に実行することもできます。

* **言語コピーを更新**: このワークフローを実行して、アセットの追加のグループを翻訳し、特定のロケールの言語コピーに含めます。 この場合、翻訳されたアセットが追加されるターゲットフォルダーには翻訳済みのアセットが既に含まれています。

>[!NOTE]
>
>アセットバイナリは、翻訳サービスプロバイダーがバイナリの翻訳をサポートしている場合にのみ翻訳されます。

>[!NOTE]
>
>If you launch a translation workflow for complex assets, such as PDF and [!DNL Adobe InDesign] files, their subassets or renditions (if any) are not submitted for translation.

## 作成と翻訳ワークフロー {#create-and-translate-workflow}

最初は、作成と翻訳ワークフローを使用して、特定の言語の言語コピーを生成します。ワークフローには次のオプションがあります。

* 構造のみを作成。
* 新しい翻訳プロジェクトを作成.
* 既存の翻訳プロジェクトに追加.

### 構造のみを作成 {#create-structure-only}

「**[!UICONTROL 構造のみを作成]**」オプションを使用して、ソース言語ルート内のソースフォルダーの階層と一致するように、ターゲット言語ルート内にターゲットフォルダー階層を作成します。この場合、ソースアセットが宛先フォルダーにコピーされます。ただし、翻訳プロジェクトは生成されません。

1. In the [!DNL Assets] interface, select the source folder for which you want to create a structure in the target language root.
1. Open the **[!UICONTROL References]** pane and click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]**.

   ![chlimage_1-57](assets/chlimage_1-57.png)

1. Click **[!UICONTROL Create &amp; Translate]** at the bottom.

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. 「**[!UICONTROL ターゲット言語]**」リストで、フォルダー構造を作成しようとしている言語を選択します。

   ![chlimage_1-59](assets/chlimage_1-59.png)

1. 「**[!UICONTROL プロジェクト]**」リストで「**[!UICONTROL 構造のみを作成]**」を選択します。

   ![chlimage_1-60](assets/chlimage_1-60.png)

1. 「**[!UICONTROL 作成]**」をクリックします。ターゲット言語の新しい構造が、「**[!UICONTROL 言語コピー]**」の下に表示されます。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Click the structure from the list, and then click **[!UICONTROL Reveal in Assets]** to navigate to the folder structure within the target language.

   ![chlimage_1-62](assets/chlimage_1-62.png)

### 新しい翻訳プロジェクトを作成 {#create-a-new-translation-project}

このオプションを使用すると、翻訳されるアセットは、翻訳先言語の言語ルートにコピーされます。選択するオプションによって異なりますが、アセットに対応する翻訳プロジェクトがプロジェクトコンソールで作成されます。設定によっては、翻訳プロジェクトを手動で開始することも、翻訳プロジェクトの作成後すぐに自動的に実行することもできます。

1. Assets UI で、言語コピーを作成しようとするソースフォルダーを選択します。
1. Open the **[!UICONTROL References]** pane and click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Click **[!UICONTROL Create &amp; Translate]** at the bottom.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 「**[!UICONTROL ターゲット言語]**」リストで、フォルダー構造を作成しようとしている言語を選択します。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 「**[!UICONTROL プロジェクト]**」リストで「**[!UICONTROL 新しい翻訳プロジェクトを作成]**」を選択します。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 「**[!UICONTROL プロジェクトタイトル]**」フィールドに、プロジェクトのタイトルを入力します。

   ![chlimage_1-67](assets/chlimage_1-67.png)

1. 「**[!UICONTROL 作成]**」をクリックします。ソースフォルダーのアセットが、手順 4 で選択したロケールのターゲットフォルダーにコピーされます。

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. そのフォルダーに移動するには、言語コピーを選択してから「**[!UICONTROL アセットで表示]**」をクリックします。

   ![chlimage_1-69](assets/chlimage_1-69.png)

1. プロジェクトコンソールに移動します。翻訳フォルダーはプロジェクトコンソールにコピーされます。

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. フォルダーを開くと翻訳プロジェクトが表示されます。

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. プロジェクトをクリックして詳細ページを開きます。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 翻訳ジョブのステータスを表示するには、「**[!UICONTROL 翻訳ジョブ]**」タイルの一番下にある省略記号をクリックします。

   ![chlimage_1-73](assets/chlimage_1-73.png)

   ジョブステータスの詳細については、[翻訳ジョブのステータスの監視](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)を参照してください。

1. Assets UI に移動し、翻訳済みアセットそれぞれのプロパティページを開き、翻訳されたメタデータを表示します。

   ![アセットのプロパティページで変換済みメタデータを表示する](assets/translated-metadata-asset-properties.png)

   *図： アセットのプロパティページの変換済みメタデータ。*


   >[!NOTE]
   >
   >この機能は、アセットに対してもフォルダーに対しても使用できます。フォルダーではなくアセットを選択すると、そのアセットの言語コピーを作成するために、言語ルートまでのフォルダーの階層全体がコピーされます。

### 既存の翻訳プロジェクトに追加 {#add-to-existing-translation-project}

このオプションを使用すると、前の翻訳ワークフローの実行後にユーザーがソースフォルダーに追加したアセットに対して、翻訳ワークフローが実行されます。新しく追加されたアセットのみが、既に翻訳済みのアセットを含むターゲットフォルダーにコピーされます。この場合、新しい翻訳プロジェクトは作成されません。

1. Assets UI で、翻訳されていないアセットを含むソースフォルダーに移動します。
1. 翻訳するアセットを選択して、**[!UICONTROL 参照パネル]**&#x200B;を開きます。「**[!UICONTROL 言語コピー]**」セクションに、現在使用可能な翻訳コピーの数が表示されます。
1. Click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]**. 使用可能な翻訳コピーのリストが表示されます。
1. Click **[!UICONTROL Create &amp; Translate]** at the bottom.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. 「**[!UICONTROL ターゲット言語]**」リストで、フォルダー構造を作成しようとしている言語を選択します。

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 「**[!UICONTROL プロジェクト]**」リストで「**[!UICONTROL 既存の翻訳プロジェクトに追加]**」を選択して、翻訳ワークフローをフォルダーに対して実行します。

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >「**[!UICONTROL 既存の翻訳プロジェクトに追加]**」オプションを選択すると、プロジェクトの設定が既存のプロジェクトの設定と完全に一致する場合にのみ、翻訳プロジェクトが既存のプロジェクトに追加されます。それ以外の場合は、新しいプロジェクトが作成されます。

1. 「**[!UICONTROL 既存の翻訳プロジェクト]**」リストで、翻訳のためのアセットを追加するプロジェクトを選択します。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 「**[!UICONTROL 作成]**」をクリックします。翻訳されるアセットがターゲットフォルダーに追加されます。更新されたフォルダーが、「**[!UICONTROL 言語コピー]**」セクションに表示されます。

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. プロジェクトコンソールに移動し、追加先の既存の翻訳プロジェクトを開きます。
1. 翻訳プロジェクトをクリックして、プロジェクトの詳細ページを表示します。

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Click the ellipsis at the bottom of the **Translation Job** tile to view the assets in the translation workflow. 翻訳ジョブリストには、アセットのメタデータとタグのエントリも表示されます。これらのエントリは、アセットのメタデータとタグも翻訳されることを意味します。

   >[!NOTE]
   >
   >タグまたはメタデータのエントリを削除した場合は、どのアセットのタグまたはメタデータも翻訳されません。

   >[!NOTE]
   >
   >機械翻訳を使用する場合は、アセットのバイナリは翻訳されません。

   >[!NOTE]
   >
   >翻訳ジョブに追加したアセットがサブアセットを含んでいる場合は、問題を避けるために、サブアセットを選択して翻訳から除外してください。

1. アセットの翻訳を開始するには、「**[!UICONTROL 翻訳ジョブ]**」タイルの矢印をクリックし、リストから「**[!UICONTROL 開始]**」を選択します。

   ![chlimage_1-81](assets/chlimage_1-81.png)

   翻訳ジョブの開始を通知するメッセージが表示されます。

   ![chlimage_1-82](assets/chlimage_1-82.png)

1. 翻訳ジョブのステータスを表示するには、「**[!UICONTROL 翻訳ジョブ]**」タイルの一番下にある省略記号をクリックします。

   ![chlimage_1-83](assets/chlimage_1-83.png)

   For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. 翻訳が完了すると、ステータスが「レビューへの準備完了」に変更されます。Assets UI に移動し、翻訳済みアセットそれぞれのプロパティページを開き、翻訳されたメタデータを表示します。

## 言語コピーを更新 {#update-language-copies}

このワークフローを実行すると、追加のアセットのセットが翻訳され、特定のロケールの言語コピーに含められます。この場合、翻訳されたアセットが追加されるターゲットフォルダーには翻訳済みのアセットが既に含まれています。オプションの選択に応じて、翻訳プロジェクトが作成されるか、既存の翻訳プロジェクトが新しいアセットを含むように更新されます。「言語コピーを更新」ワークフローには次のオプションがあります。

* 新しい翻訳プロジェクトを作成
* 既存の翻訳プロジェクトに追加

### 新しい翻訳プロジェクトを作成 {#create-a-new-translation-project-1}

このオプションを使用する場合、言語コピーを更新するアセットのセットに対して翻訳プロジェクトが作成されます。

1. Assets UI で、アセットを追加したソースフォルダーを選択します。
1. **[!UICONTROL 参照]** ペインを開き、「コピー」の **[!UICONTROL 下にある「]** 言語コピー **** 」をクリックして言語コピーのリストを表示します。
1. 「**[!UICONTROL 言語コピー]**」の前のチェックボックスを選択し、適切なロケールに対応するターゲットフォルダーを選択します。

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Click **[!UICONTROL Update language copies]** at the bottom.

   ![chlimage_1-85](assets/chlimage_1-85.png)

1. 「**[!UICONTROL プロジェクト]**」リストで「**[!UICONTROL 新しい翻訳プロジェクトを作成]**」を選択します。

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. 「**[!UICONTROL プロジェクトタイトル]**」フィールドに、プロジェクトのタイトルを入力します。

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. 「**[!UICONTROL 開始]**」をクリックします。
1. プロジェクトコンソールに移動します。翻訳フォルダーはプロジェクトコンソールにコピーされます。

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. フォルダーを開くと翻訳プロジェクトが表示されます。

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. プロジェクトをクリックして詳細ページを開きます。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. アセットの翻訳を開始するには、「**[!UICONTROL 翻訳ジョブ]**」タイルの矢印をクリックし、リストから「**[!UICONTROL 開始]**」を選択します。

   ![chlimage_1-91](assets/chlimage_1-91.png)

   翻訳ジョブの開始を通知するメッセージが表示されます。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 翻訳ジョブのステータスを表示するには、「**[!UICONTROL 翻訳ジョブ]**」タイルの一番下にある省略記号をクリックします。

   ![chlimage_1-93](assets/chlimage_1-93.png)

   ジョブステータスの詳細については、[翻訳ジョブのステータスの監視](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)を参照してください。

1. Assets UI に移動し、翻訳済みアセットそれぞれのプロパティページを開き、翻訳されたメタデータを表示します。

### 既存の翻訳プロジェクトに追加 {#add-to-existing-translation-project-1}

このオプションを使用すると、アセットのセットが既存の翻訳プロジェクトに追加され、選択したロケールの言語コピーが更新されます。

1. Assets UI で、アセットフォルダーを追加したソースフォルダーを選択します。
1. **[!UICONTROL 参照パネルを開き、「コピー」の]**&#x200B;下にある「 **[!UICONTROL 言語コピー]****** 」をクリックして言語コピーのリストを表示します。

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 「**[!UICONTROL 言語コピー]**」の前のチェックボックスをオンにします。これによりすべての言語コピーが選択されます。翻訳先のロケールに対応する言語コピーを除き、他のコピーの選択を解除します。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Click **[!UICONTROL Update language copies]** at the bottom.

   ![chlimage_1-96](assets/chlimage_1-96.png)

1. 「**[!UICONTROL プロジェクト]**」リストで「**[!UICONTROL 既存の翻訳プロジェクトに追加]**」を選択します。

   ![chlimage_1-97](assets/chlimage_1-97.png)

1. 「**[!UICONTROL 既存の翻訳プロジェクト]**」リストで、翻訳のためのアセットを追加するプロジェクトを選択します。

   ![chlimage_1-98](assets/chlimage_1-98.png)

1. 「**[!UICONTROL 開始]**」をクリックします。
1. [既存の翻訳プロジェクトに追加](translation-projects.md#add-to-existing-translation-project)の手順 9～14 を参照して、この手順の続きを完了させます。

## 一時的な言語コピーの作成 {#creating-temporary-language-copies}

翻訳ワークフローを実行して、元のアセットを編集したバージョンで言語コピーを更新するとき、翻訳済みアセットをユーザーが承認するまで、既存の言語コピーが維持されます。[!DNL Adobe Experience Manager Assets] は、新たに翻訳されたアセットを一時的な場所に格納しておき、ユーザーがアセットを明示的に承認した後で既存の言語コピーを更新します。ユーザーがアセットを承認しないと、言語コピーは変更されません。

1. Click the source root folder under **[!UICONTROL Language Copies]** for which you already created a language copy, and then click **[!UICONTROL Reveal in Assets]** to open the folder in [!DNL Experience Manager Assets].

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. From the [!DNL Assets] interface, select an asset you already translated and click **[!UICONTROL Edit]** from the toolbar to open the asset in edit mode.
1. アセットを編集して、変更内容を保存します。
1. [既存の翻訳プロジェクトに追加](#add-to-existing-translation-project)の手順 2～14 を実行して、言語コピーを更新します。
1. Click the ellipsis at the bottom of the **[!UICONTROL Translation Job]** tile. **[!UICONTROL 翻訳ジョブ]**&#x200B;ページのアセットのリストで、翻訳済みバージョンのアセットが格納されている一時的な場所を確認できます。

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. 「**[!UICONTROL タイトル]**」の横にあるチェックボックスをオンにします。
1. From the toolbar, click **[!UICONTROL Accept Translation]** and then click **[!UICONTROL Accept]** in the dialog to overwrite the translated asset in the target folder with the translated version of the edited asset.

   ![chlimage_1-102](assets/chlimage_1-102.png)

   >[!NOTE]
   >
   >翻訳ワークフローが対象のアセットを更新できるようにするには、アセットとメタデータの両方を承認します。

   Click **[!UICONTROL Reject Translation]** to retain the originally translated version of the asset in the target locale root and reject the edited version.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. 翻訳済みメタデータを表示するには、コン [!DNL Assets] ソールに移動し、翻訳済みの各アセットの [!UICONTROL プロパティ] ページを開きます。

>[!MORELIKETHIS]
>
>* [メタデータを効率的に変換するためのヒント](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/)。

