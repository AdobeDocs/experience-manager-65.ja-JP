---
title: カスタムツールバーレイアウトの作成
description: フォームのツールバーレイアウトを指定できます。ツールバーレイアウトは、フォーム上のツールバーのコマンドとレイアウトを定義します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 44516956-00aa-41d5-a7e9-746c7618e5db
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 100%

---

# カスタムツールバーレイアウトの作成{#creating-custom-toolbar-layout}

## ツールバーレイアウト {#layout}

アダプティブフォームを作成する際に、フォームのツールバーレイアウトを指定できます。ツールバーレイアウトは、フォーム上のツールバーのコマンドとレイアウトを定義します。

ツールバーレイアウトの使用は、複雑な JavaScript と CSS コードによるクライアントサイドの処理に大きく依存しています。このコードの提供を編成および最適化することが厄介な問題となることがあります。この問題に対処するために、AEM はクライアントサイドライブラリフォルダーを提供しています。これにより、クライアントサイドコードをリポジトリに格納し、カテゴリ別に整理して、それぞれのカテゴリのコードをクライアントに提供するタイミングと方法を定義できます。クライアントサイドのライブラリスステムは、最終的な web ページで正しいコードをロードするための正しいリンクを生成する作業を担当します。詳細については、[AEM におけるクライアントサイドライブラリの機能](/help/sites-developing/clientlibs.md)を参照してください。

![ツールバーのサンプルレイアウト](assets/default_toolbar_layout.png)

ツールバーのサンプルレイアウト

アダプティブフォームには、すぐに使用できる一連のレイアウトが用意されています。

![標準搭載のツールバーレイアウト ](assets/toolbar1.png)

標準搭載のツールバーレイアウト

カスタムのツールバーレイアウトを作成することもできます。

次の手順では、3 つのアクションをツールバーに表示し、その他のアクションをツールバーのドロップダウンリストに表示するカスタムツールバーの作成手順を説明します。

付属のコンテンツパッケージには、以下に示すコード全体が含まれています。コンテンツパッケージをインストールしたら、`/content/forms/af/CustomLayoutDemo.html` を開いてカスタムツールバーレイアウトのデモをご覧ください。

CustomToolbarLayoutDemo.zip

[ファイルの取得](assets/customtoolbarlayoutdemo.zip)
デモカスタムツールバーレイアウト

## カスタムツールバーレイアウトを作成するには {#layout-1}

1. カスタムツールバーレイアウトを保持するフォルダーを作成します。例：

   `/apps/customlayout/toolbar`。

   カスタムレイアウトを作成するには、次のフォルダーに用意されている既成のツールバーレイアウトの 1 つを使用（およびカスタマイズ）できます。

   `/libs/fd/af/layouts/toolbar`

   例えば、`mobileFixedToolbarLayout` ノードを `/libs/fd/af/layouts/toolbar` フォルダーから `/apps/customlayout/toolbar` フォルダーにコピーします。

   toolbarCommon.jsp も `/apps/customlayout/toolbar` フォルダーにコピーします。

   >[!NOTE]
   >
   >カスタムレイアウトを保存するために作成したフォルダーは、`apps` フォルダーで作成されたものでなければなりません。

1. コピーしたノード `mobileFixedToolbarLayout` の名前を `customToolbarLayout.` に変更します。

   また、ノードに関連する説明も入力します。例えば、ノードの jcr:description を&#x200B;**ツールバーのカスタムレイアウト**&#x200B;に変更します。

   ノードの `guideComponentType` プロパティによりレイアウトタイプが決まります。この場合、レイアウトタイプはツールバーなので、ツールバーレイアウト選択ドロップダウンに表示されます。

   ![適切な説明を付けたノード](assets/toolbar3.png)

   適切な説明を付けたノード

   新しいカスタムツールバーレイアウトは、**アダプティブフォームツールバー**&#x200B;ダイアログ設定に表示されます。

   ![使用可能なツールバーレイアウトのリスト](assets/toolbar4.png)

   使用可能なツールバーレイアウトのリスト

   >[!NOTE]
   >
   >前の手順で更新された説明が、レイアウトドロップダウンリストに表示されます。

