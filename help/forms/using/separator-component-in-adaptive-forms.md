---
title: アダプティブフォームにおけるセパレーターコンポーネント
description: セパレーターコンポーネントを使用して、フォームのセクションを視覚的に区別することができます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 97%
---
# アダプティブフォームにおけるセパレーターコンポーネント{#separator-component-in-adaptive-forms}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。 これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。 この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

セパレーターコンポーネントを使用して、フォームのパネルを視覚的に区別できます。 セパレーターコンポーネントの全体的な外観やスタイルは、次のようなセパレータコンポーネントのプロパティを指定して定義できます。

* **要素名**：コンポーネント名を指定します。 SOM 式は、要素名フィールドで指定された値を持つコンポーネントに対応しています。
* **太さ：**&#x200B;セパレーターコンポーネントの太さをピクセル単位で指定します。

* **CSS クラス：**&#x200B;セパレーターコンポーネントに対しカスタム CSS クラスを指定します。

* **インラインスタイル：** AEM Forms では、インライン CSS スタイルをアダプティブフォームの各コンポーネントに適用し、変更のプレビューをリアルタイムでプレビューできるようになりました。

レイアウトモードを使用して、セパレーターコンポーネントがまたがる列数を定義できます。 詳しくは、[レイアウトモードを使用したコンポーネントのサイズ変更](../../forms/using/resize-using-layout-mode.md)を参照してください。

セパレーターコンポーネントのプロパティを指定するには：

1. セパレーターコンポーネントを選択して、![cmppr](assets/cmppr.png) を選択します。 プロパティがサイドバーで開きます。
1. 「インライン CSS プロパティ」セクションでタブをクリックし、CSS プロパティを指定します。 例：a。 「フィールド」タブで、「**項目を追加**」をクリックします。 2 つのフィールドを持った行が追加されます。
1. 左から最初のフィールドで、適用したい CSS3 プロパティを指定します。 例えば、**ボーダー**&#x200B;を指定します。 下矢印をクリックしてプロパティを選択することもできます。 ドロップダウンリストに含まれているプロパティは一部であり、サポートされている CSS3 プロパティであればこのフィールドで任意に指定することができます。
1. 隣接するフィールドには、指定された CSS3 プロパティに対して有効な値を指定します。 例えば、「**3px solid black**」を指定します。
1. 「**アイテムの追加**」をクリックし、次のプロパティとその値を追加します。
1. 「**プレビュー**」をクリックし、フォームの変更をプレビューで表示します。
1. 「**OK**」をクリックして変更を確認するか、または「**キャンセル**」をクリックして変更せずにダイアログを閉じます。
