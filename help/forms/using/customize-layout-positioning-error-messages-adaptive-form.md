---
title: アダプティブフォームのエラーメッセージのレイアウトと位置のカスタマイズ
seo-title: Customize layout and positioning of error messages of an adaptive form
description: アダプティブフォームのエラーメッセージのレイアウトと位置をカスタマイズできます。
seo-description: You can customize layout and positioning of the error messages of an adaptive for.
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
exl-id: 5cb3ee55-f411-4692-84f7-89bf6ade729d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 100%

---

# アダプティブフォームのエラーメッセージのレイアウトと位置のカスタマイズ{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

アダプティブフォームのエラーメッセージのレイアウトと位置をカスタマイズできます。次をカスタマイズできます。

* 対応の CSS プロパティに変更を加えないでフィールドのキャプションの位置とレイアウトをカスタマイズ
* インラインエラーメッセージの位置をカスタマイズ
* 動的ヘルプインジケーターのコンテンツをカスタマイズ
* 対応の CSS プロパティに変更を加えないでフィールドコンポーネント（キャプション、ウィジェット簡単な説明、詳細な説明、ヘルプインジケーターのコンポーネント）の位置をカスタマイズ

## フィールドのレイアウトをカスタマイズ {#customize-layout-of-fields}

単位のフィールドまたはすべてのフィールドのレイアウトをカスタマイズして、キャプションやエラーメッセージの位置を変更できます。カスタムレイアウトをフィールドに適用するには、次の手順を実行します。

### 単一フィールドのレイアウトをカスタマイズ {#customize-layout-of-a-single-field}

カスタムレイアウトを単一フィールドに適用するには、次の手順を実行します。

1. **スタイル**&#x200B;モードでフォームを開きます。スタイルモードでフォームを開くには、ページツールバーで ![canvas-drop-down](assets/canvas-drop-down.png)／**スタイル**&#x200B;をタップしてください。
1. **フォームオブジェクト**&#x200B;の下のサイドバーで、フィールドを選択し、編集ボタン ![edit-button](assets/edit-button.png) をタップしてください。
1. カスタマイズするフィールドの状態を選択し、その状態のスタイル設定を指定します。

   ![フィールドのインラインスタイル設定を指定する](assets/edit-error-state.png)

### フォームのすべてのフィールドのレイアウトをカスタマイズ {#customize-layout-of-all-the-fields-of-a-form}

AEM Forms では、テーマを作成してフォームに適用できるようになりました。テーマエディターにより、フォームコンポーネントのスタイル設定を 1 箇所で行うことができます。テーマを作成すると、コンポーネントレベルでスタイルを設定します。テーマの詳細については、「[AEM Forms におけるテーマ](../../forms/using/themes.md)」を参照してください。

テーマエディターを使用してテーマを作成し、フォームにおけるすべてのフィールドのレイアウトをカスタマイズします。テーマを作成するには、次の手順を実行します。

1. フォームを編集モードで開きます。

1. 編集モードで、コンポーネントを選択し、![フィールドレベル](assets/field-level.png)／**アダプティブフォームコンテナ**&#x200B;をタップしてから、 ![cmppr](assets/cmppr.png) をタップします。
1. アダプティブフォームテーマのサイドバーで、テーマエディタで作成したテーマを選択します。

## カスタムフィールドレイアウトを作成 {#create-a-custom-field-layout}

1. CRXDE Lite を開きます。デフォルトの URL は https://&#39;[server]:[port]&#39;/crx/de です。
1. /libs/fd/af/layouts/field node からフィールドレイアウト（例えば、defaultFieldLayout）を /apps node（例えば、/apps/af-field-layout）にコピーします。
1. コピーしたノードの名前と defaultFieldLayout.jsp ファイルの名前を変更します。例えば、errorOnRight.jsp。 

1. コピーしたノードの qtip および jcr:description プロパティの値を変更します。例えば、プロパティの値を「Error On Right」に変更します。

1. 新しいスタイルおよび動作を追加するには、/etc ノードでクライアントライブラリを作成します。

   例えば、/etc/af-field-layout-clientlib で、ノード client-library を作成します。値 af.field.errorOnRight を持つカテゴリプロパティと次のコードを持つ style.less ファイルを追加します。 

   ```css
   .widgetErrorWrapper {
   
    height: 38px;
    margin: 5px;
   
    .guideFieldWidget{
    width: 60%;
    float: left; 
    }
   
    .guideFieldError{
    overflow:hidden;
    width:40%; 
    }
   
   }
   ```

1. 外観と動作を向上するには、レイアウトファイル内で作成したクライアントライブラリを含めます（errorOnRight.jsp）。
1. フィールドの編集ダイアログを開き、「**スタイル**」タブを選択します。「**フィールドレイアウトを設定**」ドロップダウンボックスで、新しく作成したレイアウトを選択し、「**OK**」をクリックします。

ErrorOnRight.zip パッケージには、フィールドの右側にエラーメッセージを表示するコードが含まれます。

[ファイルを入手](assets/erroronright.zip)
