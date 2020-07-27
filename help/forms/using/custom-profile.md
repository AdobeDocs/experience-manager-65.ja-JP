---
title: HTML5 フォームのカスタムプロファイルの作成
seo-title: HTML5 フォームのカスタムプロファイルの作成
description: HTML5 フォームプロファイルは Apache Sling のリソースノードです。それは HTML5 forms Render サービスのカスタマイズされたバージョンを表します。
seo-description: HTML5 フォームプロファイルは Apache Sling のリソースノードです。それは HTML5 forms Render サービスのカスタマイズされたバージョンを表します。
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 59%

---


# HTML5 フォームのカスタムプロファイルの作成 {#creating-a-custom-profile-for-html-forms}

A profile is a resource node in [Apache Sling](https://sling.apache.org/). HTML5フォームレンダリングサービスのカスタムバージョンを表します。 HTML5フォームレンダリングサービスを使用して、HTML5フォームの外観、動作、およびやりとりをカスタマイズできます。 A profile node exists in the `/content` folder in the JCR repository. You can place the node directly under the `/content` folder or any subfolder of the `/content` folder.

Profile ノードには **xfaforms/profile** のデフォルト値を持つ **sling:resourceSuperType**&#x200B;プロパティがあります。ノードのレンダリングスクリプトは/libs/xfaforms/プロファイルにあります。

Sling スクリプトは JSP スクリプトです。JSP スクリプトは要求されたフォームと必要な JS / CSS アーティファクトの HTML を組み立てるためのコンテナとして機能します。These Sling scripts are also referred as **Profile Renderer scripts**. 

GETおよびPOST要求のプロファイルスクリプトは、html.jspとhtml.POST.jspにあります。 これらのファイルをコピーして変更することで、上書きして独自のカスタマイズを追加できます。インプレースで変更を行わないでください。パッチの更新によって、このような変更が上書きされます。

プロファイルにはさまざまなモジュールが含まれています。これらのモジュールは、formRuntime.jsp、config.jsp、toolbar.jsp、formBody.jsp、nav_footer.jsp、および footer.jsp です。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jspモジュールには、クライアントライブラリの参照が含まれています。 これは、リクエストからロケール情報を抽出したし、ローカライズしたメッセージをリクエストに含めるなどのための方法も示します。formRuntime.jspには、独自のcustomJavaScriptライブラリまたはスタイルを含めることができます。

## config.jsp {#config-jsp}

config.jsp モジュールには、ロギング、プロキシサービス、動作バージョンなど、さまあまな設定が含まれています。独自の設定およびウィジェットカスタマイズを config.jsp モジュールに追加することができます。config.jspモジュールにカスタムウィジェット登録などの設定を追加することもできます。

## toolbar.jsp {#toolbar-jsp}

toolbar.jspには、色付きのツールバーを作成するコードが含まれています。 ツールバーを削除するには、toolbar.jsp を HTML.jsp から削除します。

## formBody.jsp {#formbody-jsp}

formBody.jspモジュールは、XFAフォームのHTML表現用です。

## nav_footer.jsp {#nav-footer-jsp}

最初に、HTML5 フォームはフォームの最初のページのみをレンダリングします。ユーザーがフォームをスクロールすると、フォームの残りの部分がロードされます。こうすることでロード体験が高速になります。nav_footer.jsp コンポーネントには、すべてのスタイルとスクロール時のページのロードを支援するために必要なエレメントが含まれます。 

## footer.jsp {#footer-jsp}

footer.jsp モジュールは空です。ユーザーの操作にのみ使用するスクリプトを追加できます。

## カスタムプロファイルの作成 {#creating-custom-profiles}

カスタムプロファイルを作成するには、次の手順を実行します。

### プロファイルノードの作成 {#create-profile-node}

1. Navigate to the CRX DE interface at the URL: `https://'[server]:[port]'/crx/de` and log in to the interface with administrator credentials.

1. 左のペインで */content/xfaforms/profiles* の場所に移動します。

1. default ノードをコピーし、*hrform* という名前で別のフォルダー (*/content/profiles*) にそのノードをペーストします。

1. 新しいノード、*hrform* を選択し、*hrform/demo* の値を持つ文字列プロパティ *sling:resourceType* を追加します。

1. ツールバーメニューで「すべて保存」をクリックして、変更を保存します。

### プロファイルレンダラースクリプトを作成する {#create-the-profile-renderer-script}

カスタムプロファイルの作成後、このプロファイルにレンダラーの情報を追加します。新しいプロファイルの要求を受け取る際に、CRX はレンダリングする JSP ページの /apps フォルダーの存在を確認します。JSP ページを /apps フォルダーで作成します。

1. In the left pane, navigate to the `/apps` folder.
1. Right-click on the `/apps` folder and choose to create a folder with name **hrform**.
1. Insider the **hrform** folder create a folder named **demo**.
1. 「**すべて保存**」ボタンをクリックします。
1. Navigate to `/libs/xfaforms/profile/html.jsp` and copy the node **html.jsp**.
1. Paste **html.jsp** node into the `/apps/hrform/demo` folder created above with same name **html.jsp** and click **Save**.
1. プロファイルスクリプトのその他のコンポーネントを持っている場合は、手順 1 から 6 に従って、/apps/hrform/demo フォルダーにそのコンポーネントをコピーします。

1. To verify that th profile is created, open URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

フォームを検証するには、ローカルファイルシステムから AEM Forms に[フォームを読み込み](/help/forms/using/get-xdp-pdf-documents-aem.md)、AEM サーバーオーサーインスタンスで[フォームをプレビュー](/help/forms/using/previewing-forms.md)します。
