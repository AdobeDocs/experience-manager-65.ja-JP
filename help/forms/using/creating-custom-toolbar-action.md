---
title: カスタムツールバーアクションの作成
description: フォーム開発者は、AEM Forms のアダプティブフォーム用にカスタムツールバーアクションを作成できます。カスタムアクションフォームを使用して、作成者はより多くのワークフローとオプションをエンドユーザーに提供できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 17f7f0e1-09d8-45cd-a4f6-0846bdb079b6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 100%

---

# カスタムツールバーアクションの作成{#creating-a-custom-toolbar-action}

## 前提条件 {#prerequisite}

カスタムツールバーアクションを作成する前に、[クライアント側のライブラリを使用する方法](/help/sites-developing/clientlibs.md)と [CRXDE Lite を使用した開発](/help/sites-developing/developing-with-crxde-lite.md)を参照して理解を深めてください。

## アクションとは {#what-is-an-action-br}

アダプティブフォームは、フォーム作成者がオプションの組み合わせを設定できるツールバーを提供します。これらのオプションは、アダプティブフォームのアクションとして定義されます。パネルのツールバーの「編集」ボタンをクリックして、アダプティブフォームがサポートするアクションを設定します。

![デフォルトのツールバーアクション](assets/default_toolbar_actions.png)

デフォルトで提供される一連のアクションに加え、カスタムアクションをツールバーに作成することができます。例えば、アクションを追加することで、フォームを送信する前にアダプティブフォームのすべてのフィールドを、ユーザーがレビューできるようにすることが可能です。

## アダプティブフォームでカスタムアクションを作成する手順 {#steps}

カスタムのツールバーアクションを作成するには、次の手順を実行して、記入の済んだフォームを送信する前にアダプティブフォームのすべてのフィールドをエンドユーザーがレビューするためのボタンを作成します。

1. アダプティブフォームでサポートされているデフォルトのアクションは、すべて `/libs/fd/af/components/actions` フォルダーにあります。CRXDE で、`fileattachmentlisting` ノードを `/libs/fd/af/components/actions/fileattachmentlisting` から `/apps/customaction` にコピーします。

1. `apps/customaction` フォルダーにノードをコピーしたら、ノードの名前を `reviewbeforesubmit` に変更します。このノードの `jcr:title` と `jcr:description` のプロパティも変更します。

   `jcr:title` プロパティには、ツールバーダイアログに表示されるアクションの名前が含まれています。`jcr:description` プロパティには、アクションにマウスオーバーしたときに表示される詳細情報が含まれます。

   ![ツールバーのカスタマイズに使用するノードの階層](assets/action3.png)

1. `reviewbeforesubmit` ノード内の `cq:template` ノードを選択します。`guideNodeClass` プロパティの値が `guideButton` となっていることを確認し、それに合わせて `jcr:title` プロパティを変更します。
1. `cq:Template` ノードの type プロパティを変更します。この例では、タイプのプロパティをボタンに変更します。

   このコンポーネントで、生成された HTML に type の値が CSS クラスとして追加されます。ユーザーはこの CSS クラスを使用して、アクションのスタイルを設定できます。ボタン、送信、リセット、保存の各 type 値には、モバイルデバイスとデスクトップデバイスの両方に対応するデフォルトのスタイルが用意されています。

1. アダプティブフォームを編集するツールバーのダイアログから、カスタムアクションを選択します。パネルのツールバーに「レビュー」ボタンが表示されます。

   ![カスタムアクションはツールバーで使用できます](assets/custom_action_available_in_toolbar.png) ![カスタムで作成したツールバーアクションの表示](assets/action7.png)

