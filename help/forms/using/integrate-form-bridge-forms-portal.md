---
title: Form Bridge と HTML5 フォームのカスタムポータルの統合
seo-title: Form Bridge と HTML5 フォームのカスタムポータルの統合
description: FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定できます。
seo-description: FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定できます。
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Form Bridge と HTML5 フォームのカスタムポータルの統合{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge はフォームとのやりとりを可能にする HTML5 フォームのブリッジ API です。For the FormBridge API reference, see [FormBridge API reference](/help/forms/using/form-bridge-apis.md).

FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定できます。たとえば、API を使用してウィザードのような経験を築くことができます。

既存の HTML アプリケーションは FormBridge API を利用してフォームとやりとりし、それを HTML ページに埋め込むことができます。次の手順を使用して、Form Bridge API を使用してフィールドの値を設定できます。

## HTML5 フォームと Web ページの統合 {#integrating-html-forms-to-a-web-page}

1. **プロファイルの選択またはプロファイルの作成**

   1. In the CRX DE interface, navigate to: `https://'[server]:[port]'/crx/de`.
   1. 管理者の資格情報を使用してログインします。
   1. プロファイルを作成するか、既存のプロファイルを選択します。

      For details on how to create a profile, see [Creating a new Profile](/help/forms/using/custom-profile.md).

1. **HTML プロファイルの変更**

   XFA ランタイム、XFA ロケールライブラリ、および XFA フォーム HTML スニペットをプロファイルレンダラーに含めた後、Web ページをデザインして、フォームを Web ページ内に配置します。

   たとえば、次のコードスニペットを使用して、2 つの入力フィールドとフォームのあるアプリを作成し、フォームと外部アプリの間でのやり取りを示します。

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
   >The **line 9**, contains additional JSP reference for CSS styles and JavaScript files to design the page.
   >
   >
   >**18 行目**&#x200B;の &lt;div id=&quot;rightdiv&quot;> タグには XFA フォームの HTML スニペットが含まれています。
   ページは 2 つのコンテナ、**left** と **right** にスタイル設定されています。right コンテナにはフォームがあります。left コンテナには 2 つの入力フィールドと外部 HTML ページの一部があります。
   次のスクリーンショットは、フォームがどのようにブラウザーで表示されるかを示しています。

   ![ポータル](assets/portal.jpg)

   左側は **HTML ページ**&#x200B;の一部です。右側でフィールドを含んでいるのは **xfa フォーム**&#x200B;です。

1. **ページからのフォームフィールドへのアクセス**

   次にあるのは、フォームフィールドの値を設定するために追加できるサンプルのスクリプトです。

   For example, if you want to set the **EmployeeName** using the values in the Fields **First Name** and **Last Name**, call the **window.formBridge.setFieldValue** function.

   Similarly, you can read the value by calling **window.formBridge.getFieldValue** API.

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
