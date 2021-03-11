---
title: ページへの Dynamic Media アセットの追加
description: Webサイトで使用するアセットにDynamic Media機能を追加するには、Dynamic Mediaまたはインタラクティブメディアコンポーネントを直接ページに追加します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
translation-type: tm+mt
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 49%

---


# ページへの Dynamic Media アセットの追加{#adding-dynamic-media-assets-to-pages}

Webサイトで使用するアセットにDynamic Media機能を追加するには、**[!UICONTROL Dynamic Media]**&#x200B;または&#x200B;**[!UICONTROL インタラクティブメディア]**&#x200B;コンポーネントを直接ページに追加します。 これを行うには、[!UICONTROL デザイン]モードに入り、Dynamic Mediaコンポーネントを有効にします。 次に、これらのコンポーネントをページに追加し、そのコンポーネントにアセットを追加できます。Dynamic Mediaとインタラクティブメディアコンポーネントはスマートで、画像とビデオのどちらを追加するかを知っており、使用可能なオプションがそれに応じて変化します。

AEM を WCM として使用している場合は、Dynamic Media アセットを直接ページに追加します。

>[!NOTE]
>
>画像マップは追加設定なしでカルーセルバナーで使用できます。

## ページへの Dynamic Media コンポーネントの追加 {#adding-a-dynamic-media-component-to-a-page}

[!UICONTROL Dynamic Media]または[!UICONTROL インタラクティブメディア]コンポーネントをページに追加するのと、ページにコンポーネントを追加するのと同じです。 [!UICONTROL Dynamic Media]と[!UICONTROL インタラクティブメディア]のコンポーネントについては、以下の節で詳しく説明します。

ページにダイナミックメディアコンポーネント／ビューアを追加するには：

1. AEM で、Dynamic Media コンポーネントを追加するページを開きます。
1. Dynamic Mediaコンポーネントが使用できない場合は、[!UICONTROL サイドキック]のルーラーをクリックして&#x200B;**[!UICONTROL デザイン]**&#x200B;モードに入り、**[!UICONTROL パーシスを編集]**&#x200B;をクリックし、**[!UICONTROL Dynamic Media]**&#x200B;を選択してDynamic Mediaコンポーネントを使用可能にします。

   >[!NOTE]
   >
   >詳しくは、[デザインモードでのコンポーネントの設定](/help/sites-authoring/default-components-designmode.md)を参照してください。

