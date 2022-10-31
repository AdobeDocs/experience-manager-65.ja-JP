---
title: Adobe Target へのエクスペリエンスフラグメントの書き出し
seo-title: Exporting Experience Fragments to Adobe Target
description: Adobe Target へのエクスペリエンスフラグメントの書き出し
seo-description: Exporting Experience Fragments to Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 100%

---

# Adobe Target へのエクスペリエンスフラグメントの書き出し{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>このページの一部の機能には、AEM 6.5.3.0 以降のアプリケーションが必要です。
>
>6.5.3.0:
>
>* **Externalizer ドメイン**を選択できるようになりました。
   >  **メモ：** Externalizer ドメインは、Target に送信されるエクスペリエンスフラグメントのコンテンツにのみ関連し、「オファーコンテンツを表示」などのメタデータには関連しません。
>
>6.5.2.0：
>
>* エクスペリエンスフラグメントは、次のいずれかに書き出すことができます。
   >
   >   * デフォルトのワークスペース。
   >   * クラウド設定で指定された名前付きワークスペース。
   >   * **メモ：**&#x200B;特定のワークスペースに書き出すには、Adobe Target Premium が必要です。
>
>* AEM は [IMS を使用した Adobe Target と統合](/help/sites-administering/integration-target-ims.md)する必要があります。
>
>AEM 6.5.0.0 および 6.5.1.0：
>
>* AEM エクスペリエンスフラグメントは、Adobe Target のデフォルトのワークスペースに書き出されます。
>* AEM は、 [Adobe Target との統合](/help/sites-administering/target.md)の手順に従って Adobe Target と統合する必要があります。


Adobe Target（Target）向けに Adobe Experience Manager（AEM）で作成された[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)を書き出すことができます。書き出したエクスペリエンスフラグメントは、Target アクティビティのオファーとして使用し、幅広くエクスペリエンスをテストおよびパーソナライズできます。

エクスペリエンスフラグメントをAdobe Target に書き出す際には、3 つのフォーマットオプションを利用できます。

* HTML（デフォルト）：Web およびハイブリッドコンテンツ配信のサポート
* JSON：ヘッドレスコンテンツ配信のサポート
* HTML と JSON

AEM エクスペリエンスフラグメントは、Adobe Target のデフォルトワークスペースまたは Adobe Target のユーザー定義ワークスペースに書き出すことができます。これは、Adobe Developer Console を使用して行います。その場合、AEM は [IMS を使用した Adobe Target と統合](/help/sites-administering/integration-target-ims.md)する必要があります。

>[!NOTE]
>
>Adobe Target のワークスペースは、Adobe Target 自体には存在しません。これらのワークスペースは、Adobe IMS（Identity Management System）で定義および管理され、Adobe Developer Console からの統合を使用するソリューション全体で使用するために選択されます。

>[!NOTE]
>
>Adobe Target のワークスペースを使用すると、組織（グループ）のメンバーは、他のユーザーにアクセス権を付与することなく、その組織専用のオファーとアクティビティを作成および管理することができます。例えば、国際的な企業の国別の組織などです。

