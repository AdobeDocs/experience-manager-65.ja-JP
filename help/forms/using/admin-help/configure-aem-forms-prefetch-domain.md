---
title: ドメイン情報をプリフェッチするための AEM Forms の設定
seo-title: ドメイン情報をプリフェッチするための AEM Forms の設定
description: グループのネストが深いことによって応答時間が遅くなる場合や、多くのグループのメンバーである場合、ドメイン情報をプリフェッチするように AEM Forms を設定します。
seo-description: グループのネストが深いことによって応答時間が遅くなる場合や、多くのグループのメンバーである場合、ドメイン情報をプリフェッチするように AEM Forms を設定します。
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 72%

---

# ドメイン情報をプリフェッチするための AEM Forms の設定 {#configure-aem-forms-to-prefetchdomain-information}

ユーザーが多数のグループに属している場合（例えば、500 以上）や、グループのネストが深い場合（例えば、30 レベル）、応答時間が遅くなる可能性があります。この問題が発生している場合は、特定のドメインから情報をプリフェッチするように AEM Forms を設定できます。

1. 管理コンソールで、**[!UICONTROL 設定/User Management/設定/設定/設定ファイルの読み込みと書き出し]**&#x200B;をクリックします。
1. 現在の設定をファイルにエクスポートするには、**[!UICONTROL エクスポート]**&#x200B;をクリックし、設定ファイルを別の場所に保存します。
1. 次のノード（太字でマーク）を追加します。

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   この例では、複数のドメインがプリフェッチ用に設定されています。ドメイン名は「/」によって区切られます。このことは、上の例において *Domain_Name1*、*Domain_Name2*&#x200B;および&#x200B;*Domain_Name3* として示されています。

1. 更新したファイルを読み込むには、User Managementで、**[!UICONTROL 設定/設定ファイルの読み込みと書き出し]**&#x200B;をクリックします。
1. 「**[!UICONTROL 参照]**」をクリックしてファイルを探し、「読み込み」をクリックして、「**[!UICONTROL OK]**」をクリックします。
