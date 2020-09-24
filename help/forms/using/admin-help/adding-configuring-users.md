---
title: 'ユーザーの追加および設定 '
seo-title: 'ユーザーの追加および設定 '
description: 管理コンソールの User Management 設定では、ユーザーの作成または削除、および他のユーザー設定を行うことができます。
seo-description: 管理コンソールの User Management 設定では、ユーザーの作成または削除、および他のユーザー設定を行うことができます。
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 74%

---


# ユーザーの追加および設定 {#adding-and-configuring-users}

ユーザーおよびグループの情報は、LDAP ディレクトリなどのサードパーティのストレージシステムで保持されます。User Management では、サードパーティのストレージシステムに対する書き込みは行われません。代わりに、ユーザーおよびグループの情報が User Management 独自のデータベースと同期されます。

## ユーザーの作成 {#create-a-user}

ユーザーの作成時に、ユーザーをグループに追加したりユーザーにロールをアサインしたりすることができます。

1. In administration console, click **[!UICONTROL Settings > User Management > Users and Groups]**, and click **[!UICONTROL New User]**.
.
1. Under **[!UICONTROL General Settings]**, provide information as required, and then click **[!UICONTROL Next]**. この設定について詳しくは、[ユーザー設定](adding-configuring-users.md#user-settings)を参照してください。
1. (Optional) To add the user to a group, click **[!UICONTROL Find Groups]**, and do these tasks:

   * In the **[!UICONTROL Find]** box, type all or part of the group name.
   * Select the domain to search, select the number of items to display, and click **[!UICONTROL Find]**.
   * (Optional) To view group details, select the group name, and then click **[!UICONTROL OK]** to return to the search results page.
   * Select the check box for the group and click **[!UICONTROL OK]**.
   * 「**[!UICONTROL 次へ]**」をクリックします。

1. (Optional) To assign roles to the user, click **[!UICONTROL Find Roles]**, select the check box for the roles to assign, and then click **[!UICONTROL OK]**.
1. 「**[!UICONTROL Finish]**」をクリックします。

   >[!NOTE]
   >
   >ユーザーのログイン問題が生じた場合は、[JEE 上の AEM Forms ユーザーが AEM Forms に OSGi サイドでログインできない](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html)を参照してください。

## ユーザー設定 {#user-settings}

ユーザーを作成または編集するときは、以下の設定を指定します。

**正規名：**（必須）ユーザーの固有の識別子。ドメイン内のユーザーおよびグループは、固有の正規名を持つ必要があります。「システムで自動的に生成する」チェックボックスを選択して User Management が一意な値を割り当てるようにするか、このチェックボックスの選択を解除して「正規名」にカスタム値を指定します。

例えば `sample_user` のように、正規名にアンダースコア文字（_）を使用するのは避けてください。正規名に基づいてユーザーを検索する場合、アンダースコア文字を含む正規名は返されません。

**名：**（必須）ユーザーの名

**姓：**（必須）ユーザーの姓

**共通名：**&#x200B;ユーザーのフルネームまたは表示名。例えば、「名」が Gloria で「姓」が Rios の場合、「共通名」は Gloria Rios です。

**電子メール：**&#x200B;ユーザーの電子メールアドレス

**電話番号：**&#x200B;ユーザーの電話番号

**説明：**&#x200B;オプションの説明。組織のニーズに合わせて、このフィールドを使用します。

**住所：**&#x200B;ユーザーの住所

**組織：**&#x200B;ユーザーが所属する組織

**電子メールエイリアス：**&#x200B;ユーザーの電子メールエイリアス。電子メールエイリアスはコンマで区切ります。

**ドメイン：**&#x200B;ユーザーが所属するドメイン

**ロケール：**&#x200B;ユーザーの ISO ロケール

**業務カレンダーキー：**&#x200B;この設定の値に基づいて、業務カレンダーをユーザーにマップできます。業務カレンダーによって稼働日と非稼働日が定義されます。AEM Forms では、リマインダー、デッドラインおよびエスカレーションなどのイベントの今後の日付や時間を計算するときに、この業務カレンダーを使用できます。業務カレンダーキーをユーザーに割り当てる方法は、エンタープライズドメイン、ローカルドメイン、ハイブリッドドメインを使用しているかどうかによって異なります（[ドメインの追加](/help/forms/using/admin-help/adding-domains.md#adding-domains)を参照）。

ローカルドメインまたはハイブリッドドメインを使用している場合は、ユーザーに関する情報は、User Management データベースにのみ保存されます。これらのユーザーについては、業務カレンダーキーを文字列に設定します。その後、業務カレンダーキー（文字列）を forms ワークフローの業務カレンダーにマップします。

エンタープライズドメインを使用している場合、ユーザーに関する情報は、LDAP ディレクトリなど、サードパーティのストレージシステムに格納されます。User Management によって、ディレクトリのユーザー情報が User Management データベースと同期されます。この機能によって、業務カレンダーキーを LDAP ディレクトリのフィールドにマップできるようになります。例えば、ディレクトリ内の各ユーザーレコードに「国」フィールドがあり、ユーザーの所在地に基づいて業務カレンダーを割り当てるとします。この場合、「国」フィールド名を業務カレンダー設定の値として指定します。その後、業務カレンダーキー（LDAP ディレクトリの「国」フィールドに対して定義された値）を forms ワークフローの業務カレンダーにマップできます。

業務カレンダーキーを業務カレンダーにマップする方法など、業務カレンダーの追加情報については、[業務カレンダーの設定](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars)を参照してください。

名前は 53 文字未満に制限します。名前を短くすると、管理コンソールの forms ワークフローページに業務カレンダーキーを表示する際の問題を防ぐことができます。

**ユーザー ID：**（必須）ユーザーがログインに使用するユーザー ID。ユーザー ID は、大文字と小文字が区別されません。また、ドメイン全体で一意である必要があります。

エンタープライズドメインでは、ユーザーの DN はユーザーが組織内の別の部署に移動すると変更される場合があるので、ユーザー ID として DN 以外の属性を使用します。この設定は、ディレクトリサーバーによって異なります。The value is `objectGUID` for Active Directory 2003, `nsuniqueID` for Sun™ One, and `guid` for eDirectory.

ユーザー ID が一意であることを確認します。削除したユーザーに割り当てられていたユーザー ID は使用しないでください。

AEM Forms は、ユーザー ID およびパスワードが同一で所属ドメインの異なるユーザーアカウントを区別できません。この問題を回避するには、ユーザー ID の同じアカウントを複数のドメインで作成しないでください。

SQL Server をデータベースとして使用する場合は、作成できるユーザー ID は最大 255 文字です。

MySQL を使用する場合は、ユーザー ID に拡張文字が含まれることがあります。ただし、abcde と âbcdè のような 2 つの文字列を比較すると、同じものと判断されます。例えば、同期を行う場合、データベースに新しいユーザーが追加されていると、同一のユーザー ID を持つユーザーがデータベースに存在するかどうかを調べるために比較が行われます。データベースにユーザー *abcde* が存在する場合に、新しいユーザー *âbcdè* を追加すると、比較ではこの 2 つの名前を区別することはできません。データベースには既に同じ名前のユーザーが追加されているものと見なされ、新しいユーザーは無視されて追加されません。

番号記号（#）で始まるユーザー名は作成しないでください。タスク検索を実行した場合、こうしたユーザー名については結果が返されません（[タスクの使用](/help/forms/using/admin-help/tasks.md#working-with-tasks)を参照）。

**パスワードおよびパスワードの確認：**&#x200B;ユーザーがログインに使用するパスワード。パスワードは最低 8 文字必要です。ハイブリッドドメインの一部であるユーザーにはパスワードは必要ありません。

## ユーザーに関する詳細の表示 {#view-details-about-a-user}

1. 管理コンソールで、設定／User Management／ユーザーとグループをクリックします。
1. 検索条件を絞り込む情報を指定し、「イン」リストで「ユーザー」を選択し、「検索」をクリックします。検索の結果がページの下部に表示されます。列見出しをクリックすると、リストを並べ替えることができます。
1. 詳細を表示するユーザーの名前をクリックします。ユーザーを編集ページに、ユーザーに関する以下のような詳細が表示されます。

   * 名前、電子メール、住所、ドメイン、組織などの全般的な識別情報
   * ユーザーにアサインされたロール
   * ユーザーが属しているグループ

## ローカルユーザーのパスワードの変更 {#change-the-password-for-a-local-user}

1. In administration console, click **[!UICONTROL Settings > User Management > Users and Groups]**.
1. Specify information to narrow the search for a particular user and click **[!UICONTROL Find]**. 検索の結果がページの下部に表示されます。列見出しをクリックすると、リストを並べ替えることができます。
1. Click the name of the user and then click **[!UICONTROL Change Password]**.
1. Type and confirm the new password, and then click **[!UICONTROL OK]**. パスワードは最低 8 文字必要です。

## ユーザーのプロパティの編集 {#edit-a-user-s-properties}

1. In administration console, click **[!UICONTROL Settings > User Management > Users and Groups]**.
1. 編集するユーザーを検索するには、次のタスクを実行します。

   * In the **[!UICONTROL Find]** box, type your search criteria.
   * In the **[!UICONTROL Using]** list, select **[!UICONTROL Name]**, **[!UICONTROL Email]**, or **[!UICONTROL User ID]**.
   * In the **[!UICONTROL In list]**, select **[!UICONTROL Users]**.
   * Select the domain, select the number of items to display, and then click **[!UICONTROL Find]**.

1. 編集するユーザーをクリックします。
1. For a user who is part of a local or hybrid domain, on the **[!UICONTROL Detail]** tab, edit the **[!UICONTROL General Settings]** and **[!UICONTROL Login Settings]**, and click **[!UICONTROL Save]**. この設定について詳しくは、[ユーザー設定](adding-configuring-users.md#user-settings)を参照してください。エンタープライズドメインに属するユーザーの一般設定およびログイン設定は、編集できません。
1. To edit the group settings for the user, click the **[!UICONTROL Group Membership]** tab and do these tasks:

   * Click **[!UICONTROL Find Group]** and complete the search information.
   * To add the user to a new group, select the check box for the group, click **[!UICONTROL OK]**, and then click **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >ローカルユーザーをディレクトリグループに追加することはできません。ただし、ディレクトリユーザーをローカルグループに追加することはできます。

   * To remove the user from a group, select the check box for the group, click **[!UICONTROL Delete]**, and then click **[!UICONTROL Save]**.


1. To edit the user’s roles, click the **[!UICONTROL Role Assignments]** tab and do these tasks:

   * To display a list of roles, click **[!UICONTROL Find Roles]**.
   * To add a role, select the check box for the role, click **[!UICONTROL OK]**, and then click **[!UICONTROL Save]**.
   * To remove a role, select the check box for the role, click **[!UICONTROL Unassign]**, and then click **[!UICONTROL Save]**.

## ユーザーの削除 {#delete-a-user}

1. In administration console, click **[!UICONTROL Settings > User Management > Users and Groups]**.
1. 削除するユーザーを検索するには、次のタスクを実行します。

   * In the **[!UICONTROL Find]** box, type your search criteria.
   * In the **[!UICONTROL Using]** list, select **[!UICONTROL Name]**, **[!UICONTROL Email]**, or **[!UICONTROL User ID]**.
   * In the **[!UICONTROL In list]**, select **[!UICONTROL Users]**.
   * Select the domain, select the number of items to display, and then click **[!UICONTROL Find]**.

1. Select the check box for the user, click **[!UICONTROL Delete]**, and then click **[!UICONTROL OK]**.

>[!NOTE]
>
>JEE 上の AEM Forms では、OSGi で実行されている AEM Forms アドオンのユーザーを AEM ユーザーとして認識できます。これは、JEE 上の AEM Forms と OSGi で実行されている AEM Forms アドオンの間でシングルサインオンが必要となるシナリオでは必須です（例えば、HTML Workspace など）。上述の削除操作では、JEE 上の AEM Forms からのみユーザーが削除されます。OSGi 環境で実行されている AEM Forms アドオンからユーザーは削除されません。しかし、ユーザーを削除した後で JEE サーバー上の AEM Forms アドオンまたは OSGi 環境の AEM Forms アドオンにログインしようとすると、拒否されます。

## カスタムのログインエラーハンドラを作成する {#create-custom-login-error-handler}

必要な AEM Forms および CQ の権限を持たないユーザーが次の CQ に埋め込まれた AEM Forms アプリケーションにログインしようとすると、ユーザーは次のエラートレースを含むデフォルトの CQ 404 ページにリダイレクトされます。

* Correspondence Management Solution
* AEM Forms Workspace

   ***注意&#x200B;**：AEM Forms のリリースでは Flex Workspace は廃止されています。*

* Forms Manager
* プロセスレポート

CQ にはデフォルトの 404 ハンドラ jsp を上書きするメカニズムが提供されています。

エラーハンドリングページのカスタマイズ方法については、Adobe Experience Manager 文書の「[エラーハンドラーによって表示されるページのカスタマイズ](https://docs.adobe.com/docs/en/cq/current/developing/customizing_error_handler_pages.html)」を参照してください。
