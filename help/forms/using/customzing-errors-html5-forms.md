---
title: HTML5 フォームのエラーメッセージのカスタマイズ
seo-title: HTML5 フォームのエラーメッセージのカスタマイズ
description: HTML5 フォームのエラーメッセージの表示をカスタマイズする方法（メッセージの位置や外観の変更方法を含む）について説明します。
seo-description: HTML5 フォームのエラーメッセージの表示をカスタマイズする方法（メッセージの位置や外観の変更方法を含む）について説明します。
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 78%

---


# HTML5 フォームのエラーメッセージのカスタマイズ {#customizing-error-messages-for-html-forms}

初期設定の状態の HTML5 フォームでは、エラーメッセージおよび警告の位置と外観（フォントおよび色）は固定されており、エラーは選択されたフィールドにのみひとつだけ表示されます。

この記事では、HTML5フォームのエラーメッセージをカスタマイズして、

* エラーメッセージの外観および位置を変更できます。任意のフィールドの上、下、右にエラーを表示させることができます。
* 複数のフィールドのエラーメッセージをいつでも表示できます。
* フィールドが選択されているかどうかに関係なく、エラーを表示します。

## エラーメッセージのカスタマイズ{#customizing-error-messages-nbsp}

エラーメッセージをカスタマイズする前に、添付のパッケージ (CustomErrorManager-1.0-SNAPSHOT.zip) をダウンロードして抽出します。

パッケージの抽出後、CustomErrorManager-1.0-SNAPSHOT フォルダーを開きます。jcr_root および META-INF フォルダーが含まれています。これらのフォルダーには、エラーメッセージのカスタマイズに必要な CSS および JS ファイルが含まれています。

[ファイルを入手](assets/customerrormanager-1.0-snapshot.zip)

### エラーメッセージの位置のカスタマイズ{#customizing-the-position-of-error-messages-nbsp}

エラーメッセージの位置をカスタマイズするには、各エラーおよび警告フィールドごとに &lt;div> タグを追加し、&lt;div> タグを左側または右側に配置して &lt;div> タグに CSS スタイルを適用します。詳しくは、次の手順を参照してください。

1. Navigate to the `CustomErrorManager-1.0-SNAPSHOT`folder and open the `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` folder.
1. Open the `customErrorManager.js` file for editing. The `markError` function in the file accepts the following parameters:

   |  |  |
   |---|---|
   | jqWidget | ウィジェットのハンドル |
   | msg | エラーメッセージが含まれています |
   | type | エラーか警告かを表します |

1. 初期設定での実装では、エラーメッセージはフィールドの右側に表示されます。エラーメッセージを上側に表示するには、次のコードを使用します。

   ```javascript
   markError: function (jqWidget, msg, type) {
               var element = jqWidget.element,                                //Gives the div containing widget
                   pos = $(element).offset(),                          //Calculates the position of the div in the view port
                                                                   msgHeight = xfalib.view.util.TextMetrics.measureExtent(msg).height + 5;  //Calculating the height of the Error Message
                   styles = {};
                   styles.left = pos.left + "px";         // Assign the desired left position using pos.left. Here it is calculated for exact left of the field
                   styles.top = pos.top - msgHeight + "px";  // Assign the desired top position using pos.top. Here it is calculated for top of the field
               if (type != "warning") {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the warning div if it is not present already
                       jqWidget.errorDiv=$("<div id='customError'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the warning div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               } else {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the error div if it is not present already
                       jqWidget.errorDiv=$("<div id='customWarning'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the error div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               }
   
           },
   ```

1. ファイルを保存して閉じます。
1. `CustomErrorManager-1.0-SNAPSHOT` フォルダーに移動し、jcr_root および META-INF フォルダーのアーカイブを作成します。アーカイブの名前を CustomErrorManager-1.0-SNAPSHOT.zip に変更します。
1. パッケージマネージャーを使ってパッケージをアップロードし、インストールします。

## 複数のフィールドのエラーメッセージの表示{#display-error-messages-for-multiple-fields-nbsp}

すべてのフィールドのエラーメッセージを同時に表示するには、添付されているパッケージを使用します。エラーメッセージを単独で表示するには、デフォルトのプロファイルを使用します。

### エラーメッセージの外観のカスタマイズ{#customizing-the-appearance-of-error-messages-nbsp}

1. etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css フォルダーに移動します。

1. sample.css ファイルを開いて編集します。CSS ファイルには、#customError と #customWarning の 2 つの ID が含まれています。これらの ID を使用して、色やフォントサイズなど、さまざまなプロパティを変更することができます。

   エラー／警告メッセージのフォントサイズおよび色を変更するには、次のコードを使用します。

   ```css
   #customError {
   color: #0000FF; // it changes the color of Error Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 24px;  // it changes the font size of Error Message
   z-index:5;
   }
   
   #customWarning {
   color: #00FF00;  // it changes the color of Warning Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 18px;   // it changes the font size of Warning Message
   z-index:5;
   }
   
   Save the changes.
   ```

1. ファイルを保存して閉じます。
1. CustomErrorManager-1.0-SNAPSHOT フォルダーに移動し、jcr_root および META-INF フォルダーのアーカイブを作成します。アーカイブの名前を CustomErrorManager-1.0-SNAPSHOT.zip に変更します。
1. パッケージマネージャーを使ってパッケージをアップロードし、インストールします。

## 新しいプロファイルでフォームをレンダリングします。  {#render-the-form-with-the-new-profile-nbsp}

初期設定では、html5フォームは次のデフォルトのプロファイルを使用します。 https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location>&amp;template=&lt;name of the xdp>

カスタムエラーメッセージを使用してフォームを表示するには、次のエラープロファイルを使用してフォームをレンダリングします。 https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location>&amp;template=&lt;name of the xdp>

>[!NOTE]
>
>エラープロファイルは、添付されているパッケージによりインストールされます。

