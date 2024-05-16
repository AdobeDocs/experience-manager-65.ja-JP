---
title: アダプティブフォームのセットを使用したアダプティブフォームの作成
description: AEM Forms では、アダプティブフォームを統合して 1 つの大きなアダプティブフォームを作成し、その機能を理解することができます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 4254c2cb-66cc-4a46-b447-bc5e32def7a0
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '620'
ht-degree: 100%

---

# アダプティブフォームのセットを使用したアダプティブフォームの作成{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

## 概要 {#overview}

銀行口座の開設の申し込みなどのワークフローでは、ユーザーは複数のフォームに記入します。一連のフォームに記入してもらう代わりに、フォームを積み重ねて大きなフォーム（親フォーム）を作成できます。大きなフォームにアダプティブフォームを追加すると、パネル（子フォーム）として追加されます。一連の子フォームを追加して、親フォームを作成します。ユーザーの入力に基づいて、パネルの表示と非表示を切り替えることができます。親フォームのボタン（送信やリセットなど）は、子フォームのボタンを上書きします。親フォームにアダプティブフォームを追加するには、アダプティブフォームを（アダプティブフォームフラグメントと同様に）アセットブラウザーからドラッグ＆ドロップします。

使用できる機能は、次のとおりです。

* 独立オーサリング
* 適切なフォームの表示／非表示
* 遅延読み込み

独立オーサリングや遅延読み込みなどの機能を使用すると、個々のコンポーネントを使用して親フォームを作成する場合のパフォーマンスが向上します。

>[!NOTE]
>
>XFA ベースのアダプティブフォームやフラグメントは、子フォームまたは親フォームとして使用することはできません。

## 機能の仕組み {#behind-the-scenes}

親フォームに XSD ベースのアダプティブフォームとフラグメントを追加できます。親フォームの構造は[任意のアダプティブフォーム](../../forms/using/prepopulate-adaptive-form-fields.md)と同様です。アダプティブフォームを子フォームとして追加すると、親フォームのパネルとして追加されます。バインドされた子フォームのデータは、親フォームの XML スキーマの `afBoundData` セクションの `data` ルートに保存されます。

例えば、顧客がアプリケーションフォームに入力するとします。フォームの最初の 2 つのフィールドは、名前と ID です。XML は次のようになります。

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

顧客がオフィスの住所を入力できるフォームをアプリケーションに追加します。子フォームのスキーマのルートは `officeAddress` です。`bindref`、`/application/officeAddress` または `/officeAddress` を適用します。`bindref` がない場合、子フォームが `officeAddress` サブツリーとして追加されます。以下のフォームの XML を参照してください。

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

顧客が住所を入力できる別のフォームを挿入する場合は、`bindref` `/application/houseAddress or /houseAddress.`を適用すると、XML は次のようになります。

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

スキーマのルートと同じサブルート名にするには、（この例では`Address` ）、インデックス付きの bindref を使用します。

例えば、bindref `/application/address[1]` または `/address[1]` および `/application/address[2]` または `/address[2]` を適用します。このフォームの XML は、以下のようになります。

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

`bindRef` プロパティを使用して、フォームまたはフラグメントのデフォルトサブツリーを変更することができます。`bindRef` プロパティにより、XML スキーマのツリー構造における位置を示すパスを指定できます。

バインドされていない子フォームのデータは、親フォームの XML スキーマの `afUnboundData` セクションの `data` ルートに保存されます。

アダプティブフォームを子フォームとして、複数回追加できます。`bindRef` が正しく修正されて、アダプティブフォームの各使用済みインスタンスが、データルート上で異なるサブルートを指定するようにします。

>[!NOTE]
>
>異なるフォームやフラグメントが同じサブルートにマッピングされている場合、データは上書きされます。

## アセットブラウザーを使用した子フォームとしてのアダプティブフォームの追加 {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

アセットブラウザーを使用してアダプティブフォームを子フォームとして追加するには、次の手順を実行します。

1. 親フォームを編集モードで開きます。
1. サイドバーで、**アセット**／![アセットブラウザー](assets/assets-browser.png)をクリックします。アセットの下で、**アダプティブフォーム** をドロップダウンリストから選択します。
   [![アセットでアダプティブフォームを選択する](assets/asset.png)](assets/asset-1.png)

1. 子フォームとして追加するアダプティブフォームをドラッグ＆ドロップします。
   [![サイトにアダプティブフォームをドラッグ＆ドロップ](assets/drag-drop.png)](assets/drag-drop-1.png)ドロップしたアダプティブフォームは、子フォームとして追加されます。
