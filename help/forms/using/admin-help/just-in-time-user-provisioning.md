---
title: ジャストインタイムのユーザープロビジョニング
seo-title: ジャストインタイムのユーザープロビジョニング
description: ジャストインタイムのプロビジョニングを使用して、正常に認証された後でユーザーを User Management に追加し、新しいユーザーに関連するロールおよびグループを動的に割り当てます。
seo-description: ジャストインタイムのプロビジョニングを使用して、正常に認証された後でユーザーを User Management に追加し、新しいユーザーに関連するロールおよびグループを動的に割り当てます。
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 95%

---


# ジャストインタイムのユーザープロビジョニング {#just-in-time-user-provisioning}

AEM Forms では、User Management にまだ存在していないユーザーのジャストインタイムプロビジョニングをサポートしています。ジャストインタイムプロビジョニングを使用した場合、ユーザーは、秘密鍵証明書が正常に認証されると、自動的に User Management に追加されます。さらに、関連するロールおよびグループが新しいユーザーに動的にアサインされます。

## ジャストインタイムのユーザープロビジョニングの必要性 {#need-for-just-in-time-user-provisioning}

従来の認証の手順を次に示します。

1. ユーザーが AEM Forms にログインしようとすると、User Management は、使用可能なすべての認証プロバイダーにユーザーの秘密鍵証明書を連続して渡します（ログイン資格情報には、ユーザー名とパスワードの組み合わせ、Kerberos チケット、PKCS7 署名などが含まれます）。
1. 認証プロバイダーは、秘密鍵証明書を検証します。
1. 認証プロバイダーは、次に、ユーザーが User Management データベースに存在するかどうかを確認します。可能性のある結果を次に示します。

   **存在する：** ユーザーが最新でロック解除されている場合、User Managementは認証成功を返します。 これに対して、ユーザーが登録されていないか、またはロックされている場合、User Management は認証失敗を返します。

   **存在しない：** User Managementは、認証失敗を返します。

   **無効：** User Managementは、認証失敗を返します。

1. 認証プロバイダーが返した結果が評価されます。認証プロバイダーが認証成功を返した場合、ユーザーのログインが許可されます。そうでない場合は、User Management は次の認証プロバイダーに対して確認（手順 2～3）を行います。
1. ユーザーの秘密鍵証明書を検証する利用可能な認証プロバイダーがなくなると、認証の失敗が返されます。

ジャストインタイムプロビジョニングが実装されているときに、認証プロバイダーの 1 つがユーザーの秘密鍵証明書を検証すると、新しいユーザーが User Management 内に動的に作成されます（上記、従来の認証手順 3 の後）。

## ジャストインタイムのユーザープロビジョニングの実装 {#implement-just-in-time-user-provisioning}

### ジャストインタイムプロビジョニングの API {#apis-for-just-in-time-provisioning}

AEM Forms で提供するジャストインタイムプロビジョニングの API を次に示します。

```java
package com.adobe.idp.um.spi.authentication  ;
publ ic interface IdentityCreator {
/**
* Tries  to create a user with the  in formation  provided in the <code>UserProvisioningBO</code> object.
* If the user is successfully created, a valid AuthResponse is returned along with the information using which the user was created.
* It is the responsibility of the IdentityCreator to set the User obje ct  in the cre dential map with th e  ke y  <code>UMA u thenticationUtil.authenticatedUserKey</code>
* The credentials are available in the <code>UserProvisioningBO</code> object in the 'credentials' property.
* If the IdentityCreator is unable to create a user due to any reason, it returns <code>null</code>
* @param userBO An object of <code>com.adobe. i dp.um . spi.authenti c ationUserProvisioningBO</code>
* @return */public AuthResponse create(UserProvisioningBO userBO);
/**
* Returns the name of the IdentityCreator which will be registered in preferences.
* This name is used to associate the IdentityProvider with the Auth Provider Configuration in the domain.
* @return The name of the Identity Creator which is recognized in Configuration.
*/
public String getName();
}
package com.adobe.idp.um.spi.authentication;
import com.adobe.idp.um.api.infomodel.User;
public interface AssignmentProvider {
/**
* Tries to assign roles or permissions or group memberships to users created via Just-in-time provisioning.
* @param user The User created via the Just-in-time provisioning process.
* @return a Boolean flag indicating whether the assignment was successful or not.
*/
public Boolean assign(User user);
/**
* Returns the name of the AssignmentProvider through which it is registered under preferences.
* This name is used to associate the AssignmentProvider with the Auth Provider Configuration in the domain.
* @return The name of the AssignmentProvider which is recognized in Configuration.
*/public String getName();
}
```

### ジャストインタイムが有効なドメインを作成する際の考慮事項 {#considerations-while-creating-a-just-in-time-enabled-domain}

* ハイブリッドドメインのカスタム `IdentityCreator` を作成する際に、ローカルユーザーにダミーのパスワードが指定されていることを確認します。このパスワードフィールドを空白のままにしないでください。
* 推奨事項：`DomainSpecificAuthentication` を使用して、特定のドメインに対するユーザーの秘密鍵証明書を検証します。

### ジャストインタイムが有効なドメインの作成 {#create-a-just-in-time-enabled-domain}

1. 「ジャストインタイムプロビジョニングの API」にある DSC による API の実装を記述します。
1. DSC を forms サーバーにデプロイします。
1. ジャストインタイムが有効なドメインを作成します。

   * 管理コンソールで、設定／User Management／ドメインの管理／新規エンタープライズドメインをクリックします。
   * ドメインを設定し、「ジャストインタイムプロビジョニングを有効にする」を選択します<!--Fix broken link (See Setting up and managing domains).-->
   * 認証プロバイダーを追加します。認証プロバイダーを追加する際に、新規認証画面で、登録された「ID 作成者」および「割り当てプロバイダー」を選択します。

1. 新しいドメインを保存します。

## 機能の仕組み {#behind-the-scenes}

ユーザーが AEM Forms にログインを試みて、認証プロバイダーがユーザーの秘密鍵証明書を受け入れるとします。ユーザーがまだ User Management データベースに存在していない場合、ユーザーの ID 確認は失敗します。このとき、AEM Forms は次のアクションを実行します。

1. 認証データを持つ `UserProvisioningBO` オブジェクトを作成し、秘密鍵証明書マップに配置します。
1. `UserProvisioningBO` によって返されるドメイン情報に基づいて、ドメインの登録された `IdentityCreator` および `AssignmentProvider` を取得して呼び出します。
1. Invoke `IdentityCreator`. 正常な `AuthResponse` が返される場合、秘密鍵証明書マップから `UserInfo` を抽出します。ユーザー作成後のグループ／ロールアサインおよびその他の後処理のために `AssignmentProvider` に渡します。
1. ユーザーが正常に作成されると、成功としてユーザーのログイン試行を返します。
1. ハイブリッドドメインの場合、認証プロバイダーに提供された認証データからユーザー情報を引き出します。この情報が正常に取得されると、ユーザーがオンザフライで作成されます。

>[!NOTE]
>
>ジャストインタイムプロビジョニング機能は、動的にユーザーを作成するために使用できる `IdentityCreator` のデフォルトの実装に付属しています。ユーザーは、ドメインのディレクトリに関連付けられている情報を使用して作成されます。

