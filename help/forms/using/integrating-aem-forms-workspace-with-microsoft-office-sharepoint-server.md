---
title: AEM Forms Workspace に Microsoft Office SharePoint Server を統合する
description: AEM Forms Workspace に Microsoft Office SharePoint Server を統合することができます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '551'
ht-degree: 100%

---

# AEM Forms Workspace に Microsoft Office SharePoint Server を統合する{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- 要件**

**必要な知識**
AEM Forms Workspace を SharePoint Server に追加するに当たり、SharePoint Server への適切なアクセス権を持っている必要があります。また、Workspace にアクセスするための URL を把握している必要もあります。以下の手順では、SharePoint Server に精通していることを前提としています。SharePoint Server 内の web パーツについて詳しくは、「Windows SharePoint Services 内の web パーツ」を参照してください。

**ユーザレベル**
初心者

AEM Forms Workspace は、Microsoft Office SharePoint Server（例えば、Microsoft Office SharePoint Server 2007）で web パーツとして使用することができます。ユーザーは、web ブラウザーから SharePoint Server に接続することで、AEM Forms Workspace にアクセスすることができます。これにより、統一されたエクスペリエンスを用意することができます。この記事では、AEM Forms Workspace を Microsoft Office SharePoint Server 内で web パーツとして表示するための、基本的な手順を説明します。この記事で説明される手順を実行することで、統一されたエクスペリエンスを用意することができます。これにより、SharePoint Server に接続する各ユーザーに対して、同じポートから AEM Forms Workspace にアクセス可能な環境を提供できます。

>[!NOTE]
>
>この資料に記載されている手順は、Microsoft SharePoint Server 2007 に特有のものです。また、他のサポート対象バージョンの Microsoft SharePoint も、HTML Workspace と統合することができます。

## AEM Forms Workspace に Microsoft Office SharePoint Server 2007 を統合する {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

次の手順を実行して、AEM Forms Workspace を web パーツに統合します。

1. Web ブラウザーから、SharePoint サイト（例：`https://[myMOSSserver]:44299/default.aspx`）を開きます。`[myMOSSserver]` は SharePoint サーバーの名前または IP アドレスです。

   >[!NOTE]
   >
   >SharePoint サーバーにおけるデフォルトのポート番号は 44299 です。ポート番号は、SharePoint Server のインストール構成によって異なります。

1. Web ページの右上で「**サイトの操作**」をクリックし、「**ページの編集**」を選択します。
1. 「**Web パーツの追加**」ボタンをクリックします。
1. 「その他」の下に表示される「web パーツの追加：web ページダイアログ」のダイアログボックスで、「**ページビューアの web パーツ**」を選択し、「**追加**」をクリックします。
1. 「ページビューアの web パーツ」ボックスで「**編集**」をクリックし、「**共有 web パーツの変更**」を選択します。

   >[!NOTE]
   >
   >手順 3 でクリックした「**web パーツの追加**」ボタンの下に「ページビューアの web パーツ」ボックスが表示されます（次の図 1 を参照）。

   ![Microsoft Office SharePoint Server の「ページビューアの web パーツ」ボックス。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   図 1：- Microsoft Office SharePoint サーバーの「ページビューアの web パーツ」ボックス。

1. 「ページビューア」ページで、次のタスクを実行します。

   1. 「リンク」ボックスで、AEM Forms Workspace の URL（例：`https://[AEM_forms_Server]:8080/lc/ws`）を入力します。`[AEM_forms_Server]` は、AEM Forms サーバーの IP または名前を表します。
   1. 「**表示方法**」をクリックします。高さ、幅、およびタイトルを変更し、ワークスペースのユーザーインターフェイス全体が表示されるようにします。例えば、高さと幅をそれぞれ 6 インチと 11 インチに設定することができます。
   1. 「**リンクのテスト**」をクリックします。新しい web ブラウザーのウィンドウが起動し、Workspace が表示されます。
   1. （オプション）「**Layout**」をクリックして、web パーツ内のワークスペースレイアウトを変更します。
   1. （オプション）「**詳細設定**」をクリックして、他の設定を変更します。例えば、説明の追加や、web パーツ内で Workspace を最小化したり閉じたりできる機能のオン／オフを切り替える、などの設定が可能です。

      「**適用**」をクリックします。

1. 「**編集モードを閉じる**」をクリックし、ワークスペースにアクセスできることを確認します。

上記の手順を完了すると、SharePointサイトは、次の図 2 のようになります。

![Microsoft Office SharePoint Server を統合した AEM Forms Workspace](assets/aem-forms-workspace.jpg)

図 2：Microsoft Office SharePoint Server を統合した AEM Forms Workspace