1. **[!UICONTROL サイドキック]の鉛筆アイコンをクリックして、[!UICONTROL 編集]**&#x200B;モードに戻ります。
1. サイドキックの&#x200B;**[!UICONTROL その他]**&#x200B;グループから目的の場所のページに、**[!UICONTROL Dynamic Media]**&#x200B;または&#x200B;**[!UICONTROL インタラクティブメディア]**&#x200B;コンポーネントをドラッグします。
1. 「**[!UICONTROL 編集]**」をクリックしてコンポーネントを開きます。
1. [](#dynamic-media-component)コンポーネントの編集を必要に応じておこない、「**[!UICONTROL OK]**」をクリックして変更内容を保存します。

## Dynamic Media コンポーネント {#dynamic-media-components}

[!UICONTROL Dynamic ] Mediaおよび [!UICONTROL Interactive ] Mediaは、  Dynamic Mediaの **[!UICONTROL Sidekickで入手できます。]****[!UICONTROL インタラクティブメディア]**&#x200B;コンポーネントは、すべてのインタラクティブアセット（インタラクティブビデオ、インタラクティブ画像、カルーセルセットなど）に使用します。その他すべてのDynamic Mediaコンポーネントには、**[!UICONTROL Dynamic Media]**&#x200B;コンポーネントを使用します。

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できません。使用する前にデザインモードで選択しておく必要があります。[コンポーネントをデザインモードで使用できるようになったら](/help/sites-authoring/default-components-designmode.md)、他のAEMコンポーネントと同様に、コンポーネントをページに追加できます。

### Dynamic Media コンポーネント {#dynamic-media-component}

Dynamic Mediaコンポーネントはスマートです。画像を追加するかビデオを追加するかに応じて、様々なオプションがあります。 このコンポーネントは画像プリセット、画像ベースのビューア（画像セット、スピンセット、混在メディアセットなど）およびビデオをサポートします。また、ビューアはレスポンシブです。 つまり、画面のサイズは、画面のサイズに基づいて自動的に変更されます。 すべてのビューアはHTML5ベースのビューアです。

>[!NOTE]
>
>[!UICONTROL Dynamic Media]コンポーネントを追加し、**[!UICONTROL Dynamic Media設定]**&#x200B;が空白の場合、またはアセットを正しく追加できない場合は、次を確認してください。
>
>* [Dynamic Media を有効にしている](/help/assets/config-dynamic.md)こと。Dynamic Media はデフォルトで無効になっています。
>* 画像にピラミッドのTIFFファイルが含まれています。Dynamic Mediaが有効になる前に読み込まれた画像には、ピラミッドTIFFファイルがありません。

>



#### 画像を操作する場合 {#when-working-with-images}

[!UICONTROL Dynamic Media]コンポーネントを使用すると、画像セット、スピンセット、混在メディアセットなどの動的な画像を追加できます。ズームイン、ズームアウトが可能です。必要に応じて、スピンセット内の画像を回転させたり、別の種類の画像セットから画像を選択したりできます。

また、ビューアプリセット、画像プリセットまたは画像形式をコンポーネント内で直接設定することもできます。画像をレスポンシブにするために、ブレークポイントの設定かレスポンシブ画像プリセットの適用のいずれかを実行できます。

![chlimage_1-72](assets/chlimage_1-72a.png)

次のDynamic Media設定を編集するには、コンポーネントで「**[!UICONTROL 編集]**」をクリックし、「**[!UICONTROL Dynamic Media設定]**」タブをクリックします。

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>デフォルトでは、Dynamic Media 画像コンポーネントはアダプティブです。固定サイズにする場合は、「**[!UICONTROL 詳細]**」タブのコンポーネントに、**[!UICONTROL 幅]**&#x200B;および&#x200B;**[!UICONTROL 高さ]**&#x200B;のプロパティを設定します。

**[!UICONTROL ビューアプリセット]**  — ドロップダウンメニューから既存のビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

これは、画像セット、スピンセットまたは混在メディアセットを表示している場合に使用できる唯一のオプションです。表示されるビューアプリセットもスマートで、関連するビューアプリセットのみが表示されます。

**[!UICONTROL 画像プリセット]**  — ドロップダウンメニューから既存の画像プリセットを選択します。探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

**[!UICONTROL 画像修飾子]**  — 画像効果を変更するには、追加の画像コマンドを指定します。これらについては、[画像プリセットの管理](/help/assets/managing-viewer-presets.md)および[コマンドリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)で説明します。

このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

**[!UICONTROL ブレークポイント]**  — レスポンシブサイトでこのアセットを使用する場合は、ページのブレークポイントを追加する必要があります。画像のブレークポイントをコンマ（,）で区切って指定する必要があります。このオプションを使用できるのは、画像プリセットで高さまたは幅が定義されていないときです。

このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

コンポーネント内の&#x200B;**[!UICONTROL 「]**&#x200B;編集」をクリックして、次の[!UICONTROL 詳細設定]を編集できます。

**[!UICONTROL タイトル]**  — 画像のタイトルを変更します。

**[!UICONTROL 代替テキスト]**  — グラフィックをオフにしているユーザーの画像のタイトル。

このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

**[!UICONTROL URL、開く場所]**  — リンクを開くアセットを設定できます。**[!UICONTROL URL]**&#x200B;と&#x200B;**[!UICONTROL Open in]**&#x200B;を設定して、同じウィンドウで開くか、新しいウィンドウで開くかを指定します。

このオプションは、画像セット、スピンセットまたは混在メディアセットを表示している場合には使用できません。

**[!UICONTROL 幅と高さ]**  — 画像を固定サイズにする場合は、値をピクセル単位で入力します。これらの値を空にすると、アダプティブなアセットになります。

#### ビデオの操作時{#when-working-with-video}

[!UICONTROL Dynamic Media]コンポーネントを使用して、動的なビデオをWebページに追加します。コンポーネントを編集する際に、定義済みのビデオビューアプリセットをページ上でのビデオ再生に使用するよう選択できます。

![chlimage_1-74](assets/chlimage_1-74a.png)

コンポーネント内の&#x200B;**[!UICONTROL 「]**&#x200B;編集」をクリックして、次の[!UICONTROL Dynamic Media設定]を編集できます。

>[!NOTE]
>
>デフォルトでは、Dynamic Media ビデオコンポーネントはアダプティブです。ビデオコンポーネントを固定サイズにする場合は、そのコンポーネントで、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL 幅]**」と「**[!UICONTROL 高さ]**」を使用してサイズを設定します。

