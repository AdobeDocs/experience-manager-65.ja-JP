---
title: Form Bridge と HTML5 フォームのカスタムポータルの統合
seo-title: Integrating Form Bridge with custom portal for HTML5 forms
description: FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定できます。
seo-description: You can use the FormBridge API to get or set the values of form fields from the HTML page and submit the form.
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
feature: Mobile Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 100%

---

# Form Bridge と HTML5 フォームのカスタムポータルの統合{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge はフォームとのやりとりを可能にする HTML5 フォームのブリッジ API です。FormBridge API リファレンスについては、[FormBridge API リファレンス](/help/forms/using/form-bridge-apis.md)を参照してください。

FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定できます。たとえば、API を使用してウィザードのような経験を築くことができます。

既存の HTML アプリケーションは FormBridge API を利用してフォームとやりとりし、それを HTML ページに埋め込むことができます。次の手順を使用して、Form Bridge API を使用してフィールドの値を設定できます。

## HTML5 フォームと Web ページの統合 {#integrating-html-forms-to-a-web-page}

1. **プロファイルの選択またはプロファイルの作成**

   1. CRX DE インターフェイスで、`https://'[server]:[port]'/crx/de` に移動します。
   1. 管理者の資格情報を使用してログインします。
   1. プロファイルを作成するか、既存のプロファイルを選択します。

      プロファイルの作成方法について詳しくは、[新しいプロファイルの作成](/help/forms/using/custom-profile.md)を参照してください。

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
   >**9 行目**&#x200B;には、このページをデザインするための、CSS スタイルと JavaScript ファイルの追加 JSP 参照が含まれています。
   >
   >
   >**18 行目**&#x200B;の &lt;div id=&quot;rightdiv&quot;> タグには XFA フォームの HTML スニペットが含まれています。
   >ページは 2 つのコンテナ、**left** と **right** にスタイル設定されています。right コンテナにはフォームがあります。left コンテナには 2 つの入力フィールドと外部 HTML ページの一部があります。
   >次のスクリーンショットは、フォームがどのようにブラウザーで表示されるかを示しています。

   ![ポータル](assets/portal.jpg)

   左側は **HTML ページ**&#x200B;の一部です。右側でフィールドを含んでいるのは **xfa フォーム**&#x200B;です。

1. **ページからのフォームフィールドへのアクセス**

   次にあるのは、フォームフィールドの値を設定するために追加できるサンプルのスクリプトです。

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
