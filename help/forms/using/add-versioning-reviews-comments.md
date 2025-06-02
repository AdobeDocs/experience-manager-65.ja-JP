---
title: Am AEM 6.5 アダプティブフォームにバージョン、コメント、注釈を追加する。
description: AEM 6.5 アダプティブフォームのコアコンポーネントを使用すると、アダプティブフォームにコメント、注釈、バージョン管理を追加できます。
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
exl-id: 91e6fca2-60ba-45f1-98c3-7b3fb1d762f5
source-git-commit: 130d900a9c268362b75ffa947606c7145a1f8c9d
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 50%

---

# アダプティブフォームのバージョン管理、レビューおよびコメント

<!--
<span class="preview"> This feature is under the early adopter program. If you're interested in joining our early access program for this feature, send an email from your official address to aem-forms-ea@adobe.com to request access </span>
-->

<span class="preview"> この機能はデフォルトでは有効になっていません。 公式アドレスからaem-forms-ea@adobe.comに書き込んで、機能へのアクセスをリクエストできます。</span>

アダプティブフォームのコアコンポーネントを使用すると、フォーム作成者はフォームにバージョン管理、コメント、注釈を追加できます。 これらの機能を使用すると、複数のバージョンの作成と管理、コメントを介した共同作業、特定のフォームセクションへのメモの追加などが可能になり、フォームの作成作業が簡略化されます。

アダプティブフォームのバージョン管理、コメント、注釈の機能については、このビデオを参照してください。

>[!VIDEO](https://video.tv.adobe.com/v/3463265)

## 前提条件 {#prerequisite-versioning}

アダプティブフォームでバージョン管理機能、コメント機能、注釈機能を使用するには、AEM 6.5 Formsで [ アダプティブフォームのコアコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components) が有効になっていることを確認してください。

## アダプティブフォームのバージョン管理 {#adaptive-form-versioning}

アダプティブフォームのバージョン管理は、フォームにバージョンを追加するのに役立ちます。フォーム作成者は、フォームの複数のバージョンを簡単に作成し、最終的にビジネス目標に適したバージョンを使用できます。さらに、フォームユーザーは、フォームを以前のバージョンに戻すこともできます。また、作成者は、フォームの 2 つのバージョンをプレビューして比較することが容易になるので、UI の観点からフォームをより適切に分析できます。各アダプティブフォームのバージョン管理機能について詳しく見ていきましょう。

### フォームのバージョンの作成 {#create-a-form-version}

フォームのバージョンを作成するには、次の手順に従います。

1. AEM Forms環境で、**[!UICONTROL フォーム]**/]**2}Formsおよびドキュメント } に移動し、** フォーム **を選択します。**[!UICONTROL 
1. 左パネルの選択ドロップダウンから、「**[!UICONTROL バージョン]**」を選択します。
   ![フォームの選択](assets/select-a-form.png)
1. 左下のパネルにある **3 つのドット**&#x200B;をクリックし、「**[!UICONTROL バージョンとして保存]**」をクリックします。
1. フォームバージョンにラベルを指定します。コメントを通じてフォームに関する情報を追加することもできます。
   ![フォームのバージョンの作成](assets/create-a-form-version.png)

### フォームのバージョンの更新 {#update-a-form-version}

フォームを編集および更新したら、新しいバージョンをフォームに追加します。 最後の節で示した手順に従って、画像に示すようにフォームの新しいバージョンに名前を付けます。

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
> 前述のように、アダプティブフォームのコアコンポーネントでコメントを使用すると、フォーム機能 [ フォームへのレビュー担当者の追加 ](/help/forms/using/create-reviews-forms.md) が無効になります。


![フォームにコメントの追加](assets/form-comments.png)

## 注釈の追加 {#adaptive-form-annotations}

多くの場合、フォームグループユーザーは、レビュー目的（特定のタブやフォームのコンポーネントなど）でフォームに注釈を追加する必要があります。 このような場合、作成者は注釈を使用できます。
フォームに注釈を追加するには、次の手順を実行します。

1. **[!UICONTROL 編集]**&#x200B;モードでフォームを開きます。

1. 画像に示すように、右上のパネルにある&#x200B;**追加アイコン**をクリックします。
   ![注釈](assets/annotation.png)

1. 次に、画像で示されているように左上のレールにある **追加アイコン** をクリックして、注釈を追加します。
   ![注釈の追加](assets/add-annotation.png)

1. これで、コメントを追加したり、複数のカラーでスケッチを描画してフォームコンポーネントを作成したりできます。

1. フォームに追加されたすべての注釈を表示するには、フォームを選択すると、画像に示すように、左側のパネルに注釈が追加されます。

   ![追加した注釈を表示](assets/see-annotations.png)

## 関連トピック

* [アダプティブ Formsのコアコンポーネントの比較](/help/forms/using/compare-forms-core-components.md)
