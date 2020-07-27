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
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 72%

---


# ドメイン情報をプリフェッチするための AEM Forms の設定 {#configure-aem-forms-to-prefetchdomain-information}

ユーザーが多数のグループに属している場合（例えば、500 以上）や、グループのネストが深い場合（例えば、30 レベル）、応答時間が遅くなる可能性があります。この問題が発生している場合は、特定のドメインから情報をプリフェッチするように AEM Forms を設定できます。

1. In administration console, click **[!UICONTROL Settings > User Management > Configuration > Import And Export Configuration Files]**.
1. To export the current configuration setting to a file, click **[!UICONTROL Export]** and save the configuration file in another location.
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

1. To import the updated file, in User Management, click **[!UICONTROL Configuration > Import And Export Configuration Files]**.
1. Click **[!UICONTROL Browse]** to find the file, click Import, and then click **[!UICONTROL OK]**.

