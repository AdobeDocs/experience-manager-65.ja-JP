---
title: ドメイン情報をプリフェッチするためのAEM forms の設定
description: 深くネストされたグループが原因で応答時間が遅くなった場合や、多くのグループのメンバーである場合は、AEM forms を設定してドメイン情報をプリフェッチします。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 39%

---

# ドメイン情報をプリフェッチするためのAEM forms の設定 {#configure-aem-forms-to-prefetchdomain-information}

多数のグループに属している場合（例：500 以上）や、グループが深くネストされている場合（例：30 レベル）は、応答時間が長くなる場合があります。 この問題が発生した場合は、特定のドメインから情報をプリフェッチするようにAEM forms を設定できます。

1. 管理コンソールで、**[!UICONTROL 設定／User Management／設定／既存の設定ファイルのインポートとエクスポート]**&#x200B;をクリックします。
1. ファイルに現在の設定をエクスポートするには、「**[!UICONTROL エクスポート]**」をクリックして別の場所に設定ファイルを保存します。
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

   この例では、プリフェッチ用に複数のドメインが設定されています。 ドメイン名は「/」で区切られます。 このことは、上の例において *Domain_Name1*、*Domain_Name2* および *Domain_Name3* として示されています。

1. 更新したファイルをインポートするには、User Management で、「**[!UICONTROL 設定ファイルのインポートとエクスポート]**」をクリックします。
1. 「**[!UICONTROL 参照]**」をクリックしてファイルを探し、「インポート」をクリックして「**[!UICONTROL OK]**」をクリックします。
