---
title: 権限管理のプリンシパルビュー
seo-title: Principal View for Permissions Management
description: 権限管理を容易にする新しいタッチ UI インターフェイスについて説明します。
seo-description: Learn about the new Touch UI interface that facilitates permissions management.
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
source-git-commit: ddd908ed8287d77d9009633399c1e0bc1a12fe1b
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 26%

---


# 権限管理のプリンシパルビュー{#principal-view-for-permissions-management}

## 概要 {#overview}

AEM 6.5 では、ユーザーとグループの権限管理が導入されています。 主な機能は従来の UI と同じですが、よりユーザーフレンドリーで効率的です。

## 使用方法 {#how-to-use}

### UI へのアクセス {#accessing-the-ui}

新しい UI ベースの権限管理には、次に示すように、セキュリティの下の権限カードを通じてアクセスします。

![権限管理 UI](assets/screen_shot_2019-03-17at63333pm.png)

新しいビューでは、権限が明示的に付与されたすべてのパスで、特定のプリンシパルの特権と制限の全体を簡単に確認できます。 これにより、

CRXDE を使用して、高度な権限および制限を管理します。 同じビューに統合されています。 表示のデフォルトは「全員」グループです。

![「全員」グループの表示](assets/unu-1.png)

ユーザーが参照するプリンシパルのタイプを選択できるフィルターがあります **ユーザー**, **グループ**&#x200B;または **すべて**&#x200B;プリンシパルを検索します。**.**

![プリンシパルのタイプの検索](assets/image2019-3-20_23-52-51.png)

### プリンシパルの権限の表示 {#viewing-permissions-for-a-principal}

左側のフレームを使用すると、下にスクロールしてプリンシパルを探したり、選択したフィルターに基づいてグループまたはユーザーを検索したりできます（下図を参照）。

![プリンシパルの権限の表示](assets/doi-1.png)

名前をクリックすると、割り当てられた権限が右側に表示されます。 権限ウィンドウには、特定のパスのアクセス制御エントリのリストと、設定された制限が表示されます。

![ACL リストを表示](assets/trei-1.png)

### プリンシパルの新しいアクセス制御エントリの追加 {#adding-new-access-control-entry-for-a-principal}

新しい権限は、「ACE を追加」ボタンをクリックして、新しいアクセス制御エントリを追加することで追加できます。

![プリンシパルに新しい ACL を追加](assets/patru.png)

これにより、以下のウィンドウが表示されます。次の手順では、許可を設定する必要があるパスを選択します。

![権限パスの設定](assets/cinci-1.png)

ここでは、**dam-users** にアクセス権を設定したいパスを選択します。

![dam-users の設定例](assets/sase-1.png)

パスが選択された後、ワークフローはこの画面に戻るので、以下に示すように、利用可能な名前空間（`jcr`、`rep`、`crx` など）から 1 つ以上の権限を選択します。

権限は、テキストフィールドを使用して検索し、リストから選択することで追加できます。

>[!NOTE]
>
>権限と説明の完全なリストについては、 [このページ](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![特定のパスの検索権限](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

権限のリストを選択したら、ユーザーは「権限タイプ」を選択できます。拒否または許可（下図を参照）

![権限を選択](assets/screen_shot_2019-03-17at63938pm.png) ![権限を選択](assets/screen_shot_2019-03-17at63947pm.png)

### 制限の使用 {#using-restrictions}

この画面では、特定のパスの権限のリストと権限の種類に加えて、次に示すように、詳細なアクセス制御の制限を追加することもできます。

![制限を追加](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>各制限の意味について詳しくは、 [Jackrabbit Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)を参照してください。

以下に示すように、制限のタイプを選択し、値を入力して、 **+** アイコン

![制限タイプの追加](assets/sapte-1.png) ![制限タイプの追加](assets/opt-1.png)

新しい ACE は、次に示すように、アクセス制御リストに反映されます。 `jcr:write` は、上で追加された `jcr:removeNode` を含む集計権限ですが、`jcr:write` でカバーされているので、下に表示されません。

### ACE の編集 {#editing-aces}

アクセス制御エントリは、プリンシパルを選択し、編集する ACE を選択することで編集できます。

例えば、ここでは、以下のエントリを **dam-users** 右側の鉛筆アイコンをクリックします。

![制限を追加](assets/image2019-3-21_0-35-39.png)

編集画面には事前に選択された設定済み ACE が表示されます。これらは ACE の横にある × アイコンをクリックすると削除できます。また、下に示すように、指定したパスに新しい権限を追加できます。

![エントリを編集](assets/noua-1.png)

ここでは、与えられたパス上の `addChildNodes`dam-users **に** の権限を追加しています。

![権限を追加](assets/image2019-3-21_0-45-35.png)

変更は、 **保存** ボタンを右上に置き、変更が **dam-users** を次に示します。

![変更を保存](assets/zece-1.png)

### ACE の削除 {#deleting-aces}

アクセス制御エントリを削除して、特定のパス上のプリンシパルに与えられているすべての権限を削除できます。 ACE の横にある X アイコンを使用して、次に示すように ACE を削除できます。

![ACE を削除](assets/image2019-3-21_0-53-19.png) ![ACE を削除](assets/unspe.png)

### クラシック UI 権限の組み合わせ {#classic-ui-privilege-combinations}

新しい権限 UI では、付与された基本的な権限が真に反映されていない事前定義の組み合わせの代わりに、基本的な権限のセットが明示的に使用されることに注意してください。

その結果、設定内容に関して混乱が生じました。 次の表に、クラシック UI の権限の組み合わせと、それらを構成する実際の権限とのマッピングを示します。

<table>
 <tbody>
  <tr>
   <th>クラシック UI 権限の組み合わせ</th>
   <th>権限 UI 権限</th>
  </tr>
  <tr>
   <td>読み取り</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>変更</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>作成</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>削除</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>ACL 読み取り</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>ACL 編集</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>レプリケーション</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