1. 「レビュー」ボタンに機能を持たせるには、`reviewbeforesubmit` ノードにある init.jsp ファイルに JavaScript、CSS コード、およびサーバーサイドのコードを追加します。

   `init.jsp` に次のコードを追加します。

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <guide:initializeBean name="guideField" className="com.adobe.aemds.guide.common.GuideButton"/>
   
   <c:if test="${not isEditMode}">
           <cq:includeClientLib categories="reviewsubmitclientlibruntime" />
   </c:if>
   
   <%--- BootStrap Modal Dialog  --------------%>
   <div class="modal fade" id="reviewSubmit" tabindex="-1">
       <div class="modal-dialog">
           <div class="modal-content">
               <div class="modal-header">
                   <h3>Review the Form Fields</h3>
               </div>
               <div class="modal-body">
                   <div class="modal-list">
                       <table class="table table-bordered">
                           <tr class="name">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Name is: </label>
                               </td>
                           </tr>
                           <tr class="pan">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Pan Number is: </label>
                               </td>
                           </tr>
                           <tr class="dob">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Date Of Birth is: </label>
                               </td>
                           </tr>
                           <tr class="80cdeclaration">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total 80C Declaration Amount is: </label>
                               </td>
                           </tr>
                           <tr class="rentpaid">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total HRA Amount is: </label>
                               </td>
                           </tr>
                       </table>
                   </div>
               </div><!-- /.modal-body -->
               <div class="modal-footer">
                   <div class="fileAttachmentListingCloseButton col-md-2 col-xs-2 col-sm-2">
                       <button data-dismiss="modal">Close</button>
                   </div>
               </div>
           </div><!-- /.modal-content -->
       </div><!-- /.modal-dialog -->
   </div><!-- /.modal -->
   ```

   `ReviewBeforeSubmit.js` ファイルに次のコードを追加します。

   ```javascript
   /*anonymous function to handle show of review before submit view */
   $(function () {
       if($("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").length > 0) {
           $("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").click(function(){
               // Create the options object to be passed to the getElementProperty API
               var options = {},
                   result = [];
               options.somExpressions = [];
               options.propertyName = "value";
               guideBridge.visit(function(model){
                   if(model.name === "name" || model.name === "pan" || model.name === "dateofbirth" || model.name === "total" || model.name === "totalmonthlyrent"){
                           options.somExpressions.push(model.somExpression);
                   }
               }, this);
               result = guideBridge.getElementProperty(options);
   
               $('#reviewSubmit .reviewlabel').each(function(index, item){
                   var data = ((result.data[index] == null) ? "No Data Filled" : result.data[index]);
                   if($(this).next().hasClass("reviewlabelvalue")){
                       $(this).next().html(data);
                   } else {
                       $(this).after($("<td></td>").addClass("reviewlabelvalue col-md-6 active").html(data));
                   }
               });
               // added because in mobile devices it was causing problem of backdrop
               $("#reviewSubmit").appendTo('body');
               $("#reviewSubmit").modal("show");
           });
       }
   });
   ```

   `ReviewBeforeSubmit.css` ファイルに次のコードを追加します。

   ```css
   .modal-list .reviewlabel {
       white-space: normal;
       text-align: right;
       padding:2px;
   }
   
   .modal-list .reviewlabelvalue {
       border: #cde0ec 1px solid;
       padding:2px;
   }
   
   /* Adding icon for this action in mobile devices */
   /* This is the glyphicon provided by bootstrap eye-open */
   /* .<type> .iconButton-icon */
   .reviewbeforesubmit .iconButton-icon {
       position: relative;
       top: -8px;
       font-family: 'Glyphicons Halflings';
       font-style: normal;
   }
   
   .reviewbeforesubmit .iconButton-icon:before {
       content: "\e105"
   }
   ```

1. カスタムアクションの機能を検証するには、プレビューモードでアダプティブフォームを開いて、ツールバーの「レビュー」ボタンをクリックします。

   >[!NOTE]
   >
   >オーサリングモードでは `GuideBridge` ライブラリは読み込まれません。そのため、オーサリングモードではこのカスタムアクションは動作しません。

   ![カスタムレビューボタンのアクションのデモ](assets/action9.png)

## サンプル {#samples}

コンテンツパッケージは次のアーカイブにあります。このパッケージには、上記のカスタムツールバーアクションのデモに関連するアダプティブフォームが含まれています。

[ファイルを取得](assets/customtoolbaractiondemo.zip)
