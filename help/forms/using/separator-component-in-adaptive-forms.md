---
title: アダプティブフォームにおけるセパレータコンポーネント
description: セパレーターコンポーネントを使用して、フォームのセクションを視覚的に区別することができます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 100%

---

# アダプティブフォームにおけるセパレータコンポーネント{#separator-component-in-adaptive-forms}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

セパレータコンポーネントを使用して、フォームのパネルを視覚的に区別できます。セパレータコンポーネントの全体的な外観やスタイルは、次のようなセパレータコンポーネントのプロパティを指定して定義できます。

* **要素名**：コンポーネント名を指定します。SOM 式は、要素名フィールドで指定された値を持つコンポーネントに対応しています。
* **太さ：**&#x200B;セパレーターコンポーネントの太さをピクセル単位で指定します。

* **CSS クラス：**&#x200B;セパレーターコンポーネントに対しカスタム CSS クラスを指定します。

* **インラインスタイル：** AEM Forms では、インライン CSS スタイルをアダプティブフォームの各コンポーネントに適用し、変更のプレビューをリアルタイムでプレビューできるようになりました。

レイアウトモードを使用して、セパレーターコンポーネントがまたがる列数を定義できます。詳しくは、[レイアウトモードを使用したコンポーネントのサイズ変更](../../forms/using/resize-using-layout-mode.md)を参照してください。

セパレータコンポーネントのプロパティを指定するには：

1. セパレータコンポーネントを選択して、![cmppr](assets/cmppr.png) を選択します。プロパティがサイドバーで開きます。
1. 「インライン CSS プロパティ」セクションでタブをクリックし、CSS プロパティを指定します。例えば、「フィールド」タブで「**アイテムの追加**」をクリックします。2 つのフィールドを持った行が追加されます。
1. 左から最初のフィールドで、適用したい CSS3 プロパティを指定します。例えば、**ボーダー**&#x200B;を指定します。下矢印をクリックしてプロパティを選択することもできます。ドロップダウンリストに含まれているプロパティは一部であり、サポートされている CSS3 プロパティであればこのフィールドで任意に指定することができます。
1. 隣接するフィールドには、指定された CSS3 プロパティに対して有効な値を指定します。例えば、「**3px solid black**」を指定します。
1. 「**アイテムの追加**」をクリックし、次のプロパティとその値を追加します。
1. 「**プレビュー**」をクリックし、フォームの変更をプレビューで表示します。
1. 「**OK**」をクリックして変更を確認するか、または「**キャンセル**」をクリックして変更せずにダイアログを閉じます。
