---
title: Form Bridge と HTML5 フォームのカスタムポータルの統合
description: FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定し、フォームを送信できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '393'
ht-degree: 100%

---

# Form Bridge と HTML5 フォームのカスタムポータルの統合{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge は、フォームの操作を可能にする HTML5 forms ブリッジ API です。FormBridge API リファレンスについては、[FormBridge API リファレンス](/help/forms/using/form-bridge-apis.md)を参照してください。

FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定し、フォームを送信できます。例えば、API を使用してウィザードのようなエクスペリエンスを作成できます。

既存の HTML アプリケーションは、FormBridge API を使用してフォームを操作し、HTML ページに埋め込むことができます。次の手順で、Form Bridge API を使用してフィールドの値を設定できます。

## HTML5 フォームと web ページの統合 {#integrating-html-forms-to-a-web-page}

1. **プロファイルの選択またはプロファイルの作成**

   1. CRX DE インターフェイスで、`https://'[server]:[port]'/crx/de` に移動します。
   1. 管理者の資格情報でログインします。
   1. プロファイルを作成するか、既存のプロファイルを選択します。

      プロファイルの作成方法について詳しくは、[プロファイルの作成](/help/forms/using/custom-profile.md)を参照してください。

1. **HTML プロファイルを変更**

   XFA ランタイム、XFA ロケールライブラリ、および XFA フォーム HTML スニペットをプロファイルレンダラーに含め、web ページをデザインし、フォームを web ページ内に配置します。

   例えば、次のコードスニペットを使用して、2 つの入力フィールドとフォームを含むアプリを作成し、フォームと外部アプリの間のインタラクションを示します。

   ```xml
   <%@ page session="false"
                  contentType="text/html; charset=utf-8"%><%
   %><%@ taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
   %><!DOCTYPE html>
   <html manifest="${param.offlineSpec}">
       <head>
          <cq:include script="formRuntime.jsp"/>
           <!-- Portal Scripts and Styles -->
          <cq:include script="portalheader.jsp"/>
       </head>
       <body>
           <div id="leftdiv" >
               <div id="leftdivcontentarea">
                   <!-- Portal Body -->
                 <cq:include script="portalbody.jsp"/>
               </div>
           </div>
           <div id="rightdiv">
               <div id="formBody">
               <cq:include script="config.jsp"/>
               <!-- Form body -->
               <cq:include script="formBody.jsp"/>
               <!  --To assist in page transitions -- add navigation, based on scrolling -->
               <cq:include  script="../nav/scroll/nav_footer.jsp"/>
               <cq:include script="footer.jsp"/>
               </div>
           </div>
       </body>
   </html>
   ```

   >[!NOTE]
   >
   >**9 行目**&#x200B;には、このページをデザインするための、CSS スタイルと JavaScript ファイルの追加 JSP 参照が含まれています。
   >
   >
   >**18 行目**&#x200B;の &lt;div id=&quot;rightdiv&quot;> タグには XFA フォームの HTML スニペットが含まれています。
   >
   >
   ページは 2 つのコンテナ、**left** と **right** にスタイル設定されます。right コンテナにはフォームがあります。left コンテナには 2 つの入力フィールドと外部 HTML ページの一部があります。
   >
   >
   次のスクリーンショットは、フォームがブラウザーでどのように表示されるかを示します。

   ![ポータル](assets/portal.jpg)

   左側は **HTML ページ**&#x200B;の一部です。右側でフィールドを含んでいるのは **xfa フォーム**&#x200B;です。

1. **ページからのフォームフィールドへのアクセス**

   以下は、フォームフィールドに値を設定する際に追加できるサンプルスクリプトです。

   たとえば、「**名前 (名)**」と「**名前 (姓)**」のフィールドにある値を使用して **EmployeeName**&#x200B;を設定する場合、**window.formBridge.setFieldValue** 関数を呼び出します。

   同様に、**window.formBridge.getFieldValue** API を呼び出すことで値を読み取れます。

   ```javascript
   $(function() {
               $(".input").blur(function() {
                   window.formBridge.setFieldValue(
                               'xfa.form.form1.#subform[0].EmployeeName',
                                $("#lname").val()+' '+$("#fname").val()
                              )
                   });
           });
   ```
