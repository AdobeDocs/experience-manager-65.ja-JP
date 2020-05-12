---
title: アダプティブフォームでの SOM 式の使用
seo-title: アダプティブフォームでの SOM 式の使用
description: アダプティブフォームのパネルで SOM 式を抽出する方法を学びます。
seo-description: アダプティブフォームのパネルで SOM 式を抽出する方法を学びます。
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
translation-type: tm+mt
source-git-commit: 6b4bc58efd72900c54cb245878239e345d72ae3e
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 91%

---


# アダプティブフォームでの SOM 式の使用{#using-som-expressions-in-adaptive-forms}

アダプティブフォームは AEM ページとしてモデル化され、AEM リポジトリで JCR コンテンツ構造で表示されます。コンテンツ構造のキー要素は guideContainer ノードです。guideContainer の下にある rootPanel にはネストされたパネルやフィールドが含まれる場合があります。

Scripting Object Model（SOM）を使用し、特定の Document Object Model（DOM）内の値、プロパティ、メソッドを参照できます。DOM はメモリのオブジェクトとプロパティをツリー階層で編成します。SOM 式はフィールド／描画の要素とパネルを参照します。

次の画像は、コンポーネントをフォームに追加する際にアダプティブフォームが変換するノード構造を示しています。 例えば、パネルをルートパネルに追加し、実行時に DOM に変換されるパネルにラジオボタンを追加できます。The SOM Expression for the radio-button field in adaptive form is specified as `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![DOM ツリー](assets/hierarchy.png)

DOM ツリー

アダプティブフォーム内のすべての要素の SOM 式には、`guide[0].guide1[0]` ] というプレフィックスが付けられます。ノード構造階層のコンポーネントの場所は SOM 式の派生に使用されます。

![2 つのラジオボタンを持つ DOM ツリー](assets/hierarchy_radio_button.png)

2 つのラジオボタンを持つ DOM ツリー

アダプティブフォームでラジオボタンの位置を変更すると、SOM 式が変更されます。オーサリングモードでは、「SOM 式を表示」オプションを使用して AEM Forms 内のフィールドや要素の SOM 式を表示できます。このオプションはフィールドや要素を右クリックするとパネル上に表示されます。

![アダプティブフォームでの SOM 式の抽出](assets/som-expressions.png)

アダプティブフォームでの SOM 式の抽出

パネル内では、この機能にパネルツールバーからアクセスできます。この機能はアダプティブフォーム作成者のスクリプティングを促進します。 

![パネルツールバーを使用した SOM 式の抽出](assets/som-expression.png)

パネルツールバーを使用した SOM 式の抽出

[GuideBridge](https://helpx.adobe.com/jp/aem-forms/6/javascript-api/GuideBridge.html) に一覧表示されている API の一部は要素の SOM 式を使用します。例えば、アダプティブフォーム内の特定のフィールドにフォーカスを移動するには、対応する SOM 式を `getFocus` の `guideBridge` API に渡します。 

