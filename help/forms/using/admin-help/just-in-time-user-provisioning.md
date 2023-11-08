---
title: ジャストインタイムのユーザープロビジョニング
seo-title: Just-in-time user provisioning
description: ジャストインタイムプロビジョニングを使用して、認証が正常に完了した後でユーザーを User Management に追加し、新しいユーザーに関連する役割とグループを動的に割り当てます。
seo-description: Use just-in-time provisioning to add users to User Management after successfull authentication and dynamically assign relevant roles and groups to the new user.
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 33%

---

# ジャストインタイムのユーザープロビジョニング {#just-in-time-user-provisioning}

AEM forms は、User Management にまだ存在しないユーザーのジャストインタイムプロビジョニングをサポートしています。 ジャストインタイムプロビジョニングでは、ユーザーの資格情報が正常に認証されると、ユーザーは User Management に自動的に追加されます。 さらに、関連する役割とグループが新しいユーザーに動的に割り当てられます。

## ジャストインタイムのユーザープロビジョニングが必要 {#need-for-just-in-time-user-provisioning}

従来の認証の仕組みは次のとおりです。

1. ユーザーがAEM forms にログインしようとすると、User Management はユーザーの資格情報を、使用可能なすべての認証プロバイダーに順番に渡します。 （ログイン資格情報には、ユーザー名とパスワードの組み合わせ、Kerberos チケット、PKCS7 署名などが含まれます）。
1. 認証プロバイダーが資格情報を検証します。
1. 次に、認証プロバイダーは、ユーザーが User Management データベースに存在するかどうかを確認します。 次の結果が考えられます。

   **存在する：**&#x200B;ユーザーが登録されており、ロックされていない場合、User Management は認証成功を返します。これに対して、ユーザーが登録されていないか、またはロックされている場合、User Management は認証失敗を返します。

   **存在しない：** User Management は認証失敗を返します。

   **無効：** User Management は認証失敗を返します。

1. 認証プロバイダーから返された結果が評価されます。 認証プロバイダーが認証成功を返した場合、ユーザーはログインできます。 それ以外の場合は、User Management は次の認証プロバイダー（手順 2～3）と確認します。
1. ユーザーの資格情報を検証する使用可能な認証プロバイダーがない場合は、認証失敗が返されます。

ジャストインタイムプロビジョニングを実装すると、いずれかの認証プロバイダーがユーザーの資格情報を検証すると、User Management に新しいユーザーが動的に作成されます。 （上記の従来の認証手順の手順 3 の後）。

## ジャストインタイムのユーザープロビジョニングを実装する {#implement-just-in-time-user-provisioning}

### ジャストインタイムプロビジョニング用の API {#apis-for-just-in-time-provisioning}

AEM forms は、ジャストインタイムプロビジョニング用に以下の API を提供します。

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

### ジャストインタイム対応ドメインを作成する際の考慮事項 {#considerations-while-creating-a-just-in-time-enabled-domain}

* ハイブリッドドメインのカスタム `IdentityCreator` を作成する際に、ローカルユーザーにダミーのパスワードが指定されていることを確認します。このパスワードフィールドを空白のままにしないでください。
* 推奨事項：`DomainSpecificAuthentication` を使用して、特定のドメインに対するユーザーの資格情報を検証します。

### ジャストインタイムが有効なドメインの作成 {#create-a-just-in-time-enabled-domain}

1. 「ジャストインタイムプロビジョニングの API」の節にある、DSC による API の実装を記述します。
1. DSC をForms Server にデプロイします。
1. ジャストインタイムが有効なドメインの作成:

   * 管理コンソールで、設定/User Management/ドメイン管理/新しいエンタープライズドメインをクリックします。
   * ドメインを設定し、「ジャストインタイムプロビジョニングを有効にする」を選択します。 <!--Fix broken link (See Setting up and managing domains).-->
   * 認証プロバイダーを追加します。 認証プロバイダーを追加する際に、新しい認証画面で、登録されている ID 作成者と割り当てプロバイダーを選択します。

1. 新しいドメインを保存します。

## 舞台裏 {#behind-the-scenes}

ユーザーがAEM forms にログインしようとしていて、認証プロバイダーがユーザーの資格情報を受け入れたとします。 ユーザーが User Management データベースにまだ存在しない場合、そのユーザーの ID チェックは失敗します。 AEM forms では、次のアクションが実行されるようになりました。

1. 認証データを持つ `UserProvisioningBO` オブジェクトを作成し、資格情報マップに配置します。
1. `UserProvisioningBO` によって返されるドメイン情報に基づいて、ドメインの登録された `IdentityCreator` および `AssignmentProvider` を取得して呼び出します。
1. `IdentityCreator`を呼び出します。正常な `AuthResponse` が返される場合、資格情報マップから `UserInfo` を抽出します。ユーザー作成後のグループ／ロールアサインおよびその他の後処理のために `AssignmentProvider` に渡します。
1. ユーザーが正常に作成された場合は、成功したとユーザーによるログイン試行を返します。
1. ハイブリッドドメインの場合、認証プロバイダーに提供される認証データからユーザー情報を取り込みます。 この情報が正常に取得された場合は、その場でユーザーを作成します。

>[!NOTE]
>
>ジャストインタイムプロビジョニング機能は、動的にユーザーを作成するために使用できる `IdentityCreator` のデフォルトの実装に付属しています。ユーザーは、ドメインのディレクトリに関連付けられている情報を使用して作成されます。
