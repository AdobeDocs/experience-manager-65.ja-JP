---
title: エクスペリエンスフラグメントのAdobe Targetへの書き出し
seo-title: エクスペリエンスフラグメントのAdobe Targetへの書き出し
description: エクスペリエンスフラグメントのAdobe Targetへの書き出し
seo-description: エクスペリエンスフラグメントのAdobe Targetへの書き出し
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 45%

---

# エクスペリエンスフラグメントのAdobe Targetへの書き出し{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>このページの一部の機能には、AEM 6.5.3.0が必要です。
>
>6.5.3.0
>
>* **Externalizer Domainscanが選** 択されるようになりました。
   >  **注意：** Externalizerドメインは、Targetに送信されるエクスペリエンスフラグメントのコンテンツにのみ関連し、オファーコンテンツを表示などのメタデータには関連しません。
>
>
6.5.2.0:
>
>* エクスペリエンスフラグメントは、次のいずれかに書き出すことができます。
   >
   >   
   * デフォルトのワークスペース。
   >   * クラウド設定で指定された名前付きワークスペース。
   >   * **注意：** 特定のワークスペースに書き出すには、Adobe Target Premiumが必要です。
>
>* AEMは、Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md)を使用してAdobe Targetと[統合する必要があります。

>
>

AEM 6.5.0.0および6.5.1.0:
>
>* AEMエクスペリエンスフラグメントは、Adobe Targetのデフォルトのワークスペースに書き出されます。
>* [Adobe Targetとの統合](/help/sites-administering/target.md)の手順に従って、AEMをAdobe Targetと統合する必要があります。


Adobe Experience Manager(AEM)で作成した[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)をAdobe Target(Target)に書き出すことができます。 書き出したエクスペリエンスフラグメントは、Target アクティビティのオファーとして使用し、幅広くエクスペリエンスをテストおよびパーソナライズできます。

エクスペリエンスフラグメントをAdobe Target に書き出す際には、3 つのフォーマットオプションを利用できます。

* HTML（デフォルト）:Webおよびハイブリッドコンテンツ配信のサポート
* JSON:ヘッドレスコンテンツ配信のサポート
* HTML と JSON

AEMエクスペリエンスフラグメントは、Adobe Targetのデフォルトのワークスペースに書き出すことも、Adobe Targetのユーザー定義ワークスペースに書き出すこともできます。 これはAdobe I/Oを使用しておこない、AEMは、Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md)を使用してAdobe Targetと[統合する必要があります。

>[!NOTE]
>
>Adobe Targetワークスペースは、Adobe Target自体には存在しません。 これらは、AdobeIMS(Identity Managementシステム)で定義および管理され、Adobe I/O統合を使用するソリューション間での使用のために選択されます。

>[!NOTE]
>
>Adobe Target workspacesを使用すると、組織（グループ）のメンバーに対して、この組織のオファーとアクティビティの作成と管理のみを許可できます。他のユーザーへのアクセス権を付与することなく。 例えば、グローバルに関係する国固有の組織。

>[!NOTE]
>
>詳しくは、以下を参照してください。
>
>* [Adobe Target開発](https://www.adobe.io/apis/experiencecloud/target.html)
>* [コアコンポーネント — エクスペリエンスフラグメント](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

>



## 前提条件 {#prerequisites}

>[!CAUTION]
>
>このページの一部の機能には、AEM 6.5.3.0が必要です。

様々なアクションが必要です。

1. Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md)を使用して、AEMとAdobe Targetを[統合する必要があります。
2. エクスペリエンスフラグメントはAEMオーサーインスタンスから書き出されるので、オーサーインスタンスでAEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)を設定して、エクスペリエンスフラグメント内の参照がWeb配信用に外部化されるようにする必要があります。[

   >[!NOTE]
   >
   >デフォルトでカバーされていないリンクの書き換えでは、[Experience Fragment Link Rewriter Provider](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) が利用可能です。これにより、インスタンスに合わせてカスタマイズされたルールを開発できます。

## クラウド設定{#add-the-cloud-configuration}の追加

フラグメントを書き出す前に、**Adobe Target** 用の&#x200B;**クラウド設定**&#x200B;をフラグメント、またはフォルダーに追加する必要があります。また、次の操作も可能です。

* エクスポートに使用するフォーマットオプションを指定します。
* 宛先としてのTargetワークスペースの選択
* エクスペリエンスフラグメント内の参照を書き換える外部化子ドメインを選択します（オプション）。

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

1. 「**Cloud Service設定**」で、ドロップダウンリストから「**Adobe Target**」を選択します。

   >[!NOTE]
   >
   >エクスペリエンスフラグメントオファーのJSON形式はカスタマイズできます。 これをおこなうには、顧客のエクスペリエンスフラグメントコンポーネントを定義し、そのプロパティをコンポーネントSling Modelに書き出す方法に注釈を付けます。
   >
   >コアコンポーネントを参照してください。
   >
   >[コアコンポーネント — エクスペリエンスフラグメント](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   **Adobe Target**&#x200B;の下で、次を選択します。

   * 適切な設定
   * 必要な形式オプション
   * Adobe Target
   * 必要な場合 — externalizerドメイン

   >[!CAUTION]
   >
   >Externalizerドメインはオプションです。
   >
   > AEM Externalizerは、書き出されたコンテンツが特定の&#x200B;*パブリッシュ*&#x200B;ドメインを指すように設定する場合に設定します。 詳しくは、[AEM Link Externalizerの設定](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)を参照してください。
   >
   > また、Externalizerドメインは、Targetに送信されるエクスペリエンスフラグメントのコンテンツにのみ関連し、オファーコンテンツを表示などのメタデータには関連しません。

   例えば、フォルダーの場合：

   ![フォルダー — クラウドサ](assets/xf-target-integration-01.png "ービスフォルダー —Cloud Services")

1. **保存して閉じます**。

## エクスペリエンスフラグメントのAdobe Targetへの書き出し{#exporting-an-experience-fragment-to-adobe-target}

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
   >エクスペリエンスフラグメントがすでに書き出されている場合は、**Adobe Target でアップデート** を選択します。

1. 要求に応じて&#x200B;**公開せずに書き出し**&#x200B;または&#x200B;**公開**&#x200B;をタップ／クリックします。

   >[!NOTE]
   >
   >**公開**&#x200B;を選択すると、エクスペリエンスフラグメントはすぐに公開され、Target に送信されます。

1. 確認ダイアログで「**OK**」をタップまたはクリックします。

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

## Adobe Target {#using-your-experience-fragments-in-adobe-target}でのエクスペリエンスフラグメントの使用

前述のタスクを実行すると、エクスペリエンスフラグメントがTargetのオファーページに表示されます。 Target 側でできることを詳しく知るには、[Target に特化したドキュメント](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html)を参照してください。

>[!NOTE]
>
>Adobe Target でエクスペリエンスフラグメントを表示すると、表示される&#x200B;*最終変更日*&#x200B;は、フラグメントが最後に Adobe Target に書き出された日付ではなく、AEM でフラグメントが最後に変更された日付です。

## 既にAdobe Targetに書き出されたエクスペリエンスフラグメントの削除{#deleting-an-experience-fragment-already-exported-to-adobe-target}

Target に書き出し済みのエクスペリエンスフラグメントを削除すると、そのフラグメントがすでに Target のオファーで使用されている場合に問題が発生する可能性があります。フラグメントのコンテンツが AEM によって配信されているため、フラグメントを削除するとオファーが使用できなくなります。

そのような状況を避けるためには：

* エクスペリエンスフラグメントが現在アクティビティで使用されていない場合、AEM はユーザーに警告メッセージなしでフラグメントを削除することを許可します。
* エクスペリエンスフラグメントが現在ターゲットのアクティビティで使用されている場合、フラグメントを削除するとアクティビティに影響が及ぶ可能性があると、AEM ユーザーに警告メッセージが表示されます。

   AEM のエラーメッセージは、ユーザーがエクスペリエンスフラグメントを（強制的に）削除することを禁止するものではありません。エクスペリエンスフラグメントを削除した場合：

   * AEMエクスペリエンスフラグメントを含むTargetオファーで、望ましくない動作が表示される場合があります

      * エクスペリエンスフラグメントHTMLがTargetにプッシュされた場合、オファーは引き続きレンダリングされる可能性が高くなります
      * 参照元のアセットがAEMでも削除された場合、エクスペリエンスフラグメント内の参照が正しく機能しない可能性があります。
   * もちろん、エクスペリエンスフラグメントはAEMに存在しなくなったので、エクスペリエンスフラグメントに対するそれ以上の変更は不可能です。
