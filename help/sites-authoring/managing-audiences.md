---
title: オーディエンスの管理
description: オーディエンスコンソールを使用して、Adobe Targetアカウント用のオーディエンスを作成、整理および管理したり、ContextHub または ClientContext 用のセグメントを管理したりできます
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
exl-id: 97e02986-049f-4747-a67a-6aa0677b281e
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 83%

---

# オーディエンスの管理{#managing-audiences}

オーディエンスコンソールを使用して、Adobe Targetアカウント用のオーディエンスを作成、整理および管理したり、ContextHub または ClientContext 用のセグメントを管理したりできます。

* オーディエンスの追加 - Adobe Target オーディエンスまたは ContextHub セグメント。
* オーディエンスの管理 

オーディエンス（ContextHub および ClientContext では&#x200B;*セグメント*&#x200B;と呼びます）とは、特定の条件によって定義される訪問者のクラスのことです。この条件が、ターゲットアクティビティの表示対象を決定します。アクティビティをターゲット設定する場合は、ターゲティングプロセスで直接オーディエンスを選択するか、またはオーディエンスコンソールでオーディエンスを追加作成します。

オーディエンスコンソールでは、オーディエンスはブランド別に整理されます。

オーディエンスは、ターゲティングモードで[ターゲットコンテンツのオーサリング](/help/sites-authoring/content-targeting-touch.md)に使用できます。その際、オーディエンスを作成することもできます（ただし、オーディエンスコンソールで Adobe Target オーディエンスを作成する必要があります）。ターゲティングモードで作成したオーディエンスは、オーディエンスコンソールに表示されます。

オーディエンスは、定義されているオーディエンスの種類を示すラベルと共に表示されます。

* CH - ContextHub セグメント
* CC - ClientContext セグメント
* AT - Adobe Target オーディエンス

## オーディエンスコンソールでの ContextHub セグメントの作成 {#creating-a-contexthub-segment-in-the-audiences-console}

ContextHub セグメントは、オーディエンスコンソールまたはターゲット設定プロセスで作成できます。

オーディエンスコンソールで ContextHub セグメントを作成するには：

1. ナビゲーションコンソールで、 **パーソナライズ**. クリック **オーディエンス**.
1. クリック **ContextHub セグメントを作成**.

   ![screen-shot_2019-03-05at124034](assets/screen-shot_2019-03-05at124034.png)

1. **新しい ContextHub セグメント**&#x200B;ダイアログボックスで、タイトルを入力し、ブーストを調整して、「**作成**」をクリックします。新しい ContextHub セグメントがオーディエンスリストに表示されます。

   >[!NOTE]
   >
   >新しく作成したオーディエンスがあるか確認するために降順に並べ替えるには、「**変更済み**」をタップまたはクリックして、変更済みのリストを並べ替えることができます。

ContextHub を使用するセグメント作成の詳細については、[ContextHub によるセグメント化の設定](/help/sites-administering/segmentation.md)ドキュメントを参照してください。

## オーディエンスコンソールを使用した Adobe Target オーディエンスの作成 {#creating-an-adobe-target-audience-using-the-audience-console}

オーディエンスコンソールを使用して、Adobe Target オーディエンスを AEM で直接作成できます。

オーディエンスは、誰がターゲットアクティビティに含まれるかを決定するルールによって定義されます。オーディエンス定義には複数のルールを含めることができ、各ルールには複数のパラメーターを含めることができます。

複数のルールを指定した場合は、ルールがブール演算式 AND で結合されます。つまり、定義済みの条件をすべて満たす場合にのみ、潜在的なオーディエンスメンバーがアクティビティに含められます。例えば、AND を使用して OS ルールとブラウザールールを定義した場合、定義された OS と定義されたブラウザーの両方を使用している訪問者のみ、アクティビティに含められます。

>[!NOTE]
>
>**作成**&#x200B;メニューに「ターゲットオーディエンスを作成」が表示されない場合は、オーディエンスの作成に必要な権限がありません。オーディエンスを作成するには、**/etc/segmentation** より下の階層における書き込み権限が必要です。content-authors グループには、デフォルトで書き込み権限があります。

