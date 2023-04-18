---
title: Adobe Experience ManagerでのAdobe Campaign Formsの作成
description: Adobe Experience Managerを使用すると、Web サイト上でAdobe Campaignとやり取りするフォームを作成して使用できます
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 37%

---

# AEM での Adobe Campaign フォームの作成  {#creating-adobe-campaign-forms-in-aem}

AEMを使用すると、Web サイト上でAdobe Campaignとやり取りするフォームを作成して使用できます。 特定のフィールドをフォームに挿入し、Adobe Campaignデータベースにマッピングできます。

新しい連絡先の購読、購読解除およびユーザープロファイルデータを管理し、そのデータをAdobe Campaignデータベースに統合できます。

AEMでAdobe Campaign forms を使用するには、このドキュメントで説明する次の手順に従う必要があります。

1. テンプレートを使用可能にします。
1. フォームを作成します。
1. フォームコンテンツを編集します。

デフォルトでは、Adobe Campaign専用の 3 種類のフォームを使用できます。

* プロファイルの保存
* サービスを購読
* サービスを購読解除

これらのフォームは、Adobe Campaignプロファイルの暗号化されたプライマリキーを受け入れる URL パラメーターを定義します。 この URL パラメーターに基づいて、フォームは関連するAdobe Campaignプロファイルのデータを更新します。

これらのフォームは独立して作成していますが、一般的な使用例では、ニュースレターコンテンツ内のフォームページにパーソナライズされたリンクを生成するので、受信者はリンクを開き、プロファイルデータ（購読解除、購読、更新）を調整できます。

