---
title: AEM での Adobe Campaign フォームの作成
description: AEM では、web サイトで Adobe Campaign とやり取りするフォームを作成して使用できます。特定のフィールドをフォームに挿入して、Adobe Campaign データベースにマッピングできます。
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 93%

---

# AEM での Adobe Campaign フォームの作成 {#creating-adobe-campaign-forms-in-aem}

AEM では、web サイトで Adobe Campaign とやり取りするフォームを作成して使用できます。特定のフィールドをフォームに挿入して、Adobe Campaign データベースにマッピングできます。

新しい連絡先の購入、登録解除、ユーザープロファイルデータを管理し、そのデータを Adobe Campaign データベースに統合することができます。

AEM で Adobe Campaign フォームを使用するには、このドキュメントで説明する次の手順を実行する必要があります。

1. テンプレートを使用可能にします。
1. フォームを作成します。
1. フォームコンテンツを編集します。

デフォルトでは、Adobe Campaign 固有の次の 3 種類のフォームを使用できます。

* プロファイルを保存
* サービスを購入
* サービスを登録解除

これらのフォームは、Adobe Campaign プロファイルの暗号化されたプライマリキーを受け入れる URL パラメーターを定義します。フォームはこの URL パラメーターに基づいて、関連付けられている Adobe Campaign プロファイルのデータを更新します。

一般的なユースケースでは、これらのフォームを個別に作成しますが、ニュースレターコンテンツ内でフォームページへのパーソナライズされたリンクを生成し、受信者がリンクを開いて自分のプロファイルデータ（登録解除、購入、プロファイルの更新など）を調整できるようにします。

