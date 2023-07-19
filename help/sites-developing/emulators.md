---
title: エミュレーター
seo-title: Emulators
description: AEMを使用すると、作成者は、エンドユーザーがページを表示する環境をシミュレートするエミュレーターでページを表示できます
seo-description: AEM enables authors to view a page in an emulator that simulates the environment in which an end-user will view the page
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 71%

---

# エミュレーター{#emulators}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

Adobe Experience Manager（AEM）では、作成者がエミュレーターでページを確認できます。エミュレーターは、モバイルデバイスやメールクライアントなどでエンドユーザーがページを表示する環境をシミュレートします。

AEM エミュレーターフレームワークの機能を次に示します。

* シミュレートされたユーザーインターフェイス (UI) 内でコンテンツをオーサリングできます。例えば、モバイルデバイスや電子メールクライアント（ニュースレターの作成に使用）などです。
* シミュレートされた UI に従ってページコンテンツを変更します。
* カスタムエミュレーターを作成できます。

>[!CAUTION]
>
>この機能は、クラシック UI でのみサポートされます。

## エミュレーターの特性 {#emulators-characteristics}

エミュレーター：

* ExtJS に基づいています。
* ページ DOM 上で動作します。
* その外観は CSS を使用して制御されます。
* プラグインをサポートします（例えば、モバイルデバイスのローテーションプラグイン）。
* 作成者でのみ有効です。
* 基本コンポーネントは `/libs/wcm/emulator/components/base` にあります。

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
>上の例と同様に、プロジェクトHTMLは、本文コンテンツを 1 つの div 内にラップすることをお勧めします。 本文コンテンツに複数のタグが含まれている場合、予期しない結果が生じる可能性があります。

### モバイルエミュレーター {#mobile-emulators}

既存のモバイルエミュレーターは次のとおりです。

* /libs/wcm/mobile/components/emulators の下にあります。
* 次の場所にある JSON サーブレットを通じて使用できます。

  http://localhost:4502/bin/wcm/mobile/emulators.json

ページコンポーネントでモバイルページコンポーネント（`/libs/wcm/mobile/components/page`）を使用する場合は、次のメカニズムによって、エミュレーターの機能が自動的にページに統合されます。

* モバイルページコンポーネント `head.jsp` は、次のメソッドを使用して、デバイスグループの関連するエミュレーターの init コンポーネント（オーサーモードの場合のみ）とデバイスグループのレンダリング CSS をインクルードします。


  `deviceGroup.drawHead(pageContext);`

* メソッド `DeviceGroup.drawHead(pageContext)` には、エミュレーターの init コンポーネントを含まれています。つまり、エミュレーターコンポーネントの `init.html.jsp` を呼び出します。エミュレーターコンポーネントが独自の `init.html.jsp` を持たず、モバイルベースエミュレーター（`wcm/mobile/components/emulators/base)`）に依存している場合、モバイルベースエミュレーターの init スクリプトが呼び出されます（`/libs/wcm/mobile/components/emulators/base/init.html.jsp`）。

* モバイルベースエミュレーターの init スクリプトは、JavaScript を使用して次のように定義します。

   * ページ用に定義されるすべてのエミュレーターの設定（emulatorConfigs）
   * 次のメソッドを使用してエミュレーターの機能をページに統合するエミュレーターマネージャー。

     `emulatorMgr.launch(config)`

     エミュレーターマネージャーは次のように定義されます。

     `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### カスタムモバイルエミュレーターの作成 {#creating-a-custom-mobile-emulator}

カスタムモバイルエミュレーターを作成するには：

1. `/apps/myapp/components/emulators` の下に、コンポーネント `myemulator`（ノードタイプ：`cq:Component`）を作成します。

1. `sling:resourceSuperType` プロパティを `/libs/wcm/mobile/components/emulators/base` に設定

1. エミュレーターの外観のカテゴリ `cq.wcm.mobile.emulator` を使用して CSS クライアントライブラリを定義します：名前 = `css`、ノードタイプ = `cq:ClientLibrary`

   例として、ノード `/libs/wcm/mobile/components/emulators/iPhone/css` を参照できます。

1. 必要に応じて、JS クライアントライブラリを定義します。例えば、特定のプラグインを定義する場合は、名前 = js、ノードタイプ = cq:ClientLibrary にします。

   例として、ノード `/libs/wcm/mobile/components/emulators/base/js` を参照できます。

1. エミュレーターがプラグインで定義された特定の機能（タッチスクロールなど）をサポートする場合は、エミュレーターの下に、次のように設定ノードを作成します。名前 = `cq:emulatorConfig`、ノードタイプ = `nt:unstructured`。そして、プラグインを定義するプロパティを追加します。

   * 名前 = `canRotate`、タイプ = `Boolean`、値 = `true`：回転機能を含みます。

   * 名前 = `touchScrolling`、タイプ = `Boolean`、値 = `true`：タッチスクロール機能を含みます。

   独自のプラグインを定義することで、さらに多くの機能を追加できます。
