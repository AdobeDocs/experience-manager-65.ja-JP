---
title: コンテンツフラグメントの翻訳プロジェクトの作成
description: コンテンツフラグメントを翻訳する方法を説明します。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
feature: Content Fragments
role: User, Admin
exl-id: 19bb58da-8220-404e-bddb-34be94a3a7d7
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 45%

---

# コンテンツフラグメントの翻訳プロジェクトの作成 {#creating-translation-projects-for-content-fragments}

Adobe Experience Manager（AEM）Assets は、アセットだけでなく、[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)（バリエーションも含む）の言語コピーワークフローをサポートします。コンテンツフラグメントで言語コピーワークフローを実行する場合、追加の最適化は必要ありません。 各ワークフローでは、コンテンツフラグメント全体が翻訳用に送信されます。

コンテンツフラグメントで実行できるワークフローのタイプは、アセットに対して実行するワークフローのタイプとまったく同じです。 また、各ワークフロータイプ内で使用できるオプションは、アセットの対応するワークフロータイプで使用できるオプションと一致します。

コンテンツフラグメントに対して、次のタイプの言語コピーワークフローを実行できます。

**作成と翻訳**

このワークフローでは、翻訳対象のコンテンツフラグメントが、翻訳先の言語の言語ルートにコピーされます。 また、選択したオプションに応じて、プロジェクトコンソールのコンテンツフラグメント用に翻訳プロジェクトが作成されます。 設定に応じて、翻訳プロジェクトを手動で開始することも、翻訳プロジェクトの作成後すぐに自動的に実行することもできます。

**言語コピーを更新**

ソースコンテンツフラグメントが更新または変更された場合、対応するロケール/言語固有のコンテンツフラグメントを再翻訳する必要があります。 更新言語コピーワークフローは、追加のコンテンツフラグメントのグループを変換し、特定のロケールの言語コピーに含めます。 この場合、翻訳されたコンテンツフラグメントは、以前に翻訳されたコンテンツフラグメントを含むターゲットフォルダーに追加されます。

## 作成と翻訳ワークフロー {#create-and-translate-workflow}

作成と翻訳ワークフローには、次のオプションが含まれます。 各オプションに関連する手順は、アセットの対応するオプションに関連する手順と似ています。

