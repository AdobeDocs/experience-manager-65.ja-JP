---
title: 認証評価の順序を変更する
description: AEM Forms が複数の認証プロバイダーを評価する順序を変更できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '159'
ht-degree: 100%

---

# 認証評価の順序を変更する {#change-the-order-of-evaluation-for-authentication}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

複数の認証プロバイダーを設定した場合、AEM Forms による認証評価の順序を変更できます。config.xml ファイルにリストされている認証プロバイダーの順序によって、認証評価の順序が決まります。

1. 管理コンソールで、設定／User Management／設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. ファイルに現在の設定をエクスポートするには、「エクスポート」をクリックして別の場所に設定ファイルを保存します。
1. ファイル内で次のノードを見つけます。

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

1. 更新したファイルをインポートするには、User Management で、「設定ファイルのインポートとエクスポート」をクリックします。
1. 「参照」をクリックしてファイルを探し、「インポート」をクリックして「OK」をクリックします。
