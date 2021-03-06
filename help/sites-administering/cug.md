---
title: 閉じられたユーザーグループの作成
seo-title: Creating a Closed User Group
description: 閉じられたユーザーグループの作成方法について説明します。
seo-description: Learn how to create a Closed User Group.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 100%

---

# 閉じられたユーザーグループの作成{#creating-a-closed-user-group}

閉じられたユーザーグループ（CUG）は、公開済みのインターネットサイト内にある特定のページへのアクセスを制限するために使用します。このようなページでは、割り当て済みのメンバーがログインしてセキュリティ資格情報を指定する必要があります。

Web サイト内にこのような領域を設定するには、次の操作をおこないます。

* [クローズドユーザーグループを実際に作成して、メンバーを割り当てます](#creating-the-user-group-to-be-used)。

* [このグループを必要なページに適用](#applying-your-closed-user-group-to-content-pages)し、CUG のメンバーが使用するログインページを選択（または作成）します。CUG をコンテンツページに適用する場合にも指定します。

* [保護された領域内にある少なくとも 1 つのページへのリンクを作成](#linking-to-the-realm)します。リンクを作成しないとページが表示されません。
* [Dispatcher を設定](#configure-dispatcher-for-cugs)します（使用する場合）。

>[!CAUTION]
>
>閉じられたユーザーグループ（CUG）を作成する場合は、パフォーマンスに留意してください。
>
>CUG 内のユーザーとグループの数に制限はありませんが、ページ上の CUG の数が増えると、レンダリングパフォーマンスが低下する可能性があります。
>
>パフォーマンステストをおこなうときは、CUG の影響を常に考慮してください。

## 使用するユーザーグループの作成 {#creating-the-user-group-to-be-used}

閉じられたユーザーグループを作成するには：

1. AEM ホーム画面から&#x200B;**ツール - セキュリティ** に移動します。

   >[!NOTE]
   >
   >ユーザーとグループの作成および設定について詳しくは、[ユーザーとグループの管理](/help/sites-administering/security.md#managing-users-and-groups)を参照してください。

1. 次の画面から&#x200B;**グループ**&#x200B;カードを選択します。

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 新しいグループを作成するには、右上隅にある「**作成**」ボタンをクリックします。
1. 新しいグループに名前を付けます（例：`cug_access`）。

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 「**メンバー**」タブに移動して、このグループに必要なユーザーを割り当てます。

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. CUG に割り当てたユーザーを有効化します。この場合は、`cug_access` のすべてのメンバーです。
1. クローズドユーザーグループをアクティベートして、パブリッシュ環境で使用できるようにします。この場合は、`cug_access` です。

## コンテンツページへの閉じられたユーザーグループの適用 {#applying-your-closed-user-group-to-content-pages}

CUG をページに適用するには：

1. CUG に割り当てる制限付きセクションのルートページに移動します。
1. サムネイルをクリックしてページを選択し、上部パネルの「**プロパティ**」をクリックします。

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 次のウィンドウで、「**詳細**」タブに移動します。
1. 下にスクロールして、「**認証要件**」セクションのチェックボックスをオンにします。

1. 以下の設定パスを追加して、「保存」を押します。
1. 次に「**権限**」タブへ移動し、「**クローズドユーザーグループの編集**」ボタンを押します。

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[注]
   >
   > 「権限」タブの CUG をブループリントからライブコピーにロールアウトすることはできません。ライブコピーを設定する際には、この点を考慮してください。
   >
   > 詳しくは、[このページ](closed-user-groups.md#aem-livecopy)を参照してください。

1. 次のウィンドウで CUG を探して追加します。この場合は、**cug_access** という名前のグループを追加します。最後に、「**保存**」を押します。
1. 「**有効**」をクリックして、このページ（およびすべての子ページ）が CUG に属することを定義します。
1. グループのメンバーが使用する&#x200B;**ログインページ**&#x200B;を指定します。次に例を示します。

   `/content/geometrixx/en/toolbar/login.html`

   このページは省略可能です。空白のままにすると、標準のログインページが使用されます。

1. 「**許可されたグループ**」を追加します。+ を使用してグループを追加し、- を使用して削除します。ページにログインおよびアクセスできるのは、これらのグループのメンバーのみです。
1. 必要に応じて、「**領域**」（ページのグループの名前）を割り当てます。ページタイトルを使用する場合は空のままにします。
1. 「**OK**」をクリックして、指定した内容を保存します。

パブリッシュ環境におけるプロファイルおよびログイン／ログアウト用のフォームの指定については、[ID 管理](/help/sites-administering/identity-management.md)を参照してください。

## 領域へのリンク {#linking-to-the-realm}

CUG 領域へのリンクのターゲットは匿名ユーザーには表示されないので、そのようなリンクはリンクチェックによって削除されます。

この問題を回避するには、CUG 領域内のページを指す、保護されていないリダイレクトページを作成することをお勧めします。これで、ナビゲーションエントリがレンダリングされます。リンクチェックが問題の原因になることはありません。ユーザーがログイン資格情報を正しく指定した後、実際にリダイレクトページにアクセスした場合にのみ、CUG 領域内にリダイレクトされます。

## CUG 用の Dispatcher の設定 {#configure-dispatcher-for-cugs}

Dispatcher を使用する場合は、次のプロパティを使用して Dispatcher ファームを定義する必要があります。

* [virtualhosts](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts)：CUG が適用されたページのパスに一致します。
* \sessionmanagement：以下を参照してください。
* [cache](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache)：CUG が適用されたファイル専用のキャッシュディレクトリです。

### CUG 用の Dispatcher セッション管理の設定 {#configuring-dispatcher-session-management-for-cugs}

[dispatcher.any ファイルのセッション管理](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement)を CUG 用に設定します。CUG ページへのアクセスがリクエストされる際に使用される認証ハンドラーで、セッション管理の設定方法を指定します。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Dispatcher ファームでセッション管理が有効になっている場合、ファームが処理するすべてのページはキャッシュされません。CUG の外にあるページをキャッシュするには、CUG 以外のページを処理する 2 つ目のファームを dispatcher.any に
>作成します。

1. `/directory` を定義して [/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) を設定します。次に例を示します。

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. [/allowAuthorized](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used) を `0` に設定します。