1. このカスタムツールバーレイアウトを選択し、「OK」をクリックします。

   clientlib（javascript と css）を `/etc/customlayout` ノードに追加し、clientlib の参照を `customToolbarLayout.jsp` に含めます。

   ![customToolbarLayout.css ファイルのパス](assets/toolbar_3.png)

   customToolbarLayout.css ファイルのパス

   サンプル `customToolbarLayout.jsp`：

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <cq:includeClientLib categories="customtoolbarlayout" />
   <c:if test="${isEditMode}">
           <cq:includeClientLib categories="customtoolbarlayoutauthor" />
   </c:if>
   <div class="guidetoolbar mobileToolbar mobilecustomToolbar" data-guide-position-class="guide-element-hide">
       <div data-guide-scroll-indicator="true"></div>
       <%@include file="../toolbarCommon.jsp" %>
   </div>
   ```

   >[!NOTE]
   >
   >レイアウトの guidetoolbar クラスを追加します。ツールバーの標準提供のスタイル設定は、guidetoolbar クラスに基づいて定義されています。

   サンプル `toolBarCommon.jsp`：

   ```jsp
   <%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions"%>
   <%--------------------
   This code iterates over all the tool bar items using the guideToolbar bean.
   If the number of toolbar items are more than 3, then we create a dropdown menu using bootstrap for other actions present in the toolbar.
   In both desktop and mobile devices, the layout is different.
   ---------------------------------%>
   
   <c:forEach items="${guideToolbar.items}" var="toolbarItem" varStatus="loop">
       <c:choose>
         <c:when test="${loop.index gt 2}">
      <c:choose>
       <c:when test="${loop.index eq 3}">
                     <div class="btn-group dropdown">
                       <button type="button" class="btn btn-primary dropdown-toggle label" data-toggle="dropdown">Actions <span class="caret"></code></button>
                       <button type="button" class="btn btn-primary dropdown-toggle icon" data-toggle="dropdown"><span class="glyphicon glyphicon-th-list"></code></button>
             <ul class="dropdown-menu" role="menu">
                           <li>
                               <div id="${toolbarItem.id}_guide-item">
                                 <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                              </div>
                           </li>
                           <c:if test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                                </ul>
                                </div>
                           </c:if>
       </c:when>
       <c:when test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                          <li>
                                     <div id="${toolbarItem.id}_guide-item">
                                         <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                                     </div>
                           </li>
                       </ul>
                     </div>
   
       </c:when>
       <c:otherwise>
         <li>
          <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
          </div>
         </li>
       </c:otherwise>
      </c:choose>
         </c:when>
         <c:otherwise>
     <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
        </div>
         </c:otherwise>
    </c:choose>
   </c:forEach>
   ```

   CSS は clientlib ノード内に存在します。

   ```css
   .mobilecustomToolbar .dropdown {
       display: inline-block;
   }
   
   .mobilecustomToolbar .dropdown {
       float: right;
   }
   
   .mobilecustomToolbar .dropdown > button {
      padding: 6px 12px;
   }
   
   .mobilecustomToolbar .dropdown .guideFieldWidget, .mobilecustomToolbar .dropdown .guideFieldWidget button {
       width: 100%;
   }
   
   .mobilecustomToolbar .dropdown .caret{
       border-bottom: 6px solid;
       border-right: 6px solid transparent;
       border-left: 6px solid transparent;
    border-top: transparent;
   }
   
   .mobilecustomToolbar .dropdown-menu{
    top: auto;
    bottom: 100%;
   }
   
   .mobilecustomToolbar .btn-group {
    vertical-align: super;
   }
   
   .mobilecustomToolbar .glyphicon {
    font-size: 24px;
   }
   
   @media (max-width: 767px){
   
    .mobilecustomToolbar .dropdown .guideButton .iconButton-icon {
      display: none;
       }
   
       .mobilecustomToolbar .dropdown .guideButton .iconButton-label {
      display: inline-block;
       }
   
       .mobilecustomToolbar .dropdown .guideButton button {
      background-color: #013853;
       }
   
    .mobilecustomToolbar .btn-group {
     vertical-align: top;
    }
   
   }
   ```

>[!NOTE]
>
>前の手順で更新された説明が、レイアウトドロップダウンリストに表示されます。

![カスタムレイアウトツールバーのデスクトップビュー](assets/toolbar_1.png)

カスタムレイアウトツールバーのデスクトップビュー
