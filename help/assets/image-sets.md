---
title: 画像セット
description: Dynamic Media の画像セットの操作方法について説明します。
uuid: ca2fd5b0-656e-4960-b10c-f0ec3d418760
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ccc4eb23-934c-4e67-860b-a6faa2bcaafc
docset: aem65
translation-type: tm+mt
source-git-commit: c3ae4447581d946554d792c68d31b47a6b67d5df
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 87%

---


# 画像セット {#image-sets}

画像セットは、ユーザーに対して統一された閲覧エクスペリエンスを提供します。ユーザーはこのエクスペリエンスで、サムネール画像をクリックしてアイテムの様々なビューを表示できます。画像セットによって、アイテムの代替的なビューを表示でき、ビューアでは画像をより近くで確認するためのズームツールを利用できます。

画像セットのバナーには、「`IMAGESET`」と表示されます。また、画像セットが公開されている場合、公開日が&#x200B;**[!UICONTROL 地球]**&#x200B;アイコン付きでバナーに表示され、最終変更日も&#x200B;**[!UICONTROL 鉛筆]**&#x200B;アイコン付きで表示されます。

![chlimage_1-133](assets/chlimage_1-339.png)

画像セット内では、画像セットを作成してサムネールを追加することで、スウォッチを作成することもできます。

この使い方は、アイテムを異なる色、パターンまたは仕上がりで表示する場合に特に便利です。カラースウォッチを含む画像セットを作成するには、ユーザーに表示する色、パターンまたは仕上がりごとに画像を 1 つずつ用意する必要があります。また、色、パターンまたは仕上がりごとに 1 つのカラースウォッチ、パターンスウォッチまたは仕上がりスウォッチを用意する必要もあります。

例として、つばの色が異なる帽子の画像を表示します。つばの色は、赤、緑、青です。この場合、同じ帽子について 3 つの写真が必要になります。赤のつばの写真、緑のつばの写真、青のつばの写真が必要です。また、赤のカラースウォッチ、緑のカラースウォッチ、青のカラースウォッチも必要になります。カラースウォッチは、ユーザーがスウォッチセットビューアでクリックして、赤のつばの帽子、緑のつばの帽子または青のつばの帽子を表示するためのサムネールとして機能します。

>[!NOTE]
>
>アセットユーザーインターフェイスについて詳しくは、アセットの [管理を参照してください](/help/assets/manage-assets.md)。

## クイックスタート：画像セット {#quick-start-image-sets}

すぐに使い始めるには：

