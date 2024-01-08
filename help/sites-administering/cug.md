---
title: 閉じられたユーザーグループの作成
description: 閉じられたユーザーグループを作成する方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 64%

---

# 閉じられたユーザーグループの作成{#creating-a-closed-user-group}

閉じられたユーザーグループ (CUG) は、公開されたインターネットサイト内に存在する特定のページへのアクセスを制限するために使用されます。 このようなページでは、割り当てられたメンバーがログインし、セキュリティ資格情報を提供する必要があります。

Web サイト内にこのような領域を設定するには、次の操作を行います。

* [クローズドユーザーグループを実際に作成して、メンバーを割り当てます](#creating-the-user-group-to-be-used)。

* [このグループを必要なページに適用](#applying-your-closed-user-group-to-content-pages)し、CUG のメンバーが使用するログインページを選択（または作成）します。CUG をコンテンツページに適用する場合にも指定します。

* [保護された領域内の少なくとも 1 つのページへの何らかの形式のリンクを作成する](#linking-to-the-cug-pages)を含めない場合、表示されません。

* [Dispatcher の設定](#configure-dispatcher-for-cugs) （使用されている場合）

>[!CAUTION]
>
>閉じられたユーザーグループ (CUG) は、常にパフォーマンスを考慮して作成する必要があります。
>
>CUG 内のユーザーとグループの数に制限はありませんが、ページ上の CUG の数が多いと、レンダリングパフォーマンスが低下する場合があります。
>
>パフォーマンステストを行う際は、CUG の影響を常に考慮する必要があります。

## 使用するユーザーグループの作成 {#creating-the-user-group-to-be-used}

閉じられたユーザーグループを作成するには：

1. AEM ホーム画面から&#x200B;**ツール - セキュリティ** に移動します。

   >[!NOTE]
   >
   >詳しくは、 [ユーザーとグループの管理](/help/sites-administering/security.md#managing-users-and-groups) ユーザーとグループの作成と設定に関する詳細は、を参照してください。

1. を選択します。 **グループ** カードを次の画面から表示します。

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. を押します。 **作成** 」ボタンをクリックして、グループを作成します。
1. 新しいグループに名前を付けます（例：`cug_access`）。

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 「**メンバー**」タブに移動して、このグループに必要なユーザーを割り当てます。

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. CUG に割り当てたユーザーを有効化します。この場合は、`cug_access` のすべてのメンバーです。
1. クローズドユーザーグループをアクティベートして、パブリッシュ環境で使用できるようにします。この場合は、`cug_access` です。

## コンテンツページへの閉じられたユーザーグループの適用 {#applying-your-closed-user-group-to-content-pages}

CUG を単一ページまたは複数ページに適用するには：

1. CUG に割り当てる制限付きセクションのルートページに移動します。
1. サムネールをクリックしてページを選択し、上部のツールバーで「**プロパティ**」を選択します。

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 次のウィンドウで、「**詳細**」タブを開きます。

1. 「**認証要件**」セクションまでスクロールします。

   1. 「**有効にする**」チェックボックスをアクティブ化します。

   1. **ログインページ**へのパスを追加します。
空白のままにした場合、標準のログインページが使用されるので、これはオプションです。

   ![CUG が追加されました](assets/cug-authentication-requirement.png)

1. 次に、「**権限**」タブへ移動し、「**閉じられたユーザーグループを編集**」を選択します。

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >「権限」タブの CUG をブループリントからライブコピーにロールアウトすることはできません。ライブコピーを設定する際には、この問題を回避してください。
   >
   >詳しくは、[このページ](closed-user-groups.md#aem-livecopy)を参照してください。

1. The **閉じられたユーザーグループを編集** ダイアログが開きます。 ここで、CUG を検索して選択し、「**保存**」でグループの選択を確認できます。 

   グループがリストに追加されます（例：グループ **cug_access**）。

   ![CUG が追加されました](assets/cug-added.png)

1. 「**保存して閉じる**」で変更を確定します。 

>[!NOTE]
>
>パブリッシュ環境におけるプロファイルおよびログイン／ログアウト用のフォームの指定については、[ID 管理](/help/sites-administering/identity-management.md)を参照してください。

## CUG ページへのリンク {#linking-to-the-cug-pages}

CUG ページへのリンクのターゲットは匿名ユーザーには表示されないので、そのようなリンクはリンクチェックによって削除されます。

この問題を回避するには、CUG 領域内のページを指す、保護されていないリダイレクトページを作成することをお勧めします。これで、ナビゲーションエントリがレンダリングされます。リンクチェックが問題の原因になることはありません。ユーザーがログイン資格情報を正しく指定した後、実際にリダイレクトページにアクセスした場合にのみ、CUG 領域内にリダイレクトされます。

## CUG 用の Dispatcher の設定 {#configure-dispatcher-for-cugs}

Dispatcher を使用している場合は、次のプロパティを持つ Dispatcher ファームを定義する必要があります。

* [virtualhosts](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#identifying-virtual-hosts-virtualhosts):CUG が適用されるページのパスに一致します。
* \sessionmanagement：以下を参照してください。
* [キャッシュ](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache):CUG が適用されるファイル専用のキャッシュディレクトリ。

### CUG 用の Dispatcher セッション管理の設定 {#configuring-dispatcher-session-management-for-cugs}

[dispatcher.any ファイルのセッション管理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement)を CUG 用に設定します。CUG ページへのアクセスがリクエストされる際に使用される認証ハンドラーで、セッション管理の設定方法を指定します。

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

1. `/directory` を定義して [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) を設定します。次に例を示します。

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#caching-when-authentication-is-used) を `0` に設定します。