Adobe Target オーディエンスを作成するには：

1. ナビゲーションコンソールで、 **パーソナライズ**. クリック **オーディエンス**.

   ![screen-shot_2019-03-05at124139](assets/screen-shot_2019-03-05at124139.png)

1. オーディエンスコンソールで、 **作成** 「**Target オーディエンスを作成**」をクリックします。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Adobe Analytics の **Adobe Target Configuration** ダイアログボックスで、ターゲット設定を選択し、 **OK**.
1. [ 規則#1] 領域で、属性タイプをクリックし、使用可能なフィールドに属性情報を入力します。 終了したら、属性の右側にあるチェックマークを選択して保存します。すべての属性について詳しくは、[属性とそのオプション](#attributes-and-their-options)を参照してください。
1. 「**ルールを追加**」をクリックして、別のルールを追加します。必要な数だけルールを入力します。複数のルールを指定した場合は、ルールがブール演算子 AND で結合されます。これは、各ルールの要件をすべて満たすオーディエンスだけが、そのアクティビティの対象になるということです。
1. 「**次へ**」をクリックします。
1. オーディエンスの名前を入力し、 **保存**.
1. 「**保存**」をクリックします。オーディエンスはオーディエンスリストに表示されます。

### 属性とそのオプション {#attributes-and-their-options}

次の各属性に対して、ターゲティングルールを作成できます。

| **属性** | **説明** | **詳細情報** |
|---|---|---|
| **モバイル** | モバイルデバイス、デバイスの種類、デバイスのベンダー、画面の寸法（ピクセル単位）などのパラメーターに基づいてモバイルデバイスをターゲットに設定します。 | 詳しくは、Adobe Target で[モバイルドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=ja)を参照してください。 |
| **カスタム** | カスタムパラメーターは、mbox パラメーターです。mbox に対して mbox パラメーターを渡した場合、または targetPageParams 関数を使用した場合、それらのパラメーターはここに表示され、オーディエンスで使用できます。 | 詳しくは、Adobe Target で[カスタムパラメータードキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=ja)を参照してください。 |
| **OS** | 特定のオペレーティングシステムを使用する訪問者をターゲットに設定できます。 | Linux®、Macintosh または Windows を使用するユーザーをターゲットに設定します。 |
| **サイトページ** | 特定のページを閲覧している、または特定の mbox パラメーターを持つ訪問者をターゲットに設定します。 | Adobe Target で[サイトページに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=ja)を参照してください。 |
| **ブラウザー** | ページの訪問時に特定のブラウザーまたは特定のブラウザーオプションを使用するユーザーをターゲットに設定できます。 | Adobe Target で[ブラウザーオプションに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=ja)を参照してください。 |
| **訪問者プロファイル** | 特定のプロファイルパラメーターを満たす訪問者をターゲットに設定します。 | Adobe Target で[訪問者プロファイルに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html?lang=ja)を参照してください。 |
| **トラフィックソース** | サイトに導いた検索エンジンやランディングページに基づいて訪問者をターゲットに設定します。 | Adobe Target で[トラフィックソースに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=ja)を参照してください。 |

## オーディエンスコンソールでのオーディエンスの変更 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>編集している AEM インスタンスと同じ AEM インスタンスで作成された Adobe Target オーディエンスのみを編集できます。異なる AEM 環境で作成されたターゲットオーディエンスは編集できません。

ContextHub オーディエンスまたは ClientContext オーディエンスは、オーディエンスコンソールから編集できます。また、次のように Adobe Target オーディエンスも編集できますが、AEM で作成されたオーディエンスのみです。

1. ナビゲーションコンソールで、 **パーソナライズ**. クリック **オーディエンス**.
1. 編集する ContextHub または ClientContext セグメントの横のアイコンをクリックし、 **編集**.
1. セグメントエディターで編集を行います。詳しくは、[Client Context](/help/sites-administering/campaign-segmentation.md) または [ContextHub](/help/sites-developing/ch-configuring.md) ドキュメントを参照してください。