1. [複数ビュー用のプライマリソース画像をアップロードします。](#uploading-assets-in-image-sets)

   まずは画像セット用の画像をアップロードします。ユーザーは画像セットビューアで画像をズームできるので、画像を選択する際にはズームを考慮します。最適なズーム詳細には、最大サイズで 2,000 ピクセル以上の画像を使用してください。Dynamic Media では、各画像を最大 25 メガピクセルまでレンダリングできます。例えば、5,000 x 5,000 メガピクセルの画像や、その他のサイズの組み合わせを 25 メガピクセルまで使用できます。

   AEM Assets では多くの画像ファイル形式がサポートされますが、可逆圧縮 TIFF、PNG および EPS 画像の使用が推奨されます。

1. [画像セットを作成します。](#creating-image-sets)

   画像セットで、画像セットビューア内のサムネール画像をクリックします。

   Assets で画像セットを作成するには、**[!UICONTROL 作成／画像セットをタップまたはクリックします。]** 次に、画像を追加し、「 **[!UICONTROL 保存」をクリックします。]**

   [バッチセットプリセット](/help/assets/config-dms7.md)を使用して画像セットを自動的に作成することもできます。
   >[!IMPORTANT]
   >
   >バッチセットは、アセット取り込みの一環としてIPS(Image Production System)によって作成され、ダイナミックメディア —Scene7モードでのみ使用できます。

   詳しくは、[アップロード用の画像セットアセットの準備およびファイルのアップロード](#uploading-assets-in-image-sets)を参照してください。

   [セレクターの操作](/help/assets/working-with-selectors.md)を参照してください。

1. 必要に応じて[画像セットビューアプリセット](/help/assets/managing-viewer-presets.md)を追加します。

   管理者は、画像セットビューアプリセットを作成または編集できます。To see your image set with a viewer preset, select the image set, and in the left-rail drop-down menu, select **[!UICONTROL Viewers.]**

   **[!UICONTROL ツール／Assets／ビューアプリセット]**&#x200B;を選択して、ビューアプリセットを作成または編集します。

1. （オプション）バッチセットプリセットを使用して作成した[画像セットの表示](/help/assets/image-sets.md#viewing-image-sets)
1. [画像セットをプレビューします。](/help/assets/previewing-assets.md)

   画像セットを選択すると、プレビューできます。サムネールアイコンをクリックして、選択したビューアでの画像セットの表示を確認します。**[!UICONTROL ビューア]**&#x200B;メニューから様々なビューアを選択できます。このメニューは左側のレールのドロップダウンメニューにあります。

1. [画像セットを公開します。](/help/assets/publishing-dynamicmedia-assets.md)

   画像セットを公開すると、URLと埋め込みコードがアクティブになります。 さらに、作成した[カスタムビューアプリセットを公開する](/help/assets/managing-viewer-presets.md)必要があります。既製のビューアプリセットが既に公開されています。

1. [URL を Web アプリケーションにリンクする](/help/assets/linking-urls-to-yourwebapplication.md)か、[ビデオビューアまたは画像ビューアを埋め込みます](/help/assets/embed-code.md)。

   画像セットの URL コールが作成され、画像セットの公開後にそれらの URL コールがアクティベートされます。アセットをプレビューする際に、これらの URL をコピーできます。または、URL を Web サイトに埋め込むこともできます。

   Select the Image Set, then in the left rail drop-down menu, select **[!UICONTROL Viewers.]**

   詳しくは、[Web ページへの画像セットのリンク](/help/assets/linking-urls-to-yourwebapplication.md)および[ビデオビューアまたは画像ビューアの埋め込み](/help/assets/embed-code.md)を参照してください。

画像セットを編集するには、[画像セットの編集](#editing-image-sets)を参照してください。また、[画像セットのプロパティ](/help/assets/manage-assets.md#editing-properties)を表示および編集することができます。

セットの作成で問題が発生した場合は、[Dynamic Media - Scene7 モードのトラブルシューティング](/help/assets/troubleshoot-dms7.md#images-and-sets)の「画像とセット」を参照してください。

## 画像セット内のアセットのアップロード {#uploading-assets-in-image-sets}

まずは画像セット用の画像をアップロードします。ユーザーは画像セットビューアで画像をズームできるので、画像を選択する際にはズームを考慮します。最大サイズで 2,000 ピクセル以上の画像を使用してください。画像セットでは多くの画像ファイル形式がサポートされますが、可逆圧縮 TIFF、PNG および EPS 画像の使用が推奨されます。

画像セット用の画像のアップロードは、[AEM Assets での他のアセットのアップロード](/help/assets/manage-assets.md#uploading-assets)と同様に実行できます。

### アップロード用の画像セットアセットの準備 {#preparing-image-set-assets-for-upload}

画像セットを作成する前に、画像が適切なサイズと形式であることを確認します。

複数ビューの画像セットを作成するには、異なる視点からアイテムを表示するための画像、または同じアイテムの異なる面を表示するための画像が必要になります。目標は、閲覧者がアイテムの見た目や機能について全体的に把握できるように、アイテムの重要な特徴を際立たせることです。

ユーザーは画像セット内で画像をズームできるので、最大サイズで 2,000 ピクセル以上の画像を使用してください。AEM Assets では多くの画像ファイル形式がサポートされますが、可逆圧縮 TIFF、PNG および EPS 画像の使用が推奨されます。

>[!NOTE]
>
>さらに、製品スウォッチを示すサムネールを使用する場合は、次のことをおこなう必要があります。
>
>同じ画像を異なる色、パターンまたは仕上がりで表示するためのビネットまたは異なる写真が必要になります。また、それぞれの色、パターンまたは仕上がりに対応するサムネールファイルも必要です。例えば、同じジャケットをブラック、ブラウン、グリーンで表示する画像セットのサムネールを表示するには、次の項目が必要です。
>
>* 同じジャケットのブラック、ブラウンおよびグリーンの写真。
>* ブラック、ブラウンおよびグリーンの色のサムネール。


## 画像セットの作成 {#creating-image-sets}

画像セットは、ユーザーインターフェイスまたは API 経由で作成できます。ここでは、UI で画像セットを作成する方法について説明します。

>[!NOTE]
>
>[バッチセットプリセット](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用して画像セットを自動的に作成することもできます。
>**重要：**&#x200B;バッチセットは IPS（Image Production System）によってアセット取り込みの一環として作成され、Dynamic Media - Scene7 モードでのみ使用できます。

画像セットに追加したアセットは、自動的に英数字順で追加されます。追加後に、手動でアセットの順番を変更したり、並べ替えたりすることができます。

>[!NOTE]
>
>ファイル名に「,」（コンマ）が含まれているアセットについては、画像セットはサポートされません。

**画像セットを作成するには**

1. AEM で、AEM のロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ナビゲーション／アセットをタップします。]**&#x200B;画像セットを作成する場所に移動し、**[!UICONTROL 作成／画像セット]**&#x200B;をタップして、画像セットエディターページを開きます。

   アセットを格納しているフォルダー内からセットを作成することもできます。

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. 画像セットエディターページの「**[!UICONTROL タイトル]**」フィールドに画像セットの名前を入力します。この名前は、画像セット全般のバナーに表示されます。オプションで、説明を入力します。

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. 次のいずれかの操作をおこないます。

   * Near the upper-left corner of the Image Set Editor page, tap **[!UICONTROL Add Asset.]**

   * Near the middle of the Image Set Editor page, tap **[!UICONTROL Tap to open Asset Selector.]**
   画像セットに含めるアセットをタップして選択しします。選択済みのアセットにはチェックマークアイコンが付いています。When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Select.]**

   アセットセレクターでは、キーワードを入力して **[!UICONTROL Enter キーをタップまたはクリックすることで、アセットを検索することができます。]**&#x200B;フィルターを適用して、検索結果を絞り込むこともできます。パス、コレクション、ファイルタイプおよびタグでフィルタリングできます。フィルターを選択してから、ツールバーの&#x200B;**[!UICONTROL フィルター]**&#x200B;アイコンをタップします。Change the view by tapping the View icon and selecting **[!UICONTROL Column View]**, **[!UICONTROL Card View]**, or **[!UICONTROL List View.]**

   [セレクターの操作](/help/assets/working-with-selectors.md)を参照してください。

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. 画像セットに追加したアセットは、自動的に英数字順で追加されます。追加後に、手動でアセットの順番を変更したり、並べ替えたりすることができます。

   必要に応じて、アセットの並べ替えアイコンをアセットのファイル名の右にドラッグして、画像をセットリスト内で上下に並べ替えます。

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   サムネールまたはスウォッチを変更する場合は、画像の横の「**+**」**サムネール**&#x200B;アイコンをクリックし、必要なサムネールまたはスウォッチに移動します。When done selecting all the images click **[!UICONTROL Save.]**

1. （オプション）次のいずれかの操作をおこないます。

   * To delete an image, select the image and tap **[!UICONTROL Delete Asset.]**

   * ページの右上隅付近にプリセットを適用するには、「]**プリセット**[!UICONTROL 」をタップした後、すべてのアセットに一度に適用するプリセットを選択します。
   >[!NOTE]
   >
   >画像セットを作成するときに、画像セットのサムネールを変更したり、画像セット内のアセットに基づいて AEM がサムネールを自動的に選択するように設定したりできます。サムネールを選択するには、画像セットエディターページの「タイトル」フィールドの上にある「]**サムネールを変更**[!UICONTROL 」をタップし、任意の画像を選択します（他のフォルダーに移動して画像を検索することもできます）。If you have selected a thumbnail and then decide that you want AEM to generate one from the image set, select **[!UICONTROL Switch to]** **[!UICONTROL Automatic thumbnail.]**

1. 「**[!UICONTROL 保存」をクリックします。]**&#x200B;新しく作成した画像セットが、作成先のフォルダーに表示されます。

## 画像セットの表示 {#viewing-image-sets}

画像セットは、ユーザーインターフェイスで作成することも、[バッチセットプリセット](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用して自動的に作成することもできます。

>[!IMPORTANT]
>
>Batch sets are created by the IPS [Image Production System] as part of asset ingestion and are available only in Dynamic Media - Scene7 mode.)

ただし、バッチセットプリセットを使用して作成したセットは、ユーザーインターフェイスに表示&#x200B;*されません*。これらのセットは 3 つの異なる方法で表示できます（これらの方法は、画像セットをユーザーインターフェイスで作成した場合も使用できます）。

* 個々のアセットのプロパティを開きます。選択したアセットが参照されている、またはメンバーとして含まれているセットがプロパティで示されます。セットの名前をクリックして、セット全体を表示します。

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties2.png)

* 任意のセットのメンバー画像で、**[!UICONTROL セット]**&#x200B;メニューを選択して、アセットがメンバーとして含まれているセットを表示します。

   ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* From search, you can select **[!UICONTROL Filter]**, then expand **[!UICONTROL Dynamic Media]** and select **[!UICONTROL Sets.]**

   検索結果として、UI で手動で作成した一致するセットか、バッチセットプリセットを使用して自動的に作成した一致するセットが返されます。自動セットの場合、検索クエリは、AEM での検索とは異なる「次の値で始まる」検索条件を使用して実行されます。AEM での検索は、「次を含む」検索条件に基づいて実行されます。フィルターを「**[!UICONTROL セット]**」に設定するのが、自動セットを検索する唯一の方法です。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>[画像セットの編集](#editing-image-sets)の説明に従って、ユーザーインターフェイスを通じて画像セットを表示できます。

## 画像セットの編集 {#editing-image-sets}

画像セットには、次のような様々な編集タスクを実行できます。

* 画像セットへの画像の追加
* 画像セット内の画像の並べ替え
* 画像セットのアセットの削除
* ビューアプリセットの適用
* 画像セットの削除

**画像セットを編集するには**

1. 次のいずれかの操作をおこないます。

   * 画像セットアセット上にマウスポインターを置き、]**編集**[!UICONTROL （鉛筆アイコン）をタップします。
   * 画像セットアセット上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップした後、ツールバーの「**[!UICONTROL 編集]**」をタップします。
   * 画像セットアセットをタップしてから、ツールバーの&#x200B;]**編集**[!UICONTROL （鉛筆アイコン）をタップします。

1. 画像セット内の画像を編集するには、次のいずれかの操作をおこないます。

   * アセットを並べ替えるには、画像を新しい位置までドラッグします（並べ替えアイコンを選択して項目を移動します）。
   * 項目を昇順または降順に並べ替えるには、列の見出しをクリックします。
   * アセットを追加するか既存のアセットを更新するには、「**[!UICONTROL アセットを追加」をクリックします。]**&#x200B;アセットに移動して選択し、ページの右上隅にある「**[!UICONTROL 選択]**」をタップしますページ。

      >[!NOTE]
      >
      >AEM でサムネール用に使用されている画像を別の画像に置き換えて削除しても、元のアセットは表示されたままになります。
   * To delete an asset, select it and tap or click **[!UICONTROL Delete Asset.]**
   * プリセットを適用するには、ページの右上隅付近にある「**[!UICONTROL プリセット]**」をタップし、ビューアプリセットを選択します。
   * サムネールを追加または変更するには、該当するアセットの右横にあるサムネールアイコンを選択します。Navigate to the new thumbnail or swatch asset, select it, then tap **[!UICONTROL Select.]**
   * To delete an entire Image Set, navigate to the Image Set, select it, and tap **[!UICONTROL Delete.]**

   >[!NOTE]
   >
   >画像セットの画像を編集するには画像セットに移動し、左側のレールの「**[!UICONTROL メンバーを設定]**」をタップしてから、個々のアセットの鉛筆アイコンをタップして編集ウィンドウを開きます。

1. 編集が完了したら、「**[!UICONTROL 保存]**」をタップします。

## 画像セットのプレビュー {#previewing-image-sets}

詳しくは、[アセットのプレビュー](/help/assets/previewing-assets.md)を参照してください。

## 画像セットの公開 {#publishing-image-sets}

[アセットの公開](/help/assets/publishing-dynamicmedia-assets.md)を参照してください。
