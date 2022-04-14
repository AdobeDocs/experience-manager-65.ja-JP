---
title: AEM 基盤における GDPR 要件の取り扱い
seo-title: Handling GDPR Requests for the AEM Foundation
description: AEM 基盤における GDPR 要件の取り扱い
seo-description: null
uuid: d470061c-bbcf-4d86-9ce3-6f24a764ca39
contentOwner: sarchiz
discoiquuid: 8ee843b6-8cea-45fc-be6c-99c043f075d4
exl-id: 411d40ab-6be8-4658-87f6-74d2ac1a4913
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '435'
ht-degree: 100%

---

# AEM 基盤における GDPR 要件の取り扱い{#handling-gdpr-requests-for-the-aem-foundation}

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制（GDPR、CCPA など）に適用できます。

## AEM 基盤の GDPR サポート {#aem-foundation-gdpr-support}

AEM 基盤のレベルでは、保存される個人データはユーザープロファイルです。そのため、この記事では主に、GDPR のアクセスリクエストと削除リクエストに対処できるように、ユーザープロファイルのアクセス方法と削除方法について説明します。

## ユーザープロファイルへのアクセス {#accessing-a-user-profile}

### 手動の手順 {#manual-steps}

1. **[!UICONTROL 設定／セキュリティ／ユーザー]**&#x200B;を参照するか、または `https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html` を直接参照して、ユーザー管理コンソールを開きます。

   ![useradmin2](assets/useradmin2.png)

1. 次に、ページの上部にある検索バーに目的のユーザーの名前を入力して検索します。

   ![usersearch](assets/usersearch.png)

1. 最後に、ユーザープロファイルをクリックして開き、「**[!UICONTROL 詳細]**」タブで情報を確認します。

   ![userprofile_small](assets/userprofile_small.png)

### HTTP API {#http-api}

前述したように、自動化を促進するために、ユーザーデータにアクセスするための API が用意されています。利用可能な API には、以下のようにいくつかのタイプがあります。

**UserProperties API**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

*ユーザーホームの検索：*

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

*ユーザーデータの取得*

上記のコマンドで返された JSON ペイロードの home プロパティに含まれているノードパスの使用

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## ユーザーの無効化と関連プロファイルの削除 {#disabling-a-user-and-deleting-the-associated-profiles}

### ユーザーの無効化 {#disable-user}

1. 前述のように、ユーザー管理コンソールを開き、目的のユーザーを検索します。
1. ユーザーの上にマウスポインターを置き、選択アイコンをクリックします。プロファイルがグレーに変わり、選択されたことが示されます。

1. 上部のメニューの「無効にする」ボタンをクリックして、このユーザーを無効にします。

   ![userdisable](assets/userdisable.png)

1. 最後に、アクションを確認します。

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   次のように、プロファイルカードがグレーアウトされてロックが追加されるので、ユーザーのアクティベートが解除されたことがわかります。

   ![disableduser](assets/disableduser.png)

### ユーザープロファイル情報の削除 {#delete-user-profile-information}

1. CRXDE Lite にログインし、`[!UICONTROL userId]` を検索します。

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. `[!UICONTROL /home/users]` にデフォルトで配置されているユーザーノードを開きます。

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. プロファイルノードとそのすべての子ノードを削除します。プロファイルノードには、AEM のバージョンに応じて以下の 2 種類の形式があります。

   1. `[!UICONTROL /profile]` のデフォルトの非公開プロファイル
   1. `[!UICONTROL /profiles]`（AEM 6.5 を使用して作成された新しいプロファイル用）

   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### HTTP API {#http-api-1}

以下の手順では、`curl` コマンドラインツールを使用して **[!UICONTROL cavery]** `userId` を持つユーザーを無効化し、デフォルトの場所にあるそのユーザーのプロファイルを削除する方法を示します。

* *ユーザーホームの検索*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *ユーザーの無効化*

上記のコマンドから返された JSON ペイロードの home プロパティに含まれているノードパスを使用：

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *ユーザープロファイルの削除*

アカウント検索コマンドから返された JSON ペイロードの home プロパティに含まれているノードパス、および既知のデフォルトのプロファイルノード位置を使用：

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
