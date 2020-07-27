---
title: 認証評価の順序の変更
seo-title: 認証評価の順序の変更
description: AEM Forms が複数の認証プロバイダーを評価する順序を変更できます。
seo-description: AEM Forms が複数の認証プロバイダーを評価する順序を変更できます。
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 91%

---


# 認証評価の順序の変更 {#change-the-order-of-evaluation-for-authentication}

複数の認証プロバイダーを設定した場合、AEM Forms による認証評価の順序を変更できます。認証評価の順序は、config.xml ファイルに一覧表示される認証プロバイダーの順序によって決まります。

1. 管理コンソールで、設定／User Management／設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 現在の設定をファイルに書き出すには、「書き出し」をクリックして設定ファイルを別の場所に保存します。
1. ファイルから、以下のノードを検索します。

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   In `<entry key="order" value="3" />`, edit the value for each node to set the order of the authentication evaluation.

1. 更新したファイルを読み込むには、User Management で、設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 「参照」をクリックしてファイルを探し、「読み込み」をクリックして「OK」をクリックします。

