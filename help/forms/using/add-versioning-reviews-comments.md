---
title: AEM 6.5 アダプティブフォームへのバージョン管理、コメント、注釈の追加
description: AEM 6.5 アダプティブフォームのコアコンポーネントを使用して、アダプティブフォームにコメント、注釈およびバージョン管理を追加します。
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
exl-id: 91e6fca2-60ba-45f1-98c3-7b3fb1d762f5
source-git-commit: 130d900a9c268362b75ffa947606c7145a1f8c9d
workflow-type: ht
source-wordcount: '631'
ht-degree: 100%

---

# アダプティブフォームのバージョン管理、レビューおよびコメント

<!--
<span class="preview"> This feature is under the early adopter program. If you're interested in joining our early access program for this feature, send an email from your official address to aem-forms-ea@adobe.com to request access </span>
-->

<span class="preview">この機能は、デフォルトでは有効になっていません。公式アドレスから aem-forms-ea@adobe.com に書き込んで、機能へのアクセスをリクエストできます。</span>

アダプティブフォームのコアコンポーネントを使用すると、フォーム作成者はフォームにバージョン管理、コメント、注釈を追加できます。これらの機能により、ユーザーは複数のバージョンを作成および管理し、コメントを通じて共同作業を行い、特定のフォームセクションにメモを追加できるようになり、フォーム開発が簡素化され、フォーム作成エクスペリエンスが向上します。

アダプティブフォームのバージョン管理、コメント、注釈の機能について詳しくは、このステップバイステップのビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3463265)

## 前提条件 {#prerequisite-versioning}

アダプティブフォームでバージョン管理、コメント、注釈の機能を使用するには、AEM 6.5 Forms 環境で[アダプティブフォームのコアコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components)が有効になっていることを確認します。

## アダプティブフォームのバージョン管理 {#adaptive-form-versioning}

アダプティブフォームのバージョン管理は、フォームにバージョンを追加するのに役立ちます。フォーム作成者は、フォームの複数のバージョンを簡単に作成し、最終的にビジネス目標に適したバージョンを使用できます。さらに、フォームユーザーは、フォームを以前のバージョンに戻すこともできます。また、作成者は、フォームの 2 つのバージョンをプレビューして比較することが容易になるので、UI の観点からフォームをより適切に分析できます。各アダプティブフォームのバージョン管理機能について詳しく見ていきましょう。

### フォームのバージョンの作成 {#create-a-form-version}

フォームのバージョンを作成するには、次の手順に従います。

1. AEM Forms 環境で、**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動し、**フォーム**&#x200B;を選択します。
1. 左側のパネルの選択ドロップダウンから、「**[!UICONTROL バージョン]**」を選択します。
   ![フォームの選択](assets/select-a-form.png)
1. 左下のパネルにある **3 つのドット**&#x200B;をクリックし、「**[!UICONTROL バージョンとして保存]**」をクリックします。
1. フォームのバージョンにラベルを指定します。コメントを通じてフォームに関する情報を追加することもできます。
   ![フォームのバージョンの作成](assets/create-a-form-version.png)

### フォームのバージョンの更新 {#update-a-form-version}

フォームを編集および更新したら、新しいバージョンをフォームに追加します。最後の節で示した手順に従って、画像に示すようにフォームの新しいバージョンに名前を付けます。

![フォームのバージョンの更新](assets/update-a-form-version.png)

### フォームのバージョンを元に戻す {#revert-a-form-version}

フォームのバージョンを以前のバージョンに戻すには、フォームのバージョンを選択し、「**[!UICONTROL このバージョンに戻る]**」をクリックします。

![フォームのバージョンを元に戻す](assets/revert-form-version.png)

### フォームのバージョンの比較 {#compare-form-versions}

フォーム作成者は、プレビュー目的で 2 つの異なるバージョンのフォームを比較できます。バージョンを比較するには、フォームのバージョンを選択し、「**[!UICONTROL 現在のバージョンと比較]**」をクリックします。プレビューモードで 2 つの異なるフォームのバージョンが表示されます。

![フォームのバージョンの比較](assets/compare-form-versions.png)

## コメントの追加 {#add-comments}

レビューとは、1 人以上のレビュー担当者に対してフォームへのコメントを許可するメカニズムです。フォームユーザーは誰でもフォームにコメントしたり、コメントを通じてフォームをレビューしたりできます。フォームにコメントするには、「**[!UICONTROL フォーム]**」を選択し、フォームに&#x200B;**[!UICONTROL コメント]**&#x200B;を追加します。

>[!NOTE]
> 上記で説明したように、アダプティブフォームのコアコンポーネントでコメントを使用すると、フォーム機能の[フォームへのレビュアーの追加](/help/forms/using/create-reviews-forms.md)が無効になります。


![フォームにコメントの追加](assets/form-comments.png)

## 注釈の追加 {#adaptive-form-annotations}

多くの場合、フォームグループのユーザーは、レビューの目的で、フォームの特定のタブやコンポーネントなどに注釈を追加する必要があります。このような場合、作成者は注釈を使用できます。
フォームに注釈を追加するには、次の手順を実行します。

1. **[!UICONTROL 編集]**&#x200B;モードでフォームを開きます。

1. 画像に示すように、右上のパネルにある&#x200B;**追加アイコン**をクリックします。
   ![注釈](assets/annotation.png)

1. 次に、画像に示すように、左上のパネルにある **追加アイコン** をクリックして、注釈を追加します。
   ![注釈の追加](assets/add-annotation.png)

1. これで、コメントを追加したり、複数のカラーでスケッチを描画してフォームコンポーネントを作成したりできます。

1. フォームに追加したすべての注釈を表示するには、フォームを選択すると、画像に示すように、左側のパネルに追加した注釈が表示されます。

   ![追加した注釈を表示](assets/see-annotations.png)

## 関連トピック

* [アダプティブフォームのコアコンポーネントの比較](/help/forms/using/compare-forms-core-components.md)
