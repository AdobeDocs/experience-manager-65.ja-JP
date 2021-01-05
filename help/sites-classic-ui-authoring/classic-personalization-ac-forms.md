---
title: AEM での Adobe Campaign フォームの作成
seo-title: AEM での Adobe Campaign フォームの作成
description: AEM では、Web サイト上で Adobe Campaign と連携するフォームを作成できます。特定のフィールドをフォームに挿入して、Adobe Campaign データベースにマップできます。
seo-description: AEM では、Web サイト上で Adobe Campaign と連携するフォームを作成できます。特定のフィールドをフォームに挿入して、Adobe Campaign データベースにマップできます。
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 62%

---


# AEM での Adobe Campaign フォームの作成{#creating-adobe-campaign-forms-in-aem}

AEM では、Web サイト上で Adobe Campaign と連携するフォームを作成できます。特定のフィールドをフォームに挿入して、Adobe Campaign データベースにマップできます。

新しい連絡先の購読、購読解除、ユーザープロファイルデータを管理しつつ、そのデータを Adobe Campaign データベースに統合できます。

Adobe Campaign フォームを AEM で使用するには、このドキュメントで説明する以下のステップを実行する必要があります。

1. テンプレートを使用可能にします。
1. フォームを作成します。
1. フォームコンテンツを編集します。

デフォルトでは、Adobe Campaign 固有の次の 3 種類のフォームを使用できます。

* プロファイルを保存
* サービスを購読
* サービスの購読を解除

これらのフォームは、Adobe Campaign プロファイルの暗号化されたプライマリキー（EPK）を受け入れる URL パラメーターを定義します。フォームはこの URL パラメーターに基づいて、関連付けられている Adobe Campaign プロファイルのデータを更新します。

一般的な使用事例では、これらのフォームを別々に作成しますが、ニュースレターのコンテンツ内にフォームページへのパーソナライズされたリンクを組み込み、受信者がそのリンクを開いて自分のプロファイルデータを調整（購読解除、購読またはプロファイル更新）できるようにします。

