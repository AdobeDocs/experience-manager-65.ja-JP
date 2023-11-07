---
title: Adobe Experience Manager で Adobe Campaign フォームを作成
description: Adobe Experience Manager では、web サイトで Adobe Campaign とやり取りするフォームを作成して使用できます
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 95%

---

# AEM での Adobe Campaign フォームの作成  {#creating-adobe-campaign-forms-in-aem}

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

具体的な方法については、[テンプレートドキュメント](/help/sites-developing/templates.md#template-availability)を参照してください。

## フォームの作成 {#creating-a-form}

まず、オーサーインスタンスおよびパブリッシュインスタンスと Adobe Campaign の間の接続が有効であることを確認します。[Adobe Campaign Standard との統合](/help/sites-administering/campaignstandard.md)または [Adobe Campaign Classic との統合](/help/sites-administering/campaignonpremise.md)を参照してください。

>[!NOTE]
>
>Adobe Campaign Classic または Adobe Campaign Standard を使用する場合は、ページの **jcr:content** ノードの **acMapping** プロパティがそれぞれ **mapRecipient** または **profile** に設定されていることを確認してください。
>

1. AEMの Sites で、ページを作成する場所に移動します。
1. ページを作成して、「**Adobe Campaign Classic プロファイル**」または「 **Adobe Campaign Standard プロファイル**」を選択し、「**次へ**」をクリックします。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >目的のテンプレートを使用できない場合は、[テンプレートを使用可能にする](/help/sites-developing/templates.md#template-availability)を参照してください。

1. 「**名前**」フィールドにページ名を追加します。ページ名は有効な JCR 名である必要があります。
1. 「**タイトル**」フィールドにタイトルを入力し、「**作成**」をクリックします。
1. ページを開いて「**プロパティを開く**」を選択し、Cloud Service で Adobe Campaign 設定を追加し、チェックマークを選択して変更内容を保存します。

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. ページ上の&#x200B;**フォーム開始**&#x200B;コンポーネントで、フォームのタイプ（**購入、登録解除**、**プロファイルを保存**）を選択します。選択できるタイプはフォームごとに 1 つだけです。これで[フォームのコンテンツを編集](#editing-form-content)できるようになりました。

## フォームコンテンツの編集 {#editing-form-content}

Adobe Campaign 専用のフォームには、固有のコンポーネントがあります。これらのコンポーネントには、フォームの各フィールドをAdobe Campaignデータベースのフィールドにリンクするオプションがあります。

>[!NOTE]
>
>目的のテンプレートを使用できない場合は、[テンプレートを使用可能にする](/help/sites-authoring/adobe-campaign.md)を参照してください。

このセクションでは、Adobe Campaign へのリンクのみを取り上げます。Adobe Experience Manager でのフォームの使用方法に関する一般的な概要について詳しくは、[編集モードのコンポーネント](/help/sites-authoring/default-components-foundation.md)を参照してください。

1. 「**プロパティを開く**」を選択し、 Cloud Services に Adobe Campaign 設定を追加し、チェックマークを選択して変更内容を保存します。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. ページ上の&#x200B;**フォーム開始**&#x200B;コンポーネントで、設定アイコンをクリックします。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 「**詳細**」タブをクリックして、フォームのタイプ（**購読、購読解除**&#x200B;または&#x200B;**プロファイルを保存**）を選択し、「**OK」をクリックします。**&#x200B;選択できるタイプはフォームごとに 1 つだけです。

   * **Adobe Campaign：プロファイルを保存**：Adobe Campaign で受信者を作成または更新できます（デフォルト値）。
   * **Adobe Campaign：サービスを購入**：Adobe Campaign で受信者の購入を管理できます。
   * **Adobe Campaign：サービスの登録解除**：Adobe Campaign で受信者の登録をキャンセルできます。

1. 各フォームには 1 つの&#x200B;**暗号化されたプライマリキー**&#x200B;が必要です。このコンポーネントでは、Adobe Campaignプロファイルの暗号化されたプライマリキーを受け取るために使用される URL パラメーターを定義します。 「コンポーネント」で「Adobe Campaign」を選択すると、Adobe Campaign コンポーネントだけが表示されます。
1. 「**暗号化されたプライマリキー**」コンポーネントをフォーム（任意の場所）にドラッグし、「**設定**」アイコンをクリックまたはタップします。「**Adobe Campaign**」タブで、URL パラメーターに任意の名前を指定します。チェックマークをクリックまたはタップして、変更を保存します。

   このフォームへのリンクを生成するには、この URL パラメーターを使用して、Adobe Campaign プロファイルの暗号化されたプライマリキーを割り当てる必要があります。暗号化されたプライマリキーは、URL（パーセント）で適切にエンコードする必要があります。

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. 必要に応じて、「テキスト」フィールド、「日付」フィールド、「チェックボックス」フィールド、「オプション」フィールドなどのコンポーネントをこのフォームに追加します。各コンポーネントについての詳細情報は、[Adobe Campaign フォームコンポーネント](/help/sites-authoring/adobe-campaign-components.md)を参照してください。
1. 設定アイコンをクリックして、コンポーネントを開きます。例えば、「**テキストフィールド（Campaign）**」コンポーネントで、タイトルとテキストを変更します。

   「**Adobe Campaign**」をクリックして、フォームフィールドを Adobe Campaign のメタデータ変数にマップします。フォームを送信すると、マッピングされたフィールドが Adobe Campaign で更新されます。変数ピッカーには、タイプが一致するフィールドのみが表示されます（「テキスト」フィールドの文字列変数など）。

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >次の手順に従って、受信者テーブルに表示されているフィールドを追加または削除できます。[https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. 「**ページを公開**」をクリックします。ページがサイト上でアクティベートされます。AEM パブリケーションインスタンスに移動すると、ページを表示できます。[フォームをテストする](#testing-a-form)こともできます。

   >[!CAUTION]
   >
   >公開時にフォームを使用できる状態にするには、Cloud Service の匿名ユーザーに読み取り権限を付与する必要があります。ただし、匿名ユーザーに読み取り権限を付与するとセキュリティ問題が発生する可能性があるので、必ず Dispatcher の設定などの対策を講じてこのリスクを低減するようにしてください。

## フォームのテスト {#testing-a-form}

フォームを作成してフォームのコンテンツを編集した後で、フォームが想定通りに機能することを手動でテストできます。

>[!NOTE]
>
>各フォームには 1 つの&#x200B;**暗号化されたプライマリキー**&#x200B;が必要です。「コンポーネント」で「Adobe Campaign」を選択すると、Adobe Campaign コンポーネントだけが表示されます。
>
>この手順では EPK 番号を手動で入力しますが、実際には、ユーザーはニュースレター内でこのページへのリンク（登録解除、購入、プロファイルの更新）を取得します。EPK は、ユーザーに基づいて自動的に更新されます。
>
>そのようなリンクを作成するには、Adobe Campaign の EPK にリンクする可変の&#x200B;**メインリソース識別子**（Adobe Campaign Standard）または&#x200B;**暗号化された識別子**（Adobe Campaign Classic）を使用します（**テキストおよびパーソナライゼーション（Campaign）**&#x200B;コンポーネントなどで使用）。

これを行うには、Adobe Campaign プロファイルの EPK を手動で取得し、URL に追加する必要があります。

1. Adobe Campaign プロファイルの暗号化されたプライマリキー（EPK）を取得するには：

   * Adobe Campaign Standard では、**プロファイルおよびオーディエンス**／**プロファイル**&#x200B;に移動すると、既存のプロファイルが表示されます。テーブルの列に「**メインリソース識別子**」フィールドが表示されていることを確認します（「**リストを設定**」をクリックまたはタップして設定できます）。目的のプロファイルのメインリソース識別子をコピーします。
   * Adobe Campaign Classic では、**プロファイルとターゲット**／**受信者**&#x200B;に移動すると、既存のプロファイルが表示されます。テーブルの列に「**暗号化された識別子**」フィールドが表示されていることを確認します（エントリを右クリックし、「**リストを設定...**」を選択して設定できます）。目的のプロファイルの暗号化された識別子をコピーします。

1. AEM で、パブリッシュインスタンス上のフォームページを開き、ステップ 1 で取得した EPK を URL パラメーターとして付加します。フォームのオーサリング時に EPK コンポーネントで事前に定義したものと同じ名前を使用してください（例：`?epk=...`）。
1. これで、フォームを使用して、リンクされている Adobe Campaign プロファイルに関連付けられたデータと購読を変更できるようになりました。フィールドの一部を変更してフォームを送信すると、Adobe Campaign で適切なデータが更新されたことを確認できます。

フォームの検証が完了すると、Adobe Campaign データベース内のデータが更新されます。
