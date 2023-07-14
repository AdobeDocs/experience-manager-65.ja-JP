---
title: 非表示条件の使用
description: 非表示条件を使用して、コンポーネントリソースがレンダリングされるかどうかを判断できます。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 44%

---

# 非表示条件の使用 {#using-hide-conditions}

非表示条件を使用して、コンポーネントリソースがレンダリングされるかどうかを判断できます。 例えば、テンプレート作成者がコアコンポーネントを設定する場合などです [リストコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=ja) 内 [テンプレートエディター](/help/sites-authoring/templates.md) とは、子ページに基づいてリストを作成するためのオプションを無効にすることを決定します。 デザインダイアログボックスでこのオプションを無効にすると、リストコンポーネントのレンダリング時に非表示条件が評価され、子ページを表示するオプションが表示されないようにプロパティが設定されます。

## 概要 {#overview}

多数のオプションが用意されているダイアログボックスは複雑になり、使用できるオプションのごく一部しか使用できない場合があります。 これにより、ユーザーのユーザーインターフェイスエクスペリエンスが圧倒的に高まる可能性があります。

非表示条件を使用すると、管理者、開発者およびスーパーユーザーは、一連のルールに基づいてリソースを非表示にできます。 この機能を使用すると、作成者がコンテンツを編集したときに表示するリソースを決定できます。

>[!NOTE]
>
>式に基づいてリソースを非表示にしても、ACL 権限は置き換えられません。 コンテンツは編集可能なままですが表示されません。

## 実装と使用の詳細 {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` は、フィルタリング対象のフィールドの `granite:hide` プロパティの有無と値に基づいてリソースをフィルタリングします。`/libs/cq/gui/components/authoring/dialog/dialog.jsp` の実装には、`FilteringResourceWrapper.` のインスタンスが含まれます。

この実装では、Granite [ELResolver API](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) を利用し、ExpressionCustomizer を介して `cqDesign` カスタム変数を追加します。

以下に、`etc/design` 内かコンテンツポリシーとして配置されているデザインノードの非表示の条件の例をいくつか示します。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

非表示の式を定義する際は、次の点に注意してください。

* 式を有効にするには、プロパティの検索範囲を表します（例：`cqDesign.myProperty`）。
* 値は読み取り専用です。
* 関数（必要に応じて）は、サービスが提供する特定のセットに限定する必要があります。

## 例 {#example}

非表示の条件の例は、AEM 全体（特に、[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)）で確認できます。例えば、 [リストコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=ja).

[テンプレートエディターを使用](/help/sites-authoring/templates.md)した場合、テンプレート作成者は、ページ作成者が利用できるリストコンポーネントのオプションをデザインダイアログで定義できます。リストを静的リスト、子ページのリスト、タグ付きページのリストなどにするかどうかなどのオプションを有効または無効にできます。

テンプレート作成者が子ページオプションを無効にする場合、デザインプロパティが設定され、非表示の条件がそれに対して評価されるので、ページ作成者に対してオプションがレンダリングされません。

1. デフォルトでは、ページ作成者は、リストコアコンポーネントを使用し、「 」オプションを選択することで、子ページを使用したリストを作成できます **子ページ**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. テンプレート作成者は、リストコアコンポーネントのデザインダイアログでオプション「**子の無効化**」を選択して、子ページに基づいたリストを生成するオプションがページ作成者に対して表示されないようにできます。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` の下にポリシーノードが作成され、`disableChildren` プロパティが `true` に設定されます。
1. 非表示条件は、ダイアログのプロパティノード `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` の `granite:hide` プロパティの値として定義されます。

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. `disableChildren` の値がデザイン設定から取得され、式 `${cqDesign.disableChildren}` が `false` と評価されます。つまり、そのオプションはコンポーネントの一部としてレンダリングされません。

   `granite:hide` プロパティの値として非表示式を使用している例は、[GitHub のこちらのページ](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40)で確認できます。

1. ページ作成者がリストコンポーネントを使用するときに、オプション「**子ページ**」が表示されなくなりました。

   ![chlimage_1-221](assets/chlimage_1-221.png)
