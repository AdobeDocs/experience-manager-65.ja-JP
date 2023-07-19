---
title: Cookie の使用法の設定
seo-title: Configuring Cookie Usage
description: AEM では、Web ページでの Cookie の使用方法を設定および制御できるサービスを提供しています
seo-description: AEM provides a service that enables you to configure and control how cookies are used with your web pages
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 29%

---

# Cookie の使用法の設定{#configuring-cookie-usage}

AEM では、Web ページでの Cookie の使用方法を設定および制御できるサービスを提供しています:

* 設定可能なサーバー側のサービスは、使用可能な Cookie のリストを維持します。
* JavaScript API を使用すると、JavaScript コードで cookie が使用できることを検証できます。

この機能を使用して、ページが cookie の使用に関するユーザーの同意に従うようにします。

## 許可される cookie の設定 {#configuring-allowed-cookies}

AdobeGranite オプトアウトサービスを設定して、Web ページでの Cookie の使用方法を指定します。 次の表に、設定可能なプロパティを示します。

 サービスを設定するには、[Web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)を使用するか、[リポジトリに OSGi 設定を追加](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)します。次の表では、どちらの方法でも必要になるプロパティについて説明しています。OSGi 設定の場合、サービス PID は `com.adobe.granite.optout` です。

| プロパティ名（Web コンソール） | OSGi プロパティ名 | 説明 |
|---|---|---|
| オプトアウトの cookie | optout.cookies | ユーザーが Cookie の使用に同意していないことを示す Cookie の名前。ユーザーのデバイスに存在する場合。 |
| オプトアウト HTTP ヘッダー | optout.headers | 存在する場合に、ユーザーが Cookie の使用に同意していないことを示す HTTP ヘッダーの名前。 |
| ホワイトリスト Cookie | optout.whitelist.cookies | Web サイトの機能に不可欠で、ユーザーの同意なしに使用できる cookie のリスト。 |

## Cookie 使用状況の検証 {#validating-cookie-usage}

クライアント側の JavaScript を使用してAdobeGranite Opt-Out Service を呼び出し、Cookie を使用できることを確認します。 Granite.OptOutUtil javascript オブジェクトを使用して、次のタスクを実行します。

* 追跡目的での Cookie の使用にユーザーが同意していないことを示す Cookie 名のリストを取得します。
* 使用可能な cookie のリストを取得します。
* Web ブラウザーに、追跡に対する Cookie の使用にユーザーが同意していないことを示す Cookie が含まれているかどうかを判断します。
* 特定の cookie を使用できるかどうかを判断します。

granite.utils [クライアントライブラリフォルダー](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) には Granite.OptOutUtil オブジェクトが用意されています。 次のコードをページの head JSP に追加して、JavaScript ライブラリへのリンクを含めます。

`<ui:includeClientLib categories="granite.utils" />`

例えば、次の JavaScript 関数は、COOKIE_NAME Cookie を書き込む前に使用できるかどうかを判断します。

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## Granite.OptOutUtil JavaScript オブジェクト {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil を使用すると、Cookie の使用が許可されているかどうかを判断できます。

### getCookieNames() 関数 {#getcookienames-function}

存在する場合に、ユーザーが cookie の使用に対して同意していないことを示す cookie の名前を返します。

**パラメーター**

なし。

**戻り値**

cookie 名の配列。

#### getWhitelistCookieNames() 関数 {#getwhitelistcookienames-function}

ユーザーの同意に関係なく使用できる Cookie の名前を返します。

**パラメーター**

なし。

**戻り値**

cookie 名の配列。

#### isOptedOut() 関数 {#isoptedout-function}

ユーザーのブラウザーに、cookie の使用に対する同意が得られていないことを示す cookie が含まれているかどうかを判断します。

**パラメーター**

なし。

**戻り値**

同意がないことを示す Cookie が見つかった場合はブール値 `true`、同意がないことを示す Cookie が存在しない場合は値 `false`。

### maySetCookie(cookieName) 関数 {#maysetcookie-cookiename-function}

ユーザーのブラウザーで特定の cookie を使用できるかどうかを指定します。 この関数は、`isOptedOut` 関数と、`getWhitelistCookieNames` が返すリスト内に特定の特定の Cookie が含まれているかの判断を連結して使用する処理と同等です。

**パラメーター**

* cookieName：文字列。Cookie の名前。

**戻り値**

`cookieName` を使用できる場合はブール値 `true`、`cookieName` が使用できない場合は値 `false`。
