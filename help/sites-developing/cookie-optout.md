---
title: Cookie の使用法の設定
description: AEM では、web ページでの Cookie の使用方法を設定および制御できるサービスが提供されています。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 100%

---

# Cookie の使用法の設定{#configuring-cookie-usage}

AEM では、Web ページでの Cookie の使用方法を設定および制御できるサービスを提供しています:

* 設定可能なサーバー側のサービスによって、使用可能な Cookie のリストが維持されます。
* JavaScript API を使用すると、JavaScript コードで Cookie が使用できることを検証できます。

この機能を使用して、ページが Cookie の使用方法に関するユーザーの同意に従って動作するようにします。

## 許可される Cookie の設定 {#configuring-allowed-cookies}

Adobe Granite のオプトアウトサービスを設定して、web ページでの Cookie の使用方法を指定します。次の表は、設定可能なプロパティを示しています。

サービスを設定するには、[web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)を使用するか、[リポジトリに OSGi 設定を追加する](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)ことができます。次の表は、どちらの方法でも必要なプロパティを示しています。OSGi 設定の場合、サービス PID は `com.adobe.granite.optout` です。

| プロパティ名（web コンソール） | OSGi のプロパティ名 | 説明 |
|---|---|---|
| オプトアウトの Cookie | optout.cookies | ユーザーのデバイス上に存在する場合、ユーザーが Cookie の使用に同意していないことを示す Cookie の名前。 |
| オプトアウトの HTTP ヘッダー | optout.headers | 存在する場合、ユーザーが Cookie の使用に同意していないことを示す HTTP ヘッダーの名前。 |
| 許可リストの Cookie | optout.whitelist.cookies | Web サイトの動作に不可欠で、ユーザーの同意なしに使用できる Cookie のリスト。 |

## Cookie の使用状況の検証 {#validating-cookie-usage}

Cookie を使用できることを確認するには、クライアント側の JavaScript を使用して、Adobe Granite のオプトアウトサービスを呼び出します。次のタスクを実行するには、Granite.OptOutUtil という JavaScript オブジェクトを使用します。

* 追跡目的での Cookie の使用にユーザーが同意していないことを示す Cookie 名のリストを取得する
* 使用可能な Cookie のリストを取得する
* 追跡目的での Cookie の使用にユーザーが同意していないことを示す Cookie が、web ブラウザーに含まれているかどうかを確認する
* 特定の Cookie が使用可能であるかどうかを確認する

granite.utils [クライアントライブラリフォルダー](/help/sites-developing/clientlibs.md#referencing-client-side-libraries)には、Granite.OptOutUtil オブジェクトが用意されています。JavaScript ライブラリへのリンクを含めるには、ページ先頭の JSP に次のコードを追加します。

`<ui:includeClientLib categories="granite.utils" />`

例えば、次の JavaScript 関数は、COOKIE_NAME という Cookie に書き込む前に、その Cookie の使用を許可するかどうかを判定します。

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

存在する場合、ユーザーが Cookie の使用に同意していないことを示す Cookie の名前。

**パラメーター**

なし。

**戻り値**

Cookie 名の配列。

#### getWhitelistCookieNames() 関数 {#getwhitelistcookienames-function}

ユーザーの同意に関係なく使用できる Cookie の名前。

**パラメーター**

なし。

**戻り値**

Cookie 名の配列。

#### isOptedOut() 関数 {#isoptedout-function}

Cookie の使用の同意が得られていないことを示す Cookie がユーザーのブラウザーに保存されていないかを判断します。

**パラメーター**

なし。

**戻り値**

同意がないことを示す Cookie が見つかった場合はブール値 `true`、同意がないことを示す Cookie が存在しない場合は値 `false`。

### maySetCookie(cookieName) 関数 {#maysetcookie-cookiename-function}

ユーザーのブラウザーで特定の Cookie を使用できるかを判断します。この関数は、`isOptedOut` 関数を使用して、`getWhitelistCookieNames` 関数が返すリストに指定された Cookie が含まれているかどうかを判定する処理と同じです。

**パラメーター**

* cookieName：文字列。Cookie の名前。

**戻り値**

`cookieName` を使用できる場合はブール値 `true`、`cookieName` が使用できない場合は値 `false`。
