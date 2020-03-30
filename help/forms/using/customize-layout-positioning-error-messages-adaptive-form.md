---
title: アダプティブフォームのエラーメッセージのレイアウトと位置のカスタマイズ
seo-title: アダプティブフォームのエラーメッセージのレイアウトと位置のカスタマイズ
description: 'アダプティブフォームのエラーメッセージのレイアウトと位置をカスタマイズできます。 '
seo-description: 'アダプティブフォームのエラーメッセージのレイアウトと位置をカスタマイズできます。 '
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

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

1. **スタイル**&#x200B;モードでフォームを開きます。To open the form in style mode, in the page toolbar tap ![canvas-drop-down](assets/canvas-drop-down.png) > **Style**.
1. In the sidebar, under **Form Objects**, select the field and tap the edit button ![edit-button](assets/edit-button.png).
1. カスタマイズするフィールドの状態を選択し、その状態のスタイル設定を指定します。

   ![フィールドのインラインスタイル設定を指定する](assets/edit-error-state.png)

### フォームのすべてのフィールドのレイアウトをカスタマイズ {#customize-layout-of-all-the-fields-of-a-form}

AEM Forms では、テーマを作成してフォームに適用できるようになりました。テーマエディターにより、フォームコンポーネントのスタイル設定を 1 箇所で行うことができます。テーマを作成すると、コンポーネントレベルでスタイルを設定します。テーマの詳細については、「[AEM Forms におけるテーマ](../../forms/using/themes.md)」を参照してください。

テーマエディターを使用してテーマを作成し、フォームにおけるすべてのフィールドのレイアウトをカスタマイズします。テーマを作成するには、次の手順を実行します。

1. フォームを編集モードで開きます。
1. In the edit mode, select a component, then tap ![field-level](assets/field-level.png) > **Adaptive Form Container**, and then tap ![cmppr](assets/cmppr.png).
1. アダプティブフォームテーマのサイドバーで、テーマエディタで作成したテーマを選択します。

## カスタムフィールドレイアウトを作成 {#create-a-custom-field-layout}

1. CRXDE Lite を開きます。The default URL is https://&#39;[server]:[port]&#39;/crx/de.
1. /libs/fd/af/layouts/field node からフィールドレイアウト（例えば、defaultFieldLayout）を /apps node（例えば、/apps/af-field-layout）にコピーします。
1. コピーしたノードの名前と defaultFieldLayout.jsp ファイルの名前を変更します。例えば、errorOnRight.jsp。 

1. コピーしたノードのqtipおよびjcr:descriptionプロパティの値を変更します。 例えば、プロパティの値を「Error On Right」に変更します。

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
