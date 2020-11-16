---
title: エミュレーター
seo-title: エミュレーター
description: AEM では、作成者がエミュレーターでページを確認できます。エミュレーターは、エンドユーザーがページを表示する環境をシミュレートします
seo-description: AEM では、作成者がエミュレーターでページを確認できます。エミュレーターは、エンドユーザーがページを表示する環境をシミュレートします
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 64%

---


# エミュレーター{#emulators}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

Adobe Experience Manager（AEM）では、作成者がエミュレーターでページを確認できます。エミュレーターは、モバイルデバイスや電子メールクライアントなどでエンドユーザーがページを表示する環境をシミュレートします。

AEM エミュレーターフレームワークの機能を次に示します。

* シミュレートされたユーザーインターフェイス（UI）（例：ニュースレターの作成に使用するモバイルデバイスや電子メールクライアント）内でコンテンツを作成できます。
* シミュレートされた UI に従ってページコンテンツを変更します。
* カスタムエミュレーターを作成できます。

>[!CAUTION]
>
>この機能は、クラシック UI でのみサポートされます。

## エミュレーターの特徴 {#emulators-characteristics}

エミュレーターの特徴は次のとおりです。

* ExtJS に基づいています。
* ページの DOM で動作します。
* 外観は CSS によって制御されます。
* プラグイン（例：モバイルデバイスの回転プラグイン）をサポートします。
* オーサーインスタンスでのみアクティブになります。
* Its base component is at `/libs/wcm/emulator/components/base`.

### エミュレーターによるコンテンツの変換方法 {#how-the-emulator-transforms-the-content}

エミュレーターは HTML の本文コンテンツをエミュレーターの DIV にラップすることによって機能します。例えば、次の html コードがあるとします。

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

このコードは、エミュレーターの起動後、次の html コードに変換されます。

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

次の 2 つの div タグが追加されます。

* id が `cq-emulator` の div：エミュレーター全体を保持します。

* id が `cq-emulator-content` の div：ページコンテンツが配置されているデバイスの viewport/screen/content 領域を表します。

また、新しいエミュレーターの div には新しい CSS クラスが割り当てられます。これらのクラスは現在のエミュレーターの名前を表します。

エミュレーターのプラグインは、割り当てられた CSS クラスのリストを拡張できます。回転プラグインの例に示すように、現在のデバイスの回転に応じて「vertical」クラスまたは「horizontal」クラスを挿入します。

この方法では、エミュレーターの div の ID と CSS クラスに対応する CSS クラスを指定することで、エミュレーターのすべての外観を制御できます。

>[!NOTE]
>
>前述の例と同様に、単一の div 内の本文コンテンツをプロジェクトの HTML でラップすることをお勧めします。本文コンテンツに複数のタグが含まれる場合は、予測できない結果が生じる可能性があります。

### モバイルエミュレーター {#mobile-emulators}

既存のモバイルエミュレーターの特徴は次のとおりです。

* /libs/wcm/mobile/components/emulators にあります。
* JSONサーブレットを介して次の場所で使用できます。

   http://localhost:4502/bin/wcm/mobile/emulators.json

When the page component relies on the mobile page component ( `/libs/wcm/mobile/components/page`), the emulator functionality is automatically integrated in the page through the following mechanism:

* モバイルページコンポーネント `head.jsp` は、次のメソッドを使用して、デバイスグループの関連するエミュレーターの init コンポーネント（オーサーモードの場合のみ）とデバイスグループのレンダリング CSS をインクルードします。


   `deviceGroup.drawHead(pageContext);`

* The method `DeviceGroup.drawHead(pageContext)` includes the emulator&#39;s init component, i.e. calls the `init.html.jsp` of the emulator component. エミュレータコンポーネントに独自の機能がなく、モバイルベースエミュレータに依存している場合( `init.html.jsp` 、モバイルベースエミュレータのinitスクリプトは( `wcm/mobile/components/emulators/base)``/libs/wcm/mobile/components/emulators/base/init.html.jsp`)と呼ばれます。

* モバイルベースエミュレーターのinitスクリプトは、JavaScriptを使用して定義します。

   * ページ用に定義されるすべてのエミュレーターの設定（emulatorConfigs）
   * ページ内のエミュレーターの機能を次の手順に従って統合するエミュレーターマネージャー。

      `emulatorMgr.launch(config)`;

      エミュレータマネージャは次の方法で定義します。

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### カスタムモバイルエミュレーターの作成 {#creating-a-custom-mobile-emulator}

カスタムモバイルエミュレーターを作成するには：

1. 次に、コンポーネントを `/apps/myapp/components/emulators` 作成し `myemulator` ます(ノードタイプ： `cq:Component`)をクリックします。

1. Set the `sling:resourceSuperType` property to `/libs/wcm/mobile/components/emulators/base`

1. エミュレーターの外観を表すカテゴリを持つCSSクライアントライブラリ `cq.wcm.mobile.emulator` を定義します。name = `css`、ノードタイプ= `cq:ClientLibrary`

   As an example, you can refer to the node `/libs/wcm/mobile/components/emulators/iPhone/css`

1. 必要に応じて、JSクライアントライブラリを定義します。例えば、次のような特定のプラグインを定義します。name = js、node type = cq:ClientLibrary

   As an example, you can refer to the node `/libs/wcm/mobile/components/emulators/base/js`

1. エミュレーターがプラグインで定義される特定の機能（タッチスクロールなど）をサポートしている場合は、エミュレーターの下に設定ノードを作成します。name = `cq:emulatorConfig`、node type = `nt:unstructured` 、pluginを定義するプロパティを追加します。

   * Name = `canRotate`, Type = `Boolean`, Value = `true`:をクリックして回転機能を追加します。

   * Name = `touchScrolling`, Type = `Boolean`, Value = `true`:をクリックして、タッチスクロール機能を含めます。

   独自のプラグインを定義することで、さらに多くの機能を追加できます。