* 構造のみを作成：手順は、[構造のみを作成（アセット）](translation-projects.md#create-structure-only)を参照してください。
* 新しい翻訳プロジェクトを作成：手順は、[新しい翻訳プロジェクトを作成（アセット）](translation-projects.md#create-a-new-translation-project)を参照してください。
* 既存の翻訳プロジェクトに追加：手順は、[既存の翻訳プロジェクトに追加（アセット）](translation-projects.md#add-to-existing-translation-project)を参照してください。

## 言語コピーを更新ワークフロー {#update-language-copies-workflow}

言語コピーを更新ワークフローには、次のオプションが含まれます。 各オプションに関連する手順は、アセットの対応するオプションに関連する手順と似ています。

* 新しい翻訳プロジェクトを作成：手順は、[新しい翻訳プロジェクトを作成（アセット）](translation-projects.md#create-a-new-translation-project)（更新ワークフロー）を参照してください。
* 既存の翻訳プロジェクトに追加：手順は、[既存の翻訳プロジェクトに追加（アセット）](translation-projects.md#add-to-existing-translation-project)（更新ワークフロー）を参照してください。

また、アセットの一時コピーを作成する場合と同様に、フラグメントの一時言語コピーを作成することもできます。 詳しくは、 [アセットの一時的な言語コピーの作成](translation-projects.md#creating-temporary-language-copies).

## 混在メディアフラグメントの翻訳 {#translating-mixed-media-fragments}

AEMを使用すると、様々なタイプのメディアアセットやコレクションを含むコンテンツフラグメントを翻訳できます。 インラインアセットを含むコンテンツフラグメントを翻訳する場合、翻訳されたアセットのコピーがターゲット言語ルートの下に保存されます。

コンテンツフラグメントにコレクションが含まれる場合、コレクション内のアセットがコンテンツフラグメントと共に翻訳されます。 翻訳されたアセットのコピーは、ソース言語ルートの下のソースアセットの物理的な場所と一致する適切なターゲット言語ルート内の場所に保存されます。

混在メディアを含むコンテンツフラグメントを翻訳するには、まずデフォルトの翻訳フレームワークを編集して、コンテンツフラグメントに関連付けられたインラインアセットおよびコレクションの翻訳を有効にします。

1. AEM のロゴをクリックまたはタップし、**[!UICONTROL ツール／デプロイメント／クラウドサービス]**&#x200B;に移動します。
1. **[!UICONTROL Adobe Marketing Cloud]** の下にある「**[!UICONTROL 翻訳統合]**」を見つけ、「**[!UICONTROL 設定を表示]**」をクリックまたはタップします。

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. 利用可能な設定のリストで、「**[!UICONTROL デフォルト設定（翻訳統合の設定）]**」をクリックまたはタップして、**[!UICONTROL デフォルト設定]**&#x200B;ページを開きます。

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. ツールバーの「**[!UICONTROL 編集]**」をクリックして、「**[!UICONTROL 翻訳設定]**」ダイアログを表示します。

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. 次に移動： **[!UICONTROL Assets]** 「 」タブで「 」を選択します。 **[!UICONTROL インラインメディアアセットと関連するコレクション]** から **[!UICONTROL コンテンツフラグメントアセットを翻訳]** リスト。 クリックまたはタップ **[!UICONTROL OK]** をクリックして変更を保存します。

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. 英語ルートフォルダーから、コンテンツフラグメントを開きます。

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. 「**[!UICONTROL アセットを挿入]**」アイコンをクリックまたはタップします。

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. コンテンツフラグメントにアセットを挿入します。

   ![コンテンツフラグメントへのアセットの挿入](assets/column-view.png)

1. 「**[!UICONTROL コンテンツを関連付け]**」アイコンをクリックまたはタップします。

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. 「**[!UICONTROL コンテンツを関連付け]**」をクリックまたはタップします。

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. コレクションを選択し、コンテンツフラグメントに含めます。 クリックまたはタップ **[!UICONTROL 保存]**.

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. コンテンツフラグメントを選択し、 **[!UICONTROL GlobalNav]** アイコン。
1. 選択 **[!UICONTROL 参照]** メニューから、 **[!UICONTROL 参照]** ウィンドウ

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. 「**[!UICONTROL コピー]**」の下の「**[!UICONTROL 言語コピー]**」をクリックまたはタップして言語コピーを表示します。

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. パネルの下部にある「**[!UICONTROL 作成と翻訳]**」をクリックまたはタップして&#x200B;**[!UICONTROL 作成と翻訳]**&#x200B;ダイアログを表示します。

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. 「**[!UICONTROL ターゲット言語]**」リストからターゲット言語を選択します。

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. 「**[!UICONTROL プロジェクト]**」リストから翻訳プロジェクトのタイプを選択します。

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. 「**[!UICONTROL プロジェクトタイトル]**」ボックスにプロジェクトのタイトルを指定し、「**作成**」をクリックまたはタップします。

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. **[!UICONTROL プロジェクト]**&#x200B;コンソールに移動し、作成した翻訳プロジェクトのプロジェクトフォルダーを開きます。

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. プロジェクトのタイトルをクリックまたはタップして、プロジェクトの詳細ページを開きます。

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. 「翻訳ジョブ」タイルで、翻訳するアセットの数を確認します。
1. 次から： **[!UICONTROL 翻訳ジョブ]** タイルで、翻訳ジョブを開始します。

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. 「翻訳ジョブ」タイルの下部にある省略記号をクリックして、翻訳ジョブの状態を表示します。

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. コンテンツフラグメントをクリックまたはタップして、翻訳後の関連アセットのパスを確認します。

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. コレクションコンソールで、コレクションの言語コピーをレビューします。

   ![chlimage_1-465](assets/chlimage_1-465.png)

   コレクションのコンテンツのみが翻訳されます。 コレクション自体は翻訳されません。

1. 翻訳済みの関連アセットのパスに移動します。 翻訳後のアセットがターゲット言語ルートの下に保存されていることを確認します。

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. コレクション内のアセットに移動します。このアセットは、コンテンツフラグメントと共に翻訳されます。 翻訳されたアセットのコピーが適切なターゲット言語ルートに保存されていることを確認します。

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >コンテンツフラグメントを既存のプロジェクトに追加する手順や更新ワークフローを実行する手順は、アセットの対応する手順と似ています。 これらの手順については、アセットに関する説明を参照してください。
