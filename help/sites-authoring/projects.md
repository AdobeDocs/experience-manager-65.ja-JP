---
title: プロジェクト
seo-title: プロジェクト
description: プロジェクトを使用すると、リソースを 1 つのエンティティにグループ化でき、共通の共有環境でプロジェクトを簡単に管理できます
seo-description: プロジェクト 共通の共有環境を使用する1つのエンティティにリソースをグループ化すると、プロジェクトを簡単に管理できます。
uuid: 4b5b9d78-d515-46af-abe2-882da0a1c8ae
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: dee7ac7c-ca86-48e9-8d95-7826fa926c68
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# プロジェクト{#projects}

プロジェクトを使用すると、リソースを 1 つのエンティティにグループ化できます。共通の共有環境で、プロジェクトを簡単に管理できます。プロジェクトに関連付けることができるリソースのタイプは、AEM ではタイルと呼ばれます。Tiles may include project and team information, assets, workflows, and other types of information, as described in detail in [Project Tiles.](#project-tiles)

>[!CAUTION]
>
>For users in projects to see other users/groups while using Projects functionality like creating projects, creating tasks/workflows, seeing and managing the team, those users need to have read access on **/home/users** and **/home/groups**. The easiest way to implement this is to give the **projects-users** group read access to **/home/users** and**/home/groups**.

次の操作をおこなうことができます。

* プロジェクトの作成
* プロジェクトへのコンテンツフォルダーおよびアセットフォルダーの関連付け
* プロジェクトの削除
* コンテンツリンクのプロジェクトからの削除

次の追加トピックを参照してください。

* [プロジェクトの管理
   ](/help/sites-authoring/touch-ui-managing-projects.md)
* [タスクの使用](/help/sites-authoring/task-content.md)
* [プロジェクトワークフローの操作](/help/sites-authoring/projects-with-workflows.md)
* [クリエイティブプロジェクトと PIM 統合](/help/sites-authoring/managing-product-information.md)

## プロジェクトコンソール {#projects-console}

プロジェクトコンソールで、AEM 内のプロジェクトにアクセスし、管理します。

![screen-shot_2019-03-05at125110](assets/screen-shot_2019-03-05at125110.png)

* 「**タイムライン**」を選択してからプロジェクトを選択すると、プロジェクトのタイムラインが表示されます。
* 「**選択**」をクリックまたはタップすると、選択モードに入ります。
* 「**作成**」をクリックして、プロジェクトを追加します。
* 「**アクティブなプロジェクトを切り替え**」を使用して、すべてのプロジェクトとアクティブなプロジェクトのみを切り替えることができます。
* 「**統計ビューを表示**」を使用して、タスクの完了に関するプロジェクト統計を表示できます。

## プロジェクトタイル {#project-tiles}

プロジェクトを使用して、様々なタイプの情報とプロジェクトを関連付けることができます。このような情報は&#x200B;**タイル**&#x200B;と呼ばれます。各タイルと含まれる情報の種類について、このセクションで説明します。

以下のタイルをプロジェクトと関連付けることができます。それぞれについては、以降のセクションで説明します。

* アセットおよびアセットコレクション
* エクスペリエンス
* リンク
* プロジェクト情報
* チーム
* ランディングページ
* 電子メール
* ワークフロー
* ローンチ
* タスク

### アセット {#assets}

**アセット**&#x200B;タイルでは、特定のプロジェクトに使用するすべてのアセットを集めることができます。

![chlimage_1-70](assets/chlimage_1-70.png)

タイル内でアセットを直接アップロードします。さらに、ダイナミックメディアのアドオンがある場合は、画像セット、スピンセットまたは混在メディアセットを作成できます。

![chlimage_1-71](assets/chlimage_1-71.png)

### アセットコレクション {#asset-collections}

アセットと同様に、[アセットコレクション](/help/assets/managing-collections-touch-ui.md)をプロジェクトに直接追加できます。アセット内にコレクションを定義します。

![chlimage_1-72](assets/chlimage_1-72.png)

コレクションを追加するには、「**コレクションを追加**」をクリックし、適切なコレクションをリストから選択します。

### エクスペリエンス {#experiences}

**エクスペリエンス**&#x200B;タイルでは、モバイルアプリ、Web サイトまたは公開物をプロジェクトに追加できます。

![chlimage_1-73](assets/chlimage_1-73.png)

アイコンが表しているエクスペリエンスの種類（Web サイト、モバイルアプリケーションまたは公開物）を示します。エクスペリエンスを追加するには、「+」記号をクリックするか、「**エクスペリエンスを追加**」をクリックして、エクスペリエンスの種類を選択します。

![chlimage_1-74](assets/chlimage_1-74.png)

サムネイルのパスを選択し、必要に応じてエクスペリエンスのサムネイルを変更します。Experiences are grouped together in the **Experiences** tile.

### リンク {#links}

リンクタイルでは、外部リンクとプロジェクトを関連付けることができます。

![chlimage_1-75](assets/chlimage_1-75.png)

リンクにわかりやすい名前を付けたり、サムネイルを変更したりできます。

![chlimage_1-76](assets/chlimage_1-76.png)

### プロジェクト情報 {#project-info}

プロジェクト情報タイルには、説明、プロジェクトステータス（非アクティブまたはアクティブ）、期限、メンバーなどプロジェクトに関する一般的な情報が表示されます。さらに、メインのプロジェクトページに表示されるプロジェクトサムネイルを追加できます。

![chlimage_1-77](assets/chlimage_1-77.png)

チームタイルと同様に、このタイルからチームメンバーを割り当てたり、削除したり（または役割を変更したり）できます。

![chlimage_1-78](assets/chlimage_1-78.png)

### 翻訳ジョブ {#translation-job}

翻訳ジョブタイルでは、翻訳を開始したり、翻訳のステータスを表示したりもできます。翻訳を設定するには、[翻訳プロジェクトの作成](/help/assets/translation-projects.md)を参照してください。

![chlimage_1-79](assets/chlimage_1-79.png)

Click the ellipsis at the bottom of the **Translation Job** card to view the assets in the translation workflow. 翻訳ジョブリストには、アセットのメタデータとタグのエントリも表示されます。これらのエントリは、アセットのメタデータとタグも翻訳されることを意味します。

![chlimage_1-80](assets/chlimage_1-80.png)

### チーム {#team}

このタイルでは、プロジェクトチームのメンバーを指定できます。編集時に、チームメンバー名を入力して、ユーザーの役割を割り当てることができます。

![chlimage_1-81](assets/chlimage_1-81.png)

チームメンバーをチームに追加したり、チームから削除したりできます。In addition, you can edit the [user role](#userroles) assigned to the team member.

![chlimage_1-82](assets/chlimage_1-82.png)

### ランディングページ {#landing-pages}

**ランディングページ**&#x200B;タイルでは、新しいランディングページをリクエストできます。

![chlimage_1-83](assets/chlimage_1-83.png)

このワークフローについては、[ランディングページを作成ワークフロー](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)で説明します。

### 電子メール {#emails}

**電子メール**&#x200B;タイルを使用して、電子メールのリクエストを管理できます。このタイルで、電子メールをリクエストワークフローを開始します。

![chlimage_1-84](assets/chlimage_1-84.png)

詳しくは、[電子メールをリクエストワークフロー](/help/sites-authoring/projects-with-workflows.md#request-email-workflow)で説明します。

### ワークフロー {#workflows}

特定のワークフローに従うように、プロジェクトを割り当てることができます。動作しているワークフローがある場合、そのステータスがプロジェクトの&#x200B;**ワークフロー**&#x200B;タイルに表示されます。

![chlimage_1-85](assets/chlimage_1-85.png)

特定のワークフローに従うように、プロジェクトを割り当てることができます。選択したプロジェクトに応じて、使用可能なワークフローは異なります。

使用可能なワークフローについては、[プロジェクトワークフローの操作](/help/sites-authoring/projects-with-workflows.md)で説明します。

### ローンチ {#launches}

ローンチタイルには、[ローンチをリクエストワークフロー](/help/sites-authoring/projects-with-workflows.md)を使用してリクエストされたローンチがすべて表示されます。

![chlimage_1-86](assets/chlimage_1-86.png)

### タスク {#tasks}

タスクを使用して、ワークフローを含む、すべてのプロジェクト関連タスクのステータスを監視できます。Tasks are covered in detail at [Working with Tasks](/help/sites-authoring/task-content.md).

![chlimage_1-87](assets/chlimage_1-87.png)

## プロジェクトテンプレート {#project-templates}

AEMには、次の3種類のテンプレートがあらかじめ用意されています。

* 単純なプロジェクト — 他のカテゴリ（包括的）に適合しないプロジェクトのリファレンスサンプル。 3 つの基本的な役割（所有者、エディター、監視者）と 4 つのワークフロー（プロジェクト承認、ローンチをリクエスト、ランディングページをリクエスト、電子メールをリクエスト）が含まれます。
* メディアプロジェクト — メディア関連のアクティビティの参照サンプルプロジェクト。 いくつかのメディア関連プロジェクトの役割（フォトグラファー、エディター、コピーライター、デザイナー、所有者、監視者）が含まれます。また、メディアコンテンツに関連する2つのワークフロー(コピーのリクエスト（テキストのリクエストと確認）と製品撮影（製品関連の写真を管理するため）も含まれます。
* [Product Photo Shoot Project](/help/sites-authoring/managing-product-information.md) - eコマース関連の製品写真を管理するためのリファレンスサンプル。 これには、写真家、編集者、写真の再編集者、所有者、クリエイティブディレクター、ソーシャルメディアマーケター、マーケティングマネージャー、レビュー担当者およびオブザーバーの役割が含まれます。
* [翻訳プロジェクト](/help/sites-administering/translation.md) - 翻訳関連アクティビティを管理するためのリファレンスサンプルです。3 つの基本的な役割（所有者、エディター、監視者）が含まれます。これには、ワークフローユーザーインターフェイスでアクセスされる2つのワークフローが含まれます。

選択したテンプレートに基づいて、特にユーザーの役割とワークフローに関して使用可能なオプションは異なります。

## プロジェクト内のユーザーの役割 {#user-roles-in-a-project}

プロジェクトテンプレートでは様々なユーザーの役割を設定します。これらの役割は、主に次の目的に使用されます。

1. 権限。ユーザーの役割は、監視者、エディター、所有者という 3 つのカテゴリのいずれかに分類されます。例えば、写真家やコピーライターは編集者と同じ権限を持ちます。 権限によって、ユーザーがプロジェクト内のコンテンツに何をおこなえるかが決定されます。
1. ワークフロー管理。ワークフローによって、プロジェクト内のタスクに誰を割り当てるかが決定されます。タスクは、プロジェクトの役割に関連付けることができます。 例えば、タスクをフォトグラファーに割り当てると、フォトグラファーの役割を持つすべてのチームメンバーがそのタスクを取得します。

セキュリティと権限を管理するために、すべてのプロジェクトが以下のデフォルトの役割をサポートしています。

<table>
 <tbody>
  <tr>
   <td><p><strong>ロール</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
   <td><p><strong>権限</strong></p> </td>
   <td><p><strong>グループのメンバーシップ</strong></p> </td>
  </tr>
  <tr>
   <td><p>監視者</p> </td>
   <td><p>この役割のユーザーは、プロジェクトステータスなどプロジェクトの詳細を表示できます。</p> </td>
   <td><p>プロジェクトに対する読み取り専用権限</p> </td>
   <td><p>workflow-users グループ</p> </td>
  </tr>
  <tr>
   <td><p>編集者</p> </td>
   <td><p>この役割のユーザーは、プロジェクトのコンテンツをアップロードおよび編集できます。</p> <p> </p> </td>
   <td>
    <ul>
     <li>プロジェクト、関連メタデータ、関連アセットに対する読み取りおよび書き込みアクセス権</li>
     <li>撮影リストや撮影した写真をアップロードし、アセットをレビューおよび承認するための権限</li>
     <li>/etc/commerce に対する書き込み権限</li>
     <li>特定のプロジェクトに対する変更権限</li>
    </ul> </td>
   <td><p>workflow-users グループ</p> </td>
  </tr>
  <tr>
   <td><p>所有者</p> </td>
   <td><p>この役割のユーザーは、プロジェクトを開始できます。所有者は、プロジェクトを作成し、プロジェクトで作業を開始し、承認済みのアセットを実稼働フォルダに移動することもできます。 所有者は、プロジェクト内のその他すべてのタスクも表示および実行できます。</p> </td>
   <td>
    <ul>
     <li>/etc/commerce に対する書き込み権限</li>
    </ul> </td>
   <td>
    <ul>
     <li>DAM-usersグループ（プロジェクトを作成可能）</li>
     <li>プロジェクト管理者グループ（アセットの移動が可能）</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

クリエイティブプロジェクトの場合、追加の役割（フォトグラファーなど）もあります。これらの役割を使用して、特定のプロジェクト用のカスタム役割を派生させることができます。

>[!NOTE]
>
>プロジェクトを作成してユーザーを各種役割に追加すると、関連する権限を管理するために、プロジェクトに関連付けられたグループが自動的に作成されます。例えば、Myproject というプロジェクトには **Myproject Owners**、**Myproject Editors**、**Myproject Observers** という 3 つのグループがあります。ただし、プロジェクトを削除しても、これらのグループは自動的には削除されません。**ツール**／**セキュリティ**／**グループ**&#x200B;で、管理者が手動でグループを削除する必要があります。
