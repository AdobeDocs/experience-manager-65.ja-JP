---
title: アセットフォルダーのヘッドレス作成のクイック開始ガイド
description: AEM コンテンツフラグメントモデルを使用すると、ヘッドレスコンテンツの基盤となるコンテンツフラグメントの構造を定義できます。
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
source-git-commit: 40922b222e15aa3ef12b54d65addff32b679d36e
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 100%

---

# アセットフォルダーのヘッドレスクイックスタートガイドの作成 {#creating-an-assets-folder}

AEM コンテンツフラグメントモデルを使用すると、ヘッドレスコンテンツの基盤となるコンテンツフラグメントの構造を定義できます。コンテンツフラグメントはアセットフォルダーに保存されます。

## アセットフォルダーとは  {#what-is-an-assets-folder}

今後のコンテンツフラグメントに必要な構造を定義する[コンテンツフラグメントモデルを作成](create-content-model.md)できたので、フラグメントを作成するのが楽しみかと思います。

ただし、まず、アセットを保存するアセットフォルダーを作成する必要があります。

アセットフォルダーは、画像やビデオなど、従来のコンテンツアセットや[コンテンツフラグメントを整理](/help/assets/manage-assets.md)するために使用されます。

## アセットフォルダーの作成方法 {#how-to-create-an-assets-folder}

管理者は、コンテンツの作成時にフォルダーを作成してコンテンツを整理するだけで済みます。この「はじめる前に」ガイドの目的上、フォルダーを 1 つだけ作成します。

1. AEM にログインし、メインメニューで&#x200B;**ナビゲーション／アセット／ファイル**&#x200B;を選択します。
1. **作成／フォルダー**&#x200B;をタップまたはクリックします。
1. フォルダーの&#x200B;**タイトル**&#x200B;と&#x200B;**名前**&#x200B;を指定します。
   * **タイトル**&#x200B;は内容がわかるように付けます。
   * **名前**&#x200B;はリポジトリのノード名になります。
      * タイトルに基づいて自動的に生成され、[AEM の命名規則](/help/sites-developing/naming-conventions.md)に従って調整されます。
      * 必要に応じて調整できます。

   ![フォルダーを作成](../assets/assets-folder-create.png)
1. 先ほど作成したフォルダーを選択し、ツールバーから「**プロパティ**」を選択します（または、`p` [キーボードショートカットを使用します](/help/sites-authoring/keyboard-shortcuts.md)）。
1. **プロパティ**&#x200B;ウィンドウで、「**Cloud Services**」タブを選択します。
1. **クラウド設定**&#x200B;で、[以前に作成した設定](create-configuration.md)を選択します。

   ![アセットフォルダーの設定](../assets/assets-folder-configure.png)
1. 「**保存して閉じる**」をタップまたはクリックします。
1. 確認ウィンドウで「**OK**」をタップまたはクリックします。

   ![確認ウィンドウ](../assets/assets-folder-confirmation.png)

先ほど作成したフォルダー内に、追加のサブフォルダーを作成できます。サブフォルダーは、親フォルダーの&#x200B;**クラウド設定**&#x200B;を継承します。別の設定モデルを使用する場合は、この設定を上書きできます。

ローカライズされたサイト構造を使用している場合は、新しいフォルダーの下に[言語ルート](/help/assets/multilingual-assets.md)を作成できます。

## 次の手順 {#next-steps}

コンテンツフラグメント用のフォルダーを作成したら、「はじめる前に」ガイドの第 4 部に進み、[コンテンツフラグメントを作成します。](create-content-fragment.md)

>[!TIP]
>
>コンテンツフラグメントの管理について詳しくは、[コンテンツフラグメントのドキュメント](/help/assets/content-fragments/content-fragments.md)を参照してください。