フォームは、ユーザーに基づいて自動的に更新されます。 詳しくは、 [フォームコンテンツの編集](#editing-form-content) を参照してください。

## テンプレートを使用可能にする {#making-a-template-available}

Adobe Campaign専用のフォームを作成する前に、AEMアプリケーションで様々なテンプレートを使用できるようにする必要があります。

具体的な方法については、[テンプレートドキュメント](/help/sites-developing/templates.md#template-availability)を参照してください。

## フォームの作成 {#creating-a-form}

まず、オーサーインスタンスとパブリッシュインスタンスの間の接続が動作していることを確認し、Adobe Campaignが動作していることを確認します。 詳しくは、 [Adobe Campaign Standardとの統合](/help/sites-administering/campaignstandard.md) または [Adobe Campaign Classicとの統合](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Adobe Campaign Classic または Adobe Campaign Standard を使用する場合は、ページの **jcr:content** ノードの **acMapping** プロパティがそれぞれ **mapRecipient** または **profile** に設定されていることを確認してください。

1. AEM の Sites で、新しいページを作成する場所に移動します。
1. ページを作成して、「**Adobe Campaign Classic プロファイル**」または「 **Adobe Campaign Standard プロファイル**」を選択し、「**次へ**」をクリックします。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >目的のテンプレートを使用できない場合は、[テンプレートを使用可能にする](/help/sites-developing/templates.md#template-availability)を参照してください。

1. 内 **名前** 「 」フィールドで、ページの名前を追加します。 有効な JCR 名を指定する必要があります。
1. 内 **タイトル** フィールドにタイトルを入力し、 **作成**.
1. ページを開き、「 」を選択します。 **プロパティを開く** 「Cloud Services」でAdobe Campaign設定を追加し、チェックマークを選択して変更を保存します。

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. ページの **フォーム開始** コンポーネント、次のフォームのタイプを選択します。 **購読、購読解除、**&#x200B;または&#x200B;**プロファイルを保存**. 選択できるタイプはフォームごとに 1 つだけです。これで[フォームのコンテンツを編集](#editing-form-content)できるようになりました。

## フォームコンテンツの編集 {#editing-form-content}

Adobe Campaign専用のFormsには、特定のコンポーネントがあります。 これらのコンポーネントには、フォームの各フィールドをAdobe Campaignデータベースのフィールドにリンクできるオプションがあります。

>[!NOTE]
>
>目的のテンプレートを使用できない場合は、[テンプレートを使用可能にする](/help/sites-authoring/adobe-campaign.md)を参照してください。

このセクションでは、Adobe Campaign へのリンクのみを取り上げます。Adobe Experience Manager でのフォームの使用方法に関する一般的な概要について詳しくは、[編集モードのコンポーネント](/help/sites-authoring/default-components-foundation.md)を参照してください。

1. 「**プロパティを開く**」を選択し、 Cloud Services に Adobe Campaign 設定を追加し、チェックマークを選択して変更内容を保存します。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. ページ上の&#x200B;**フォーム開始**&#x200B;コンポーネントで、設定アイコンをクリックします。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 「**詳細**」タブをクリックして、フォームのタイプ（**購読、購読解除**&#x200B;または&#x200B;**プロファイルを保存**）を選択し、「**OK」をクリックします。**&#x200B;選択できるタイプはフォームごとに 1 つだけです。

   * **Adobe Campaign:プロファイルを保存**:Adobe Campaign（デフォルト値）で受信者を作成または更新できます。
   * **Adobe Campaign:サービスを購読**:Adobe Campaignで受信者の購読を管理できます。
   * **Adobe Campaign:サービスを購読解除**:Adobe Campaignで受信者の購読をキャンセルできます。

1. 次が必要です： **暗号化されたプライマリキー** 各フォームのコンポーネント このコンポーネントでは、Adobe Campaignプロファイルの暗号化されたプライマリキーを受け取るために使用される URL パラメーターを定義します。 「コンポーネント」で「Adobe Campaign」を選択すると、Adobe Campaign コンポーネントだけが表示されます。
1. 「**暗号化されたプライマリキー**」コンポーネントをフォーム（任意の場所）にドラッグし、「**設定**」アイコンをクリックまたはタップします。内 **Adobe Campaign** タブで、URL パラメーターの任意の名前を指定します。 チェックマークをクリックまたはタップして、変更を保存します。

   このフォームへのリンクを生成する場合、この URL パラメーターを使用して、Adobe Campaignプロファイルの暗号化されたプライマリキーを割り当てる必要があります。 暗号化されたプライマリキーは、URL（パーセント）で正しくエンコードする必要があります。

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. 必要に応じて、テキストフィールド、日付フィールド、チェックボックスフィールド、オプションフィールドなどのコンポーネントをフォームに追加します。 詳しくは、 [Adobe Campaign Form Components](/help/sites-authoring/adobe-campaign-components.md) を参照してください。
1. 設定アイコンをクリックして、コンポーネントを開きます。 例えば、「**テキストフィールド（Campaign）**」コンポーネントで、タイトルとテキストを変更します。

   「**Adobe Campaign**」をクリックして、フォームフィールドを Adobe Campaign のメタデータ変数にマップします。フォームを送信すると、マッピングされたフィールドがAdobe Campaignで更新されます。 変数ピッカーで使用できるのは、タイプが一致するフィールドのみです（例えば、テキストフィールドの文字列変数）。

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >次の手順に従って、受信者テーブルに表示されているフィールドを追加または削除できます。[https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. クリック **ページを公開**. ページがサイト上でアクティベートされます。 AEMパブリッシュインスタンスに移動すると、表示できます。 また、 [フォームをテストする](#testing-a-form).

   >[!CAUTION]
   >
   >公開時にフォームを使用するには、クラウドサービスの匿名ユーザーに対して読み取り権限を付与する必要があります。 ただし、匿名ユーザーに読み取り権限を付与する際にセキュリティ上の問題が発生する可能性があることに注意し、Dispatcher の設定などによってセキュリティ上の問題を軽減するようにしてください。

## フォームのテスト {#testing-a-form}

フォームを作成してフォームのコンテンツを編集した後、手動でそのフォームが期待どおりに動作しているかをテストすることができます。

>[!NOTE]
>
>各フォームには 1 つの&#x200B;**暗号化されたプライマリキー**&#x200B;が必要です。「コンポーネント」で「Adobe Campaign」を選択すると、Adobe Campaign コンポーネントだけが表示されます。
>
>この手順では EPK 番号を手動で入力しますが、実際には、ニュースレター内でこのページへのリンク（配信停止、配信登録、プロファイルの更新のいずれをおこなうかに関わらず）がユーザーに表示されます。 ユーザーに基づいて、epk が自動的に更新されます。
>
>そのようなリンクを作成するには、Adobe Campaign の EPK にリンクする可変の&#x200B;**メインリソース識別子**（Adobe Campaign Standard）または&#x200B;**暗号化された識別子**（Adobe Campaign Classic）を使用します（**テキストおよびパーソナライゼーション（Campaign）**&#x200B;コンポーネントなどで使用）。

これをおこなうには、Adobe Campaignプロファイルの EPK を手動で取得し、それを URL に追加する必要があります。

1. Adobe Campaignプロファイルの暗号化されたプライマリキー (EPK) を取得するには：

   * Adobe Campaign Standard では、**プロファイルおよびオーディエンス**／**プロファイル**&#x200B;に移動すると、既存のプロファイルが表示されます。テーブルの列に「**メインリソース識別子**」フィールドが表示されていることを確認します（「**リストを設定**」をクリックまたはタップして設定できます）。目的のプロファイルのメインリソース識別子をコピーします。
   * Adobe Campaign Classic では、**プロファイルとターゲット**／**受信者**&#x200B;に移動すると、既存のプロファイルが表示されます。テーブルの列に「**暗号化された識別子**」フィールドが表示されていることを確認します（エントリを右クリックし、「**リストを設定...**」を選択して設定できます）。目的のプロファイルの暗号化された識別子をコピーします。

1. AEM で、パブリッシュインスタンス上のフォームページを開き、ステップ 1 で取得した EPK を URL パラメーターとして付加します。フォームのオーサリング時に EPK コンポーネントで事前に定義したものと同じ名前を使用してください（例：`?epk=...`）。
1. これで、フォームを使用して、リンクされたAdobe Campaignプロファイルに関連付けられたデータと購読を変更できるようになります。 一部のフィールドを変更してフォームを送信した後、Adobe Campaign内で適切なデータが更新されたことを確認できます。

フォームの検証が完了すると、Adobe Campaignデータベース内のデータが更新されます。
