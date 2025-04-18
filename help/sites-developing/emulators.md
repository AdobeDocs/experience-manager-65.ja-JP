---
title: エミュレーター
description: AEM では、作成者がエミュレーターでページを表示できます。エミュレーターは、エンドユーザーがページを表示する環境をシミュレートします。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: ht
source-wordcount: '609'
ht-degree: 100%

---

# エミュレーター{#emulators}

{{ue-over-mobile}}

Adobe Experience Manager（AEM）では、作成者がエミュレーターでページを表示できます。エミュレーターは、モバイルデバイスやメールクライアントなどでエンドユーザーがページを表示する環境をシミュレートします。

AEM エミュレーターフレームワークの機能を次に示します。

* シミュレートされたユーザーインターフェイス（UI）（例：ニュースレターの作成に使用するモバイルデバイスやメールクライアント）内でコンテンツのオーサリング機能を提供します。
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
>前述の例と同様に、単一の div 内の本文コンテンツをプロジェクトの HTML でラップすることをお勧めします。本文コンテンツに複数のタグが含まれる場合は、予測できない結果が生じる可能性があります。

### モバイルエミュレーター {#mobile-emulators}

既存のモバイルエミュレーターの特徴は次のとおりです。

* /libs/wcm/mobile/components/emulators にあります。
* 次の場所にある JSON サーブレットを通じて使用できます。

  http://localhost:4502/bin/wcm/mobile/emulators.json

ページコンポーネントでモバイルページコンポーネント（`/libs/wcm/mobile/components/page`）を使用する場合は、次のメカニズムによって、エミュレーターの機能が自動的にページに統合されます。

* モバイルページコンポーネント `head.jsp` は、次のメソッドを使用して、デバイスグループの関連するエミュレーターの init コンポーネント（オーサーモードの場合のみ）とデバイスグループのレンダリング CSS をインクルードします。


  `deviceGroup.drawHead(pageContext);`

* メソッド `DeviceGroup.drawHead(pageContext)` には、エミュレーターの init コンポーネントを含まれ、エミュレーターコンポーネントの `init.html.jsp` を呼び出します。エミュレーターコンポーネントが独自の `init.html.jsp` を持たず、モバイルベースエミュレーター（`wcm/mobile/components/emulators/base)`）に依存している場合、モバイルベースエミュレーターの init スクリプトが呼び出されます（`/libs/wcm/mobile/components/emulators/base/init.html.jsp`）。

* モバイルベースエミュレーターの init スクリプトは JavaScript を使用して次の定義を行います。

   * ページ用に定義されるすべてのエミュレーターの設定（emulatorConfigs）
   * 次のメソッドを使用してエミュレーターの機能をページに統合するエミュレーターマネージャー。

     `emulatorMgr.launch(config)`

     エミュレーターマネージャーは次のように定義されます。

     `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### カスタムモバイルエミュレーターの作成 {#creating-a-custom-mobile-emulator}

カスタムモバイルエミュレーターを作成するには、次の手順に従います。

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
