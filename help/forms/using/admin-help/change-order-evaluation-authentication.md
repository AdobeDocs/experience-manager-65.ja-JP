---
title: 認証評価の順序の変更
seo-title: Change the order of evaluation for authentication
description: AEM Forms が複数の認証プロバイダーを評価する順序を変更できます。
seo-description: You can change the order in which AEM forms evaluates multiple authentication providers.
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '147'
ht-degree: 100%

---

# 認証評価の順序の変更 {#change-the-order-of-evaluation-for-authentication}

複数の認証プロバイダーを設定した場合、AEM forms による認証評価の順序を変更できます。認証評価の順序は、config.xml ファイルに一覧表示される認証プロバイダーの順序によって決まります。

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

   `<entry key="order" value="3" />` で、各ノードの値を編集して認証評価の順序を設定します。

1. 更新したファイルを読み込むには、User Management で、設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 「参照」をクリックしてファイルを探し、「読み込み」をクリックして「OK」をクリックします。
