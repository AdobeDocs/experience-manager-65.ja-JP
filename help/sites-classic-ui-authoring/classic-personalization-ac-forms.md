---
title: 'AEM での Adobe Campaign フォームの作成 '
seo-title: Creating Adobe Campaign Forms in AEM
description: AEM では、Web サイト上で Adobe Campaign と連携するフォームを作成できます。特定のフィールドをフォームに挿入して、Adobe Campaign データベースにマップできます。
seo-description: AEM lets you create and use forms that interact with Adobe Campaign on your website. Specific fields can be inserted into your forms and mapped to the Adobe Campaign database.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1228'
ht-degree: 100%

---

# AEM での Adobe Campaign フォームの作成 {#creating-adobe-campaign-forms-in-aem}

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

## テンプレートを使用可能にする {#making-a-template-available}

Adobe Campaign 固有のフォームを作成するには、まず、様々なテンプレートを AEM アプリケーションで使用可能にする必要があります。

具体的な方法については、[テンプレートのドキュメント](/help/sites-developing/page-templates-static.md#templateavailability)を参照してください。

まず、オーサーインスタンスおよびパブリッシュインスタンスと Adobe Campaign の間の接続が有効なことを確認します。[Adobe Campaign Standard との統合](/help/sites-administering/campaignstandard.md)または [Adobe Campaign 6.1 との統合](/help/sites-administering/campaignonpremise.md)を参照してください。

>[!NOTE]
>
>Adobe Campaign 6.1.x または Adobe Campaign Standard を使用する場合は、ページの **jcr:content** ノードの **acMapping** プロパティがそれぞれ **mapRecipient** または **profile** に設定されていることを確認してください。

### フォームの作成 {#creating-a-form}

1. サイト管理者として開始します。
1. 選択した web サイト内で、フォームを作成したい場所にツリー構造をたどって移動します。
1. **新規**／**新しいページ...**&#x200B;を選択します。
1. **Adobe Campaign プロファイル（AC 6.1）**&#x200B;または **Adobe Campaign プロファイル（ACS）**&#x200B;テンプレートを選択して、ページのプロパティを入力します。

   >[!NOTE]
   >
   >テンプレートが使用可能になっていない場合は、[テンプレートを使用可能にする](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate)のセクションを参照してください。

1. 「**作成**」をクリックしてフォームを作成します。

   ![chlimage_1-187](assets/chlimage_1-187.png)

   これで[フォームのコンテンツを編集および設定](#editing-form-content)できます。

## フォームコンテンツの編集 {#editing-form-content}

Adobe Campaign 専用のフォームには、固有のコンポーネントがあります。これらのコンポーネントでは、フォームの各フィールドを Adobe Campaign データベースのフィールドにリンクすることができます。

>[!NOTE]
>
>目的のテンプレートが使用可能になっていない場合は、[テンプレートを使用可能にする](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate)を参照してください。

このセクションでは、Adobe Campaign へのリンクのみを取り上げます。Adobe Experience Manager でのフォームの使用方法に関する一般的な概要について詳しくは、[編集モードのコンポーネント](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)を参照してください。

1. 編集するフォームに移動します。
1. ツールボックスで&#x200B;**ページ**／**ページプロパティ...**&#x200B;を選択し、ポップアップウィンドウの「**クラウドサービス**」タブに移動します。
1. 「**サービスを追加**」をクリックし、サービスのドロップダウンリストで Adobe Campaign インスタンスに対応する設定を選択して、Adobe Campaign サービスを追加します。この設定は、インスタンスとの接続を設定すると実行されます。詳しくは、[Adobe Campaign への AEM の接続](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign)を参照してください。

   >[!NOTE]
   >
   >必要に応じて、南京錠アイコンをクリックして設定をロック解除し、Adobe Campaign サービスを追加します。

1. フォームの先頭にある「**編集**」ボタンを使用して、フォームの一般的なパラメーターにアクセスします。「**フォーム**」タブを使用すると、ありがとうページを選択して、フォームの検証後にユーザーをリダイレクトすることができます。

   「**詳細**」フォームを使用すると、フォームのタイプを選択できます。「**投稿オプション**」フィールドで、次の 3 種類の Adobe Campaign フォームから選択できます。

   * **Adobe Campaign：プロファイルを保存**：Adobe Campaign で受信者を作成または更新できます（デフォルト値）。
   * **Adobe Campaign：サービスを購読**：Adobe Campaign で受信者の購読を管理できます。
   * **Adobe Campaign：サービスの購読を解除**：Adobe Campaign で受信者の購読をキャンセルできます。

   「**アクションの設定**」フィールドでは、受信者のプロファイルがまだ存在しない場合に、Adobe Campaign データベースに受信者のプロファイルを作成するかどうかを指定できます。作成する場合は、「**存在しない場合にユーザーを作成**」オプションをオンにします。

1. 選択したコンポーネントをツールボックスからフォームにドラッグ＆ドロップして追加します。使用可能な Adobe Campaign 固有コンポーネントについては、[Adobe Campaign フォームコンポーネント](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)を参照してください。

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 追加したフィールドをダブルクリックして設定します。「**Adobe Campaign**」タブを使用して、フィールドを Adobe Campaign の受信者テーブルのフィールドにリンクします。さらに、このフィールドを、Adobe Campaign データベース内の既存の受信者を認識するための調整キーの一部にするかどうかを指定できます。

   >[!CAUTION]
   >
   >**エレメント名**&#x200B;は、フォームフィールドごとに異なっている必要があります。必要に応じて変更してください。
   >
   >Adobe Campaign データベース内で受信者を正しく管理するために、フォームごとに 1 つの&#x200B;**暗号化されたプライマリキー**&#x200B;コンポーネントを含める必要があります。

1. ツールボックスで&#x200B;**ページ**／**ページをアクティベート**&#x200B;を選択して、ページをアクティベートします。ページがサイト上でアクティベートされます。AEM のパブリッシュインスタンスに移動すると、ページを見ることができます。フォームが検証されると、Adobe Campaign データベースのデータが更新されます。

## フォームのテスト {#testing-a-form}

フォームを作成してフォームのコンテンツを編集したら、そのフォームが想定どおりに機能することを手動でテストできます。

>[!NOTE]
>
>各フォームには 1 つの&#x200B;**暗号化されたプライマリキー**&#x200B;が必要です。「コンポーネント」で「Adobe Campaign」を選択すると、Adobe Campaign コンポーネントだけが表示されます。
>
>この手順では暗号化されたプライマリキー（EPK）の番号を手動で入力しますが、実際には、ニュースレター内にこのページへの（購読解除、購読またはプロファイル更新をおこなうための）リンクが表示されます。EPK はユーザーに基づいて自動的に更新されます。
>
>そのようなリンクを作成するには、Adobe Campaign の EPK にリンクする可変の&#x200B;**メインリソース識別子**（Adobe Campaign Standard）または&#x200B;**暗号化された識別子**（Adobe Campaign 6.1）を使用します（**テキストおよびパーソナライゼーション（Campaign）**&#x200B;コンポーネントなどで使用します）。

そのためには、Adobe Campaign プロファイルの EPK を手動で取得して、URL に付加する必要があります。

1. Adobe Campaign プロファイルの暗号化されたプライマリキー（EPK）を取得するには：

   * Adobe Campaign Standard では、**プロファイルおよびオーディエンス**／**プロファイル**&#x200B;に移動すると、既存のプロファイルが表示されます。テーブルの列に「**メインリソース識別子**」フィールドが表示されていることを確認します（「**リストを設定**」をクリックまたはタップして設定できます）。目的のプロファイルのメインリソース識別子をコピーします。
   * Adobe Campaign 6.11 では、**プロファイルとターゲット**／**受信者**&#x200B;に移動すると、既存のプロファイルが表示されます。テーブルの列に「**暗号化された識別子**」フィールドが表示されていることを確認します（エントリを右クリックし、「**リストを設定...**」を選択して設定できます）。目的のプロファイルの暗号化された識別子をコピーします。

1. AEM で、パブリッシュインスタンス上のフォームページを開き、ステップ 1 で取得した EPK を URL パラメーターとして付加します。フォームのオーサリング時に EPK コンポーネントで以前定義したものと同じ名前を使用してください（例：`?epk=...`）。
1. これで、フォームを使用して、リンクされている Adobe Campaign プロファイルに関連付けられたデータと購読を変更できるようになりました。一部のフィールドを変更してフォームを送信したら、Adobe Campaign で適切なデータが更新されていることを確認できます。

フォームが検証されると、Adobe Campaign データベースのデータが更新されます。