フォームは、ユーザーに基づいて自動的に更新されます。詳細情報は、[フォームコンテンツの編集](#editing-form-content)を参照してください。

## テンプレートを使用可能にする {#making-a-template-available}

Adobe Campaign 固有のフォームを作成する前に、AEM アプリケーションで様々なテンプレートを使用できるようにする必要があります。

具体的な方法については、[テンプレートのドキュメント](/help/sites-developing/page-templates-static.md#templateavailability)を参照してください。

まず、オーサーインスタンスおよびパブリッシュインスタンスと Adobe Campaign の間の接続が有効であることを確認します。詳しくは、[Adobe Campaign Standard との統合](/help/sites-administering/campaignstandard.md)または [Adobe Campaign 6.1 との統合](/help/sites-administering/campaignonpremise.md)を参照してください。

>[!NOTE]
>
>Adobe Campaign 6.1.x または Adobe Campaign Standard を使用する場合は、ページの **jcr:content** ノードの **acMapping** プロパティがそれぞれ **mapRecipient** または **profile** に設定されていることを確認してください。
>

### フォームの作成 {#creating-a-form}

1. siteadmin で開始します。
1. 選択した web サイト内で、フォームを作成したい場所にツリー構造をたどって移動します。
1. **新規**／**新しいページ...**&#x200B;を選択します。
1. **Adobe Campaign プロファイル（AC 6.1）**&#x200B;または **Adobe Campaign プロファイル（ACS）**&#x200B;テンプレートを選択して、ページのプロパティを入力します。

   >[!NOTE]
   >
   >テンプレートが使用可能になっていない場合は、[テンプレートを使用可能にする](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate)のセクションを参照してください。

1. 「**作成**」をクリックしてフォームを作成します。

   ![chlimage_1-187](assets/chlimage_1-187.png)

   その後、[フォームのコンテンツを編集および設定](#editing-form-content)できます。

## フォームコンテンツの編集 {#editing-form-content}

Adobe Campaign 専用のフォームには、固有のコンポーネントがあります。これらのコンポーネントには、フォームの各フィールドをAdobe Campaignデータベースのフィールドにリンクするオプションがあります。

>[!NOTE]
>
>目的のテンプレートを使用できない場合は、[テンプレートを使用可能にする](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate)を参照してください。

このセクションでは、Adobe Campaign へのリンクのみを取り上げます。Adobe Experience Manager でのフォームの使用方法に関する一般的な概要について詳しくは、[編集モードのコンポーネント](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)を参照してください。

1. 編集するフォームに移動します。
1. ツールボックスで&#x200B;**ページ**／**ページプロパティ...**&#x200B;を選択し、ポップアップウィンドウの「**クラウドサービス**」タブに移動します。
1. 「**サービスを追加**」をクリックし、サービスのドロップダウンリストで Adobe Campaign インスタンスに対応する設定を選択して、Adobe Campaign サービスを追加します。この設定は、インスタンスとの接続を設定すると実行されます。詳しくは、[Adobe Campaign への AEM の接続](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign)を参照してください。

   >[!NOTE]
   >
   >必要に応じて、南京錠アイコンをクリックして設定をロック解除し、Adobe Campaign サービスを追加します。

1. フォームの先頭にある「**編集**」ボタンを使用して、フォームの一般的なパラメーターにアクセスします。The **フォーム** 「 」タブを使用すると、フォームの検証後にユーザーがリダイレクトされる「ありがとうございます」ページを選択できます。

   The **詳細** フォームを使用すると、フォームのタイプを選択できます。 「**投稿オプション**」フィールドで、次の 3 種類の Adobe Campaign フォームから選択できます。

   * **Adobe Campaign：プロファイルを保存**：Adobe Campaign（デフォルト値）で受信者を作成または更新できます。
   * **Adobe Campaign：サービスを購入**：Adobe Campaign で受信者の購入を管理できます。
   * **Adobe Campaign：サービスの登録解除**：Adobe Campaignで受信者の購読をキャンセルできます。

   「**アクションの設定**」フィールドでは、受信者のプロファイルがまだ存在しない場合に、Adobe Campaign データベースに受信者のプロファイルを作成するかどうかを指定できます。作成する場合は、「**存在しない場合にユーザーを作成**」オプションをオンにします。

1. 選択したコンポーネントをツールボックスからドラッグし、フォームにドロップして追加します。使用可能な Adobe Campaign 固有のコンポーネントについて詳しくは、[アドビフォームコンポーネント](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)を参照してください。

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 追加したフィールドをダブルクリックして設定します。 「**Adobe Campaign**」タブを使用して、フィールドを Adobe Campaign の受信者テーブルのフィールドにリンクします。さらに、このフィールドを、Adobe Campaign データベース内の既存の受信者を認識するための調整キーの一部にするかどうかを指定できます。

   >[!CAUTION]
   >
   >**要素名**&#x200B;は、フォームフィールドごとに異なっている必要があります。必要に応じて変更してください。
   >
   >各フォームには、 **暗号化されたプライマリキー** Adobe Campaignデータベースで受信者を正しく管理するためのコンポーネント。

1. ツールボックスで&#x200B;**ページ**／**ページをアクティベート**&#x200B;を選択して、ページをアクティベートします。ページがサイト上でアクティベートされます。AEM パブリケーションインスタンスに移動すると、ページを表示できます。フォームの検証が完了すると、Adobe Campaign データベース内のデータが更新されます。

## フォームのテスト {#testing-a-form}

フォームを作成してフォームのコンテンツを編集した後で、フォームが想定通りに機能することを手動でテストできます。

>[!NOTE]
>
>各フォームには 1 つの&#x200B;**暗号化されたプライマリキー**&#x200B;が必要です。「コンポーネント」で「Adobe Campaign」を選択すると、Adobe Campaign コンポーネントだけが表示されます。
>
>この手順では EPK 番号を手動で入力しますが、実際には、ユーザーはニュースレター内でこのページへのリンク（登録解除、購入、プロファイルの更新）を取得します。EPK は、ユーザーに基づいて自動的に更新されます。
>
>そのようなリンクを作成するには、Adobe Campaign の EPK にリンクする可変の&#x200B;**メインリソース識別子**（Adobe Campaign Standard）または&#x200B;**暗号化された識別子**（Adobe Campaign 6.1）を使用します（**テキストおよびパーソナライゼーション（Campaign）**&#x200B;コンポーネントなどで使用します）。

これを行うには、Adobe Campaign プロファイルの EPK を手動で取得し、URL に追加する必要があります。

1. Adobe Campaign プロファイルの暗号化されたプライマリキー（EPK）を取得するには：

   * Adobe Campaign Standard では、**プロファイルおよびオーディエンス**／**プロファイル**&#x200B;に移動すると、既存のプロファイルが表示されます。テーブルの列に「**メインリソース識別子**」フィールドが表示されていることを確認します（「**リストを設定**」をクリックまたはタップして設定できます）。目的のプロファイルのメインリソース識別子をコピーします。
   * Adobe Campaign 6.11 では、**プロファイルとターゲット**／**受信者**&#x200B;に移動すると、既存のプロファイルが表示されます。テーブルの列に「**暗号化された識別子**」フィールドが表示されていることを確認します（エントリを右クリックし、「**リストを設定...**」を選択して設定できます）。目的のプロファイルの暗号化された識別子をコピーします。

1. AEM で、パブリッシュインスタンス上のフォームページを開き、ステップ 1 で取得した EPK を URL パラメーターとして付加します。フォームのオーサリング時に EPK コンポーネントで事前に定義したものと同じ名前を使用してください（例：`?epk=...`）。
1. これで、フォームを使用して、リンクされている Adobe Campaign プロファイルに関連付けられたデータと購読を変更できるようになりました。フィールドの一部を変更してフォームを送信すると、Adobe Campaign で適切なデータが更新されたことを確認できます。

フォームの検証が完了すると、Adobe Campaign データベース内のデータが更新されます。
