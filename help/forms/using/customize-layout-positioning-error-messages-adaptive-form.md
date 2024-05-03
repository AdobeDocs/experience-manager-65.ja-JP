---
title: アダプティブフォームのエラーメッセージのレイアウトと位置をカスタマイズ
description: アダプティブフォームのエラーメッセージのレイアウトと位置をカスタマイズできます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 5cb3ee55-f411-4692-84f7-89bf6ade729d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 100%

---

# アダプティブフォームのエラーメッセージのレイアウトと位置をカスタマイズ{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

アダプティブフォームのエラーメッセージのレイアウトと位置をカスタマイズできます。次のようにカスタマイズできます。

* 対応の CSS プロパティに変更を加えないでフィールドのキャプションの位置とレイアウトをカスタマイズ
* インラインエラーメッセージの位置をカスタマイズ
* 動的ヘルプインジケーターのコンテンツをカスタマイズ
* 対応の CSS プロパティに変更を加えないでフィールドコンポーネント（キャプション、ウィジェット、簡単な説明、詳細な説明、ヘルプインジケーターのコンポーネント）の位置をカスタマイズ

## フィールドのレイアウトをカスタマイズ {#customize-layout-of-fields}

単一のフィールドまたはすべてのフィールドのレイアウトをカスタマイズして、キャプションやエラーメッセージの位置を変更できます。

フィールドにカスタムレイアウトを適用するには、以下の手順を実行します。

### 単一フィールドのレイアウトをカスタマイズ {#customize-layout-of-a-single-field}

1. **スタイル**&#x200B;モードでフォームを開きます。スタイルモードでフォームを開くには、ページツールバーで ![canvas-drop-down](assets/canvas-drop-down.png)／**スタイル**&#x200B;を選択します。
1. **フォームオブジェクト**&#x200B;の下のサイドバーで、フィールドを選択し、編集ボタン ![edit-button](assets/edit-button.png) を選択してください。
1. カスタマイズするフィールドの状態を選択し、その状態のスタイル設定を指定します。

   ![フィールドのインラインスタイル設定を指定する](assets/edit-error-state.png)

### フォームのすべてのフィールドのレイアウトをカスタマイズ {#customize-layout-of-all-the-fields-of-a-form}

AEM Forms では、テーマを作成してフォームに適用できるようになりました。テーマエディターにより、フォームコンポーネントのスタイル設定を 1 箇所で行うことができます。テーマを作成したら、コンポーネントレベルでスタイルを設定します。テーマについて詳しくは、[AEM Forms におけるテーマ](../../forms/using/themes.md)を参照してください。

テーマエディターを使用してテーマを作成し、フォームにおけるすべてのフィールドのレイアウトをカスタマイズします。テーマを作成したら、次の手順を実行してフォームに適用します。

1. フォームを編集モードで開きます。

1. 編集モードで、コンポーネントを選択し、![field-level](assets/field-level.png)／**ドキュメントコンテナ**&#x200B;をクリックしてから、![cmppr](assets/cmppr.png) を選択します。
1. アダプティブフォームテーマのサイドバーで、テーマエディターで作成したテーマを選択します。

## カスタムフィールドレイアウトを作成 {#create-a-custom-field-layout}

1. CRXDE Lite を開きます。デフォルトの URL は https://&#39;[server]:[port]&#39;/crx/de です。
1. /libs/fd/af/layouts/field ノードからフィールドレイアウト（例えば、defaultFieldLayout）を /apps ノード（例えば、/apps/af-field-layout）にコピーします。
1. コピーしたノードの名前と defaultFieldLayout.jsp ファイルの名前を変更します。例えば、errorOnRight.jsp。 

1. コピーしたノードの qtip および jcr:description プロパティの値を変更します。例えば、プロパティの値を「Error On Right」に変更します。

1. 新しいスタイルおよび動作を追加するには、/etc ノードでクライアントライブラリを作成します。

   例えば、/etc/af-field-layout-clientlib で、ノード client-library を作成します。値 af.field.errorOnRight を持つカテゴリプロパティと、次のコードを持つ style.less ファイルを追加します。

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
1. フィールドの編集ダイアログを開き、「**スタイル**」タブを選択します。**フィールドレイアウトを設定**&#x200B;ドロップダウンボックスで、新しく作成したレイアウトを選択し、「**OK**」をクリックします。

ErrorOnRight.zip パッケージには、フィールドの右側にエラーメッセージを表示するコードが含まれます。

[ファイルを入手](assets/erroronright.zip)