>[!NOTE]
>
>詳しくは、以下も参照してください。
>
>* [Adobe Target Developers](https://www.adobe.io/apis/experiencecloud/target.html)
>* [コアコンポーネント - エクスペリエンスフラグメント](https://docs.adobe.com/content/help/ja/experience-manager-core-components/using/components/experience-fragment.html)
>


## 前提条件 {#prerequisites}

>[!CAUTION]
>
>このページの一部の機能には、AEM 6.5.3.0 のアプリケーションが必要です。

様々なアクションが必要です。

1. [IMS を使用して AEM と Adobe Target を統合する](/help/sites-administering/integration-target-ims.md)必要があります。
2. エクスペリエンスフラグメントは AEM オーサーインスタンスから書き出されるので、オーサーインスタンスに [AEM Link Externalizer を設定](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)して、クスペリエンスフラグメント内のあらゆる参照が web 配信用に外部化されるようにする必要があります。

   >[!NOTE]
   >
   >デフォルトでカバーされていないリンクの書き換えでは、[Experience Fragment Link Rewriter Provider](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) が利用可能です。これにより、インスタンスに合わせてカスタマイズされたルールを開発できます。

## クラウド設定の追加 {#add-the-cloud-configuration}

フラグメントを書き出す前に、**Adobe Target** 用の&#x200B;**クラウド設定**&#x200B;をフラグメントまたはフォルダーに追加する必要があります。この結果、次のことも可能になります。

* 書き出しに使用する形式オプションを指定する
* Target ワークスペースを宛先として選択する
* エクスペリエンスフラグメントに含まれる参照を書き換えるための Externalizer ドメインを選択する（オプション）

必要なオプションは、必要なフォルダーやフラグメントの&#x200B;**ページのプロパティ**&#x200B;で選択できます。仕様は必要に応じて継承されます。

1. **エクスペリエンスフラグメント**&#x200B;コンソールに移動します。

1. 適切なフォルダーまたはフラグメントの&#x200B;**ページのプロパティ**&#x200B;を開きます。

   >[!NOTE]
   >
   >クラウド設定をエクスペリエンスフラグメントの親フォルダーに追加すると、設定はすべての子に継承されます。
   >
   >
   >クラウド設定をエクスペリエンスフラグメント自体に追加すると、設定はすべての変更によって継承されます。

1. 「**クラウドサービス**」タブを選択します。

1. **クラウドサービス設定**&#x200B;で、ドロップダウンリストから「**Adobe Target**」を選択します。

   >[!NOTE]
   >
   >エクスペリエンスフラグメントオファーの JSON 形式はカスタマイズできます。これをおこなうには、顧客のエクスペリエンスフラグメントコンポーネントを定義し、そのプロパティをコンポーネント Sling Model に書き出す方法に注釈を付けます。
   >
   >コアコンポーネントを参照してください。
   >
   >[コアコンポーネント - エクスペリエンスフラグメント](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   **Adobe Target** の下で、次を選択します。

   * 適切な設定
   * 必要な形式オプション
   * Adobe Target ワークスペース
   * Externalizer ドメイン（必要な場合）

   >[!CAUTION]
   >
   >Externalizer ドメインはオプションです。
   >
   >AEM Externalizer を設定するのは、コンテンツの書き出し先を特定の&#x200B;*パブリッシュ*&#x200B;ドメインに指定する場合です。詳しくは、[AEM Link Externalizer の設定](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)を参照してください。
   >
   >また、Externalizer ドメインは、Target に送信されるエクスペリエンスフラグメントのコンテンツにのみ関係があり、「オファーコンテンツを表示」などのメタデータには関係しません。

   例えば、フォルダーの場合は下図のようになります。

   ![フォルダー - Cloud Services](assets/xf-target-integration-01.png "フォルダー - Cloud Services")

1. **保存して閉じます**。

## Adobe Target へのエクスペリエンスフラグメントの書き出し {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>画像などのメディアアセットでは、参照のみが Target に書き出されます。アセット自体は AEM Assets に格納されたままで、AEM パブリッシュインスタンスから配信されます。
>
>このため、エクスペリエンスフラグメントは、すべての関連アセットと共に、Target に書き出す前に公開する必要があります。

AEM から Target にエクスペリエンスフラグメントを書き出すには（クラウド設定を指定した後）：

1. エクスペリエンスフラグメントコンソールに移動します。
1. Target に書き出すエクスペリエンスフラグメントを選択します。

   >[!NOTE]
   >
   >エクスペリエンスフラグメント Web のバリエーションである必要があります。

1. **Adobe Target に書き出し**&#x200B;をタップ／クリックします。

   >[!NOTE]
   >
   >エクスペリエンスフラグメントが既に書き出されている場合は、**Adobe Target でアップデート** を選択します。

1. 要求に応じて&#x200B;**公開せずに書き出し**&#x200B;または&#x200B;**公開**&#x200B;をタップ／クリックします。

   >[!NOTE]
   >
   >**公開**&#x200B;を選択すると、エクスペリエンスフラグメントはすぐに公開され、Target に送信されます。

1. 確認ダイアログで「**OK**」をタップ／クリックします。

   エクスペリエンスフラグメントは Target に送信されているはずです。

   >[!NOTE]
   >
   >書き出しについての[様々な詳細](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment)は、コンソールの&#x200B;**リストビュー**&#x200B;と&#x200B;**プロパティ**&#x200B;で参照できます。

   >[!NOTE]
   >
   >Adobe Target でエクスペリエンスフラグメントを表示すると、表示される&#x200B;*最終変更日*&#x200B;は、フラグメントが最後に Adobe Target に書き出された日付ではなく、AEM でフラグメントが最後に変更された日付です。

>[!NOTE]
>
>あるいは、[ページ情報](/help/sites-authoring/author-environment-tools.md#page-information)メニューの同等のコマンドを使用して、ページエディターから書き出しを実行することもできます。

## Adobe Target でのエクスペリエンスフラグメントの使用 {#using-your-experience-fragments-in-adobe-target}

ここまでのタスクを完了すると、エクスペリエンスフラグメントが Target のオファーページに表示されます。Target 側でできることを詳しく知るには、[Target に特化したドキュメント](https://experiencecloud.adobe.com/resources/help/ja_JP/target/target/aem-experience-fragments.html)を参照してください。

>[!NOTE]
>
>Adobe Target でエクスペリエンスフラグメントを表示すると、表示される&#x200B;*最終変更日*&#x200B;は、フラグメントが最後に Adobe Target に書き出された日付ではなく、AEM でフラグメントが最後に変更された日付です。

## Adobe Target に書き出し済みのエクスペリエンスフラグメントの削除 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

Target に書き出し済みのエクスペリエンスフラグメントを削除すると、そのフラグメントが既に Target のオファーで使用されている場合に問題が発生する可能性があります。フラグメントのコンテンツが AEM によって配信されているため、フラグメントを削除するとオファーが使用できなくなります。

そのような状況を避けるためには：

* エクスペリエンスフラグメントが現在アクティビティで使用されていない場合、AEM はユーザーに警告メッセージなしでフラグメントを削除することを許可します。
* エクスペリエンスフラグメントが現在ターゲットのアクティビティで使用されている場合、フラグメントを削除するとアクティビティに影響が及ぶ可能性があると、AEM ユーザーに警告メッセージが表示されます。

   AEM のエラーメッセージは、ユーザーがエクスペリエンスフラグメントを（強制的に）削除することを禁止するものではありません。エクスペリエンスフラグメントが削除された場合は、次のような結果になります。

   * AEM エクスペリエンスフラグメントを使用した Target オファーで望ましくない動作が見られる場合があります。

      * エクスペリエンスフラグメント HTML が Target にプッシュされたため、オファーが引き続きレンダリングされる可能性があります。
      * 参照されているアセットが AEM でも削除されている場合、エクスペリエンスフラグメント内の参照はどれも正しく機能しない可能性があります。
   * 当然ながら、エクスペリエンスフラグメントが AEM には存在しないため、さらに変更することは不可能です。