**[!UICONTROL ビューアプリセット]**  — ドロップダウンメニューから既存のビデオビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。

コンポーネント内の&#x200B;**[!UICONTROL 「]**&#x200B;編集」をクリックして、次の[!UICONTROL 詳細設定]を編集できます。

**[!UICONTROL タイトル]**  — ビデオのタイトルを変更します。

**[!UICONTROL 幅と高さ]**  — ビデオを固定サイズにする場合は、値をピクセル単位で入力します。これらの値を空にすると、アダプティブな画像になります。

#### セキュアビデオの配信方法 {#how-to-delivery-secure-video}

AEM 6.2 で [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480) をインストールする場合、ビデオをセキュア SSL 接続（HTTPS）と非セキュア接続（HTTP）のどちらで配信するかを制御できます。デフォルトでは、ビデオ配信プロトコルは、埋め込み Web ページのプロトコルから自動的に継承されます。Web ページが HTTPS で読み込まれる場合、ビデオも HTTPS で配信されます。逆の場合も同様です。Web ページが HTTP で読み込まれる場合、ビデオも HTTP で配信されます。ほとんどの場合、このデフォルトの動作で問題ないため、特に設定を変更する必要はありません。ただし、ビデオをセキュアに配信するために、`VideoPlayer.ssl=on` を URL パスの最後に付加するか、または埋め込みコードスニペットにある他のビューアの設定パラメーターのリストに付加して、このデフォルトの動作をオーバーライドすることができます。

ビデオのセキュア配信、および URL パスの `VideoPlayer.ssl` 設定属性の使用について詳しくは、『ビューアリファレンスガイド』の「[ビデオのセキュア配信](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html)」を参照してください。ビデオビューアの他に、セキュアビデオ配信は混在メディアビューアとインタラクティブビデオビューアで使用できます。

### インタラクティブメディアコンポーネント {#interactive-media-component}

インタラクティブメディアコンポーネントは、インタラクティビティ（ホットスポットまたは画像マップ）を含むアセット用です。インタラクティブ画像、インタラクティブビデオまたはカルーセルバナーがある場合は、**[!UICONTROL インタラクティブメディア]**&#x200B;コンポーネントを使用します。

[!UICONTROL インタラクティブメディア]コンポーネントはスマートです。画像とビデオのどちらを追加するかによって、様々なオプションがあります。 また、ビューアはレスポンシブです。 つまり、画面のサイズは、画面のサイズに基づいて自動的に変更されます。 すべてのビューアはHTML5ベースのビューアです。

![chlimage_1-75](assets/chlimage_1-75a.png)

コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の&#x200B;**[!UICONTROL 一般]**&#x200B;設定を編集できます。

**[!UICONTROL ビューアプリセット]**  — ドロップダウンメニューから既存のビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。ビューアプリセットを使用するには、あらかじめ公開する必要があります。詳しくは、ビューアプリセットの管理を参照してください。

**[!UICONTROL タイトル]**  — ビデオのタイトルを変更します。

**[!UICONTROL 幅と高さ]**  — ビデオを固定サイズにする場合は、値をピクセル単位で入力します。これらの値を空にすると、アダプティブな画像になります。

コンポーネントの「**[!UICONTROL 編集]**」をクリックして、次の&#x200B;**[!UICONTROL 買い物かごに追加]**&#x200B;設定を編集できます。

**[!UICONTROL 製品アセットを表示]**  — デフォルトでは、この値が選択されています。製品アセットには、コマースモジュールで定義された製品の画像が表示されます。製品アセットを表示しない場合はチェックマークをオフにします。

**[!UICONTROL 製品価格の表示]**  — デフォルトでは、この値が選択されています。製品価格には、コマースモジュールで定義されたアイテムの価格が表示されます。製品価格を表示しない場合はチェックマークをオフにします。

**[!UICONTROL 製品フォームを表示]**  — デフォルトでは、この値は選択されていません。製品フォームには、サイズや色など製品のバリエーションが含まれます。製品のバリエーションを表示しない場合はチェックマークをオフにします。