フォームは、ユーザーに基づいて自動的に更新されます。詳しくは、[フォームコンテンツの編集](#editing-form-content)を参照してください。

## テンプレートを使用可能にする  {#making-a-template-available}

Adobe Campaign 固有のフォームを作成するには、まず、様々なテンプレートを AEM アプリケーションで使用可能にする必要があります。

これを行うには、[テンプレートのドキュメント](/help/sites-developing/page-templates-static.md#templateavailability)を参照してください。

まず、オーサーインスタンスおよびパブリッシュインスタンスと Adobe Campaign の間の接続が有効なことを確認します。[Adobe Campaign Standard との統合](/help/sites-administering/campaignstandard.md)または [Adobe Campaign 6.1 との統合](/help/sites-administering/campaignonpremise.md)を参照してください。

>[!NOTE]
>
>Adobe Campaign 6.1.x または Adobe Campaign Standard を使用する場合は、ページの **jcr:content** ノードの **acMapping** プロパティがそれぞれ **mapRecipient** または **profile** に設定されていることを確認してください。


### フォームの作成 {#creating-a-form}

1. サイト管理者として開始します。
1. ツリー構造をたどって、選択した Web サイト内のフォームを作成したい場所に移動します。
1. **新規**/**新規ページ…を選択します。**。
1. **Adobe Campaignプロファイル(AC 6.1)**&#x200B;または&#x200B;**Adobe Campaignプロファイル(ACS)**&#x200B;テンプレートを選択し、ページのプロパティを入力します。

   >[!NOTE]
   >
   >テンプレートが使用できない場合は、[「テンプレートを使用可能にする](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate)」の節を参照してください。

1. 「**作成**」をクリックしてフォームを作成します。

   ![chlimage_1-187](assets/chlimage_1-187.png)

   これで[フォームのコンテンツを編集および設定](#editing-form-content)できます。

## フォームコンテンツの編集  {#editing-form-content}

Adobe Campaign 専用のフォームには、固有のコンポーネントがあります。これらのコンポーネントでは、フォームの各フィールドを Adobe Campaign データベースのフィールドにリンクすることができます。

>[!NOTE]
>
>目的のテンプレートが使用できない場合は、[テンプレートを使用可能にする](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate)を参照してください。

このセクションでは、Adobe Campaign へのリンクのみを取り上げます。Adobe Experience Managerでのフォームの使い方の一般的な概要について詳しくは、[編集モードコンポーネント](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)を参照してください。

1. 編集するフォームに移動します。
1. ツールボックスで、**ページ**/**ページのプロパティを選択します。**&#x200B;次に、ポップアップウィンドウの「**Cloud Services**」タブに移動します。
1. 「追加&#x200B;**service**」をクリックし追加、Adobe Campaignサービスのドロップダウンリストで、使用しているAdobe Campaignインスタンスに対応する設定を選択します。 この設定は、インスタンスとの間の接続を設定すると実行されます。詳しくは、[AEMとAdobe Campaignの接続](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign)を参照してください。

   >[!NOTE]
   >
   >必要に応じて、南京錠アイコンをクリックして設定をロック解除し、Adobe Campaign サービスを追加します。

1. フォームの開始にある「**編集**」ボタンを使用して、フォームの一般的なパラメーターにアクセスします。 「**フォーム**」タブを使用すると、フォームの検証後にユーザーがリダイレクトされる「ありがとうございます」ページを選択できます。

   **高度な**&#x200B;フォームでは、フォームの種類を選択できます。 **投稿のオプション**&#x200B;フィールドでは、次の3種類のAdobe Campaignフォームから選択できます。

   * **Adobe Campaign：プロファイルを保存**：Adobe Campaign で受信者を作成または更新できます（デフォルト値）。
   * **Adobe Campaign：サービスを購読**：Adobe Campaign で受信者の購読を管理できます。
   * **Adobe Campaign：サービスの購読を解除**：Adobe Campaign で受信者の購読をキャンセルできます。

   **Action Configuration**&#x200B;フィールドを使用して、受信者プロファイルが存在しない場合にAdobe Campaignデータベースに作成するかどうかを指定できます。 これを行うには、「**既存の**&#x200B;でない場合はユーザーを作成」オプションを選択します。

1. 選択したコンポーネントをツールボックスからフォームにドラッグ＆ドロップして追加します。使用可能な Adobe Campaign 固有コンポーネントについては、[Adobe Campaign フォームコンポーネント](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)を参照してください。

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 追加したフィールドをダブルクリックして設定します。「**Adobe Campaign**」タブを使用すると、フィールドをAdobe Campaign受信者テーブル内のフィールドにリンクできます。 さらに、このフィールドを、Adobe Campaign データベース内の既存の受信者を認識するための調整キーの一部にするかどうかを指定できます。

   >[!CAUTION]
   >
   >**要素名**&#x200B;は、フォームフィールドごとに異なる名前にする必要があります。 必要に応じて変更してください。
   >
   >Adobe Campaignデータベース内の受信者を正しく管理するには、各フォームに暗号化されたプライマリキー&#x200B;**コンポーネントが含まれている必要があります。**

1. ツールボックスで&#x200B;**ページ**/**ページをアクティブにする/>を選択して、ページをアクティブにします。**&#x200B;ページがサイト上でアクティベートされます。AEM のパブリッシュインスタンスに移動すると、ページを見ることができます。フォームが検証されると、Adobe Campaign データベースのデータが更新されます。

## フォームのテスト  {#testing-a-form}

フォームを作成してフォームのコンテンツを編集したら、そのフォームが想定どおりに機能することを手動でテストできます。

>[!NOTE]
>
>各フォームには、**暗号化されたプライマリキー**&#x200B;コンポーネントが必要です。 「コンポーネント」で、「Adobe Campaign」を選択して、これらのコンポーネントのみを表示します。
>
>この手順では暗号化されたプライマリキー（EPK）の番号を手動で入力しますが、実際には、ニュースレター内にこのページへの（購読解除、購読またはプロファイル更新をおこなうための）リンクが表示されます。EPK はユーザーに基づいて自動的に更新されます。
>
>このリンクを作成するには、epkをAdobe Campaignにリンクする変数&#x200B;**メインリソース識別子**(Adobe Campaign Standard)または&#x200B;**暗号化された識別子**(Adobe Campaign6.1)を使用します(例えば、**テキスト&amp;パーソナライゼーション(キャンペーン)**&#x200B;コンポーネント内)。

そのためには、Adobe Campaign プロファイルの EPK を手動で取得して、URL に付加する必要があります。

1. Adobe Campaign プロファイルの暗号化されたプライマリキー（EPK）を取得するには：

   * Adobe Campaign Standardで、**プロファイルーとオーディエンス** > **プロファイル**&#x200B;に移動します。これは既存のプロファイルをリストします。 テーブルの列に「**Main Resource Identifier**」フィールドが表示されていることを確認します(「**リストを設定**」をクリックまたはタップして設定できます)。 目的のプロファイルのメインリソース識別子をコピーします。
   * Adobe Campaign6.11では、**プロファイルとターゲット** > **受信者**&#x200B;に移動します。これは既存のプロファイルをリストします。 テーブルに、列に&#x200B;**Encrypted identifier**&#x200B;フィールドが表示されていることを確認します(エントリを右クリックし、**リストを設定…を選択して設定できます)。**)。 目的のプロファイルの暗号化された識別子をコピーします。

1. AEMで、発行インスタンスでフォームページを開き、手順1のEPKをURLパラメーターとして追加します。フォームの作成時に、EPKコンポーネントで事前に定義したのと同じ名前を使用します(例：`?epk=...`)
1. これで、フォームを使用して、リンクされている Adobe Campaign プロファイルに関連付けられたデータと購読を変更できるようになりました。一部のフィールドを変更してフォームを送信したら、Adobe Campaign で適切なデータが更新されていることを確認できます。

フォームが検証されると、Adobe Campaign データベースのデータが更新されます。
