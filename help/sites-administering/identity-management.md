---
title: Identity Management
description: AEMでの ID 管理の内部機能について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: acb5b235-523e-4c01-9bd2-0cc2049f88e2
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 83%

---


# ID 管理{#identity-management}

Web サイトの個々の訪問者を識別できるのは、その訪問者にログインを許可する場合のみです。次に示すように、様々な理由でログイン機能が提供されます。

* [AEM Communities](/help/communities/overview.md) サイト訪問者がコミュニティにコンテンツを投稿するにはログインする必要があります。
* [閉じられたユーザーグループ](/help/sites-administering/cug.md)

  Web サイト（または Web サイト内のセクション）へのアクセスを特定の訪問者に制限することが必要な場合があります。

* [パーソナライズ機能](/help/sites-administering/personalization.md) 訪問者が web サイトへのアクセス方法に関する特定の要素を設定できるようにします。

ログイン（およびログアウト）機能は、[**プロファイル**](#profiles-and-user-accounts)&#x200B;付きのアカウントによって指定されます。プロファイルには、登録済みの訪問者（ユーザー）に関する追加情報が保持されます。実際の登録および承認のプロセスは状況によって異なります。

* Web サイトでの自己登録

  [コミュニティサイト](/help/communities/sites-console.md)は、訪問者が自身の Facebook や Twitter のアカウントから自動登録またはログインすることを許可するように設定できます。

* Web サイトからの登録のリクエスト

  閉じられたユーザーグループでは、訪問者が登録をリクエストできるようにし、ワークフローによる承認を強制的に行います。

* オーサー環境からの各アカウントの登録

  認証が必要なプロファイルの数が少ない場合は、各プロファイルを直接登録することもできます。

訪問者による登録を許可するには、一連のコンポーネントとフォームを使用して、必要な ID 情報、追加の（多くの場合、オプションです）プロファイル情報の順に収集できます。また、登録の完了後に、訪問者が送信した詳細の確認と更新を行えるようにする必要があります。

次に示す追加の機能を設定または作成できます。

* 必要なリバースレプリケーションを設定します。
* ワークフローと共にフォームを作成して、ユーザーが自身のプロファイルを削除できるようにします。

>[!NOTE]
>
>プロファイルに指定した情報を使用し、[セグメント](/help/sites-administering/campaign-segmentation.md)と[キャンペーン](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)を通じて、ターゲットとなるコンテンツをユーザーに提供することもできます。

## 登録フォーム {#registration-forms}

[フォーム](/help/sites-authoring/default-components.md#form-component)を使用すると、登録情報を収集して新しいアカウントとプロファイルを生成できます。

例えば、ユーザーは次の Geometrixx ページを使用して新しいプロファイルをリクエストできます。
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![登録フォームのサンプル](assets/registerform.png)

要求を送信すると、プロファイルページが開きます。ユーザーはこのページに個人の詳細情報を指定できます。

![サンプルプロファイルページ](assets/profilepage.png)

新しいアカウントは[ユーザーコンソール](/help/sites-administering/security.md)にも表示されます。

## ログイン {#login}

ログインコンポーネントを使用すると、ログイン情報を収集して、ログインプロセスをアクティベートできます。

これにより、訪問者には標準のフィールド（「**ユーザー名**」および「**パスワード**」）と「**ログイン**」ボタンが表示され、資格情報を入力するとログインプロセスがアクティベートされます。

例えば、ユーザーは、 **ログイン** 」オプションを使用します (Geometrixxを使用します )。

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![ログインページの例](assets/login.png)

## ログアウト {#logging-out}

ログインメカニズムと共に、ログアウトメカニズムも必要です。ログアウトの際は、Geometrixx の「**サインアウト**」オプションを使用します。

## プロファイルの確認と更新 {#viewing-and-updating-a-profile}

登録フォームによっては、訪問者の情報が自身のプロファイルに登録されます。訪問者が以降のステージでこの情報を確認および更新できるようにする必要があります。そのためには、同様のフォームを用意します。例えば、Geometrixx では次を使用します。

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

プロファイルの詳細を確認するには、 **マイプロファイル** をクリックします。例えば、 `admin` アカウント：
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

オーサー環境の [ClientContext](/help/sites-administering/client-context.md) を使用すると、別のプロファイルを確認できます（十分な権限がある場合）。

1. ページを開きます。例えば、次のようなGeometrixxページを開きます。

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. 右上隅にある「**マイプロファイル**」をクリックします。管理者など、現在のアカウントのプロファイルが表示されます。
1. **Ctrl + Alt + C** キーを押して ClientContext を開きます。
1. ClientContext の左上隅にある「**ClientContext にプロファイルを読み込み**」ボタンをクリックします。

   ![「プロファイルを読み込み」アイコン](do-not-localize/loadprofile.png)

1. ダイアログウィンドウのドロップダウンリストから別のプロファイルを選択します。例： **Alison Parker**.
1. 「**OK**」をクリックします。
1. もう一度「**マイプロファイル**」をクリックします。Alison の詳細を使用してフォームが更新されます。

   ![Alison のサンプルプロファイル](assets/profilealison.png)

1. 「**プロファイルを編集**」または「**パスワードを変更**」を使用して詳細を更新できます。

## プロファイル定義へのフィールドの追加 {#adding-fields-to-the-profile-definition}

プロファイル定義にフィールドを追加できます。 例えば、「お気に入りの色」フィールドをGeometrixxプロファイルに追加するには、次のようにします。

1. Web サイトコンソールから Geometrixx Outdoors Site／英語／ユーザー／マイプロファイルに移動します。
1. 次をダブルクリックします。 **マイプロファイル** ページを開いて編集します。
1. サイドキックの「**コンポーネント**」タブで、「**フォーム**」セクションを展開します。
1. サイドキックからフォーム（「**会社情報**」フィールドの直下）に&#x200B;**ドロップダウンリスト**&#x200B;をドラッグします。
1. **ドロップダウンリスト**&#x200B;コンポーネントをダブルクリックして設定用のダイアログを開き、次の情報を入力します。

   * **要素名** - `favoriteColor`
   * **タイトル** - `Favorite Color`
   * **項目** - 複数の色を項目として追加します。

   「**OK**」をクリックして保存します。

1. ページを閉じて **web サイト**&#x200B;コンソールに戻り、マイプロファイルページをアクティベートします。

   次回プロファイルを確認する際に、好きな色を選択できます。

   ![Alison Parker のお気に入りのカラーサンプルフィールド](assets/aparkerfavcolour.png)

   このフィールドは、関連するユーザーアカウントの **profile** セクションに保存されます。

   ![CRXDE での Alison Parker のデータ](assets/aparkercrxdelite.png)

## プロファイルの状態 {#profile-states}

ユーザー（またはユーザーのプロファイル）が *特定の状態* またはそうではありません。

そのためには、次に示す方法で、ユーザープロファイルに適切なプロパティを定義する必要があります。

* ユーザーに対する表示およびアクセスが可能
* 各プロパティに 2 つの状態を定義する
* では、定義された 2 つの状態を切り替えることができます

この定義を行うには、次の項目を使用します。

* [状態プロバイダー](#state-providers)

  特定のプロパティの 2 つの状態とその間の遷移を管理します。

* [ワークフロー](#workflows)

  状態に関連するアクションを管理します。

複数の状態を定義できます。例えば、Geometrixxには次の状態が含まれます。

* ニュースレターまたはコメントスレッドの通知を購読／購読解除
* 友人とのつながりを追加／削除

### 状態プロバイダー {#state-providers}

状態プロバイダーは、対象となるプロパティの現在の状態を、取りうる 2 つの状態のトランジションと共に管理します。

状態プロバイダーはコンポーネントとして実装されるので、プロジェクト用にカスタマイズできます。Geometrixx では、次のカスタマイズを行うことができます。

* フォーラムのトピックを購読／購読解除
* 友人を追加／削除

### ワークフロー {#workflows}

状態プロバイダーは、プロファイルのプロパティとその状態を管理します。

ワークフローは、状態に関連するアクションを実装するのに必要です。例えば、通知を購読する場合、ワークフローは実際の購読アクションを処理します。通知の購読を解除する場合、ワークフローは購読リストからのユーザーの削除を処理します。

## プロファイルとユーザーアカウント {#profiles-and-user-accounts}

プロファイルは、[ユーザーアカウント](/help/sites-administering/user-group-ac-admin.md)の一部としてコンテンツリポジトリに格納されます。

プロファイルは `/home/users/geometrixx` にあります。

![CRXDE で見たプロファイル](assets/chlimage_1-138.png)

標準インストール（オーサーまたはパブリッシュ）では、すべてのユーザーの全プロファイル情報に対する読み取りアクセス権限が全員に付与されています。全員は「*既存のすべてのユーザーとグループが自動的に含まれる組み込みのグループであり、メンバーのリストは編集できません*。」

これらのアクセス権は、次のワイルドカード ACL によって定義されます。

/home everyone allow jcr:read rep:glob = &#42;/profile&#42;

これにより、以下が可能になります。

* フォーラム、コメント、またはブログの投稿で、適切なプロファイルからの情報（アイコンやフルネームなど）を表示する
* Geometrixx のプロファイルページにリンクする

このようなアクセスが使用中のインストール環境に適していない場合は、デフォルト設定を変更できます。

これを行うには「**[アクセス制御](/help/sites-administering/user-group-ac-admin.md#access-right-management)**」タブを使用します。

![CRXDE での ACL の管理](assets/aclmanager.png)

## プロファイルコンポーネント {#profile-components}

サイトのプロファイル要件を定義するために、様々なプロファイルコンポーネントも用意されています。

### チェック済みパスワードフィールド {#checked-password-field}

このコンポーネントには、次の 2 つのフィールドがあります。

* パスワードの入力
* パスワードが正しく入力されていることを確認するためのチェック用フィールド

デフォルト設定では、コンポーネントは次のように表示されます。

![パスワードを確認ダイアログ](assets/dc_profiles_checkedpassword.png)

### プロファイルのアバター写真 {#profile-avatar-photo}

このコンポーネントを使用すると、ユーザーはアバター写真ファイルを選択してアップロードできるようになります。

![アバターセレクター](assets/dc_profiles_avatarphoto.png)

### プロファイルの詳細名 {#profile-detailed-name}

このコンポーネントを使用すると、ユーザーは詳細な名前を入力できます。

![詳細名ダイアログ](assets/dc_profiles_detailedname.png)

### プロファイルの性別 {#profile-gender}

このコンポーネントを使用すると、ユーザーは性別を入力できます。

![性別セレクター](assets/dc_profiles_gender.png)
