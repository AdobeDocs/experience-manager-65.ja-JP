---
title: HTML5 フォームのエラーメッセージのカスタマイズ
description: 位置や外観を変更する方法など、HTML5 フォームのエラーメッセージの表示をカスタマイズする方法について説明します。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
feature: Mobile Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 31%

---

# HTML5 フォームのエラーメッセージのカスタマイズ {#customizing-error-messages-for-html-forms}

HTML5 フォームでは、初期設定の状態で、エラーメッセージおよび警告の位置と外観（フォントと色）は固定されています。エラーは、選択したフィールドに対してのみ表示され、エラーは 1 つだけ表示されます。

この記事では、次の操作を行うために、HTML5 forms エラーメッセージをカスタマイズする手順を説明します。

* エラーメッセージの外観と位置を変更する手順を説明します。エラーの表示位置は、フィールドの上側、下側、または右側から選べます。
* 複数のフィールドのエラーメッセージを任意の時点で表示できます。
* フィールドが選択されているかどうかに関係なく、エラーを表示します。

## エラーメッセージのカスタマイズ {#customizing-error-messages-nbsp}

エラーメッセージをカスタマイズする前に、添付のパッケージ（CustomErrorManager-1.0-SNAPSHOT.zip）をダウンロードして解凍します。

パッケージを展開したら、 CustomErrorManager-1.0-SNAPSHOT フォルダーを開きます。 jcr_root および META-INF フォルダーが含まれます。 これらのフォルダーには、エラーメッセージのカスタマイズに必要な CSS ファイルと.JS ファイルが含まれています。

[ファイルを入手](assets/customerrormanager-1.0-snapshot.zip)

### エラーメッセージの位置のカスタマイズ  {#customizing-the-position-of-error-messages-nbsp}

エラーメッセージの位置をカスタマイズするには、 &lt;div> タグで、各エラーおよび警告フィールドに対して、 &lt;div> タグを左または右に追加し、 &lt;div> タグを使用します。 詳細な手順については、以下に示す手順を参照してください。

1. `CustomErrorManager-1.0-SNAPSHOT` フォルダーに移動し、`etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` フォルダーを開きます。
1. `customErrorManager.js` ファイルを編集用として開きます。ファイル内の `markError` 関数は、次のパラメーターを受け付けます。

   |   |  |
   |---|---|
   | jqWidget | jqWidget はウィジェットのハンドルです。 |
   | msg | エラーメッセージを格納します |
   | type | エラーか警告かを示します |

1. 標準実装では、フィールドの右側にエラーメッセージが表示されます。 エラーメッセージを上側に表示するには、次のコードを使用します。

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
1. `CustomErrorManager-1.0-SNAPSHOT` フォルダーに移動し、jcr_root フォルダーと META-INF フォルダーのアーカイブを作成します。アーカイブの名前を CustomErrorManager-1.0-SNAPSHOT.zip に変更します。
1. パッケージをアップロードしてインストールするには、パッケージマネージャーを使用します。

## 複数のフィールドのエラーメッセージを表示  {#display-error-messages-for-multiple-fields-nbsp}

添付されたパッケージを使用して、すべてのフィールドのエラーメッセージを同時に表示します。 単一のエラーメッセージを表示するには、デフォルトのプロファイルを使用します。

### エラーメッセージの外観のカスタマイズ。  {#customizing-the-appearance-of-error-messages-nbsp}

1. etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css フォルダーに移動します。

1. sample.css ファイルを開いて編集します。 CSS ファイルには、#customError、#customWarningの 2 つの ID が含まれます。 これらの ID を使用して、色やフォントサイズなどの様々なプロパティを変更できます。

   次のコードを使用して、エラー/警告メッセージのフォントサイズと色を変更します。

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
1. CustomErrorManager-1.0-SNAPSHOT フォルダーに移動し、jcr_root および META-INF フォルダーのアーカイブを作成します。 アーカイブの名前を CustomErrorManager-1.0-SNAPSHOT.zip に変更します。
1. パッケージをアップロードしてインストールするには、パッケージマネージャーを使用します。

## 新しいプロファイルでフォームをレンダリングします。  {#render-the-form-with-the-new-profile-nbsp}

初期設定では、html5 フォームはデフォルトのプロファイルを使用します。 `https://&lt;server&gt;/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

カスタムエラーメッセージを含むフォームを表示するには、次のエラープロファイルを含むフォームをレンダリングします。 `https://&lt;server&gt;/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

>[!NOTE]
>
>エラープロファイルは、添付されているパッケージによりインストールされます。
