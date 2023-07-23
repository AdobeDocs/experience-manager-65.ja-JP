---
title: アダプティブフォームにおけるセパレータコンポーネント
seo-title: Separator component in adaptive forms
description: セパレーターコンポーネントを使用して、フォームのセクションを視覚的に区別することができます。
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 51%

---

# アダプティブフォームにおけるセパレータコンポーネント{#separator-component-in-adaptive-forms}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象 [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

セパレーターコンポーネントを使用して、フォームのパネルを視覚的に区別することができます。セパレーターコンポーネントの全体的な外観やスタイルは、次のセパレーターコンポーネントのプロパティを指定することによって定義することができます。

* **エレメント名：** コンポーネントの名前を指定します。 SOM 式は、「要素名」フィールドで指定された値を持つコンポーネントに対応します。
* **太さ：**&#x200B;セパレーターコンポーネントの太さをピクセル単位で指定します。

* **CSS クラス：**&#x200B;セパレーターコンポーネントに対しカスタム CSS クラスを指定します。

* **インラインスタイル：** AEM Forms では、インライン CSS スタイルをアダプティブフォームの各コンポーネントに適用し、変更のプレビューをリアルタイムでプレビューできるようになりました。

レイアウトモードを使用して、セパレーターコンポーネントがまたがる列数を定義できます。詳しくは、[レイアウトモードを使用したコンポーネントのサイズ変更](../../forms/using/resize-using-layout-mode.md)を参照してください。

セパレーターコンポーネントのプロパティを指定するには：

1. セパレーターコンポーネントを選択して、![cmppr](assets/cmppr.png) をタップします。プロパティがサイドバーに開きます。
1. インライン CSS プロパティセクションのタブをクリックして、CSS プロパティを指定します。 例：a.「フィールド」タブで、 **項目を追加**. 2 つのフィールドを持つ行が追加されます。
1. 左側の最初のフィールドで、適用する CSS3 プロパティを指定します。 例： **ボーダー**. 下向き矢印ボタンをクリックしてプロパティを選択することもできます。 ドロップダウンリストに含まれるプロパティがすべてではなく、サポートされている CSS3 プロパティの名前をこのフィールドで指定できます。
1. 隣接するフィールドで、指定した CSS3 プロパティに有効な値を指定します。 例： **3px solid black**.
1. 「**アイテムの追加**」をクリックし、次のプロパティとその値を追加します。
1. 「**プレビュー**」をクリックし、フォームの変更をプレビューで表示します。
1. 「**OK**」をクリックして変更を確認するか、または「**キャンセル**」をクリックして変更せずにダイアログを閉じます。
