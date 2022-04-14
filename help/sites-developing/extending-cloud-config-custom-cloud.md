---
title: カスタムクラウドサービスの作成
seo-title: Creating a Custom Cloud Service
description: デフォルトのクラウドサービスを、カスタムクラウドサービスタイプで拡張することができます
seo-description: The default set of Cloud Services can be extended with custom Cloud Service types
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '418'
ht-degree: 100%

---

# カスタムクラウドサービスの作成{#creating-a-custom-cloud-service}

デフォルトのクラウドサービスを、カスタムクラウドサービスタイプで拡張することができます。これにより、カスタムマークアップを構造的な方法でページに挿入できます。この手法は、Google Analytics や Chartbeat など、主としてサードパーティの分析プロバイダーに使用されます。Cloud Services は、親ページから子ページに継承されますが、任意のレベルで継承を中断できます。

>[!NOTE]
>
>ここで紹介する手順は、Google Analytics を使用して新しいクラウドサービスを作成する場合の例です。この内容がそのまま実際のユースケースに当てはまるとは限りません。

1. CRXDE Lite で、`/apps` の下に新しいノードを作成します。

   * **名前**：`acs`
   * **型**：`nt:folder`

1. `/apps/acs` の下に新しいノードを作成します。

   * **名前**：`analytics`
   * **型**：`sling:Folder`

1. `/apps/acs/analytics` の下に新しいノードを 2 つ作成します。

   * **名前**：components
   * **型**：`sling:Folder`

   および

   * **名前**：templates
   * **タイプ**：`sling:Folder`


1. 「`/apps/acs/analytics/components`」を右クリックします。 「**作成...**」を選択し、「**コンポーネントを作成...**」をクリックします。表示されるダイアログで、以下の項目を指定します。

   * **ラベル**：`googleanalyticspage`
   * **タイトル**：`Google Analytics Page`
   * **スーパータイプ**：`cq/cloudserviceconfigs/components/configpage`
   * **グループ**：`.hidden`

1. 「**次へ**」を 2 回クリックして、次の項目を指定します。

   * **許可された親：** `acs/analytics/templates/googleanalytics`

   「**次へ**」を 2 回クリックして、「**OK**」をクリックします。

1. プロパティを「`googleanalyticspage`」に追加します。

   * **名前：** `cq:defaultView`
   * **値：** `html`

1. 以下の内容で、`content.jsp` という新しいファイルを `/apps/acs/analytics/components/googleanalyticspage` の下に作成します。

   ```xml
   <%@page contentType="text/html"
               pageEncoding="utf-8"%><%
   %><%@include file="/libs/foundation/global.jsp"%><div>
   
   <div>
       <h3>Google Analytics Settings</h3>
       <ul>
           <li><div class="li-bullet"><strong>accountID: </strong><br><%= xssAPI.encodeForHTML(properties.get("accountID", "")) %></div></li>
       </ul>
   </div>
   ```

1. `/apps/acs/analytics/components/googleanalyticspage/` の下に新しいノードを作成します。

   * **名前**：`dialog`
   * **型**：`cq:Dialog`
   * **プロパティ**：

      * **名前**：`title`
      * **型**：`String`
      * **値**：`Google Analytics Config`
      * **名前**：`xtype`
      * **型**：`String`
      * **値**：`dialog`

1. 「`/apps/acs/analytics/components/googleanalyticspage/dialog`」の下に新しいノードを作成します。

   * **名前**：`items`
   * **型**：`cq:Widget`
   * **プロパティ**：

      * **名前**：`xtype`
      * **型**：`String`
      * **値**：`tabpanel`

1. 「`/apps/acs/analytics/components/googleanalyticspage/dialog/items`」の下に新しいノードを作成します。

   * **名前**：`items`
   * **型**：`cq:WidgetCollection`

1. 「`/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`」の下に新しいノードを作成します。

   * **名前**：tab1
   * **型**：`cq:Panel`
   * **プロパティ**：

      * **名前**：`title`
      * **型**：`String`
      * **値**：`Config`

1. 「`/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`」の下に新しいノードを作成します。

   * **名前**：items
   * **型**：`nt:unstructured`
   * **プロパティ**：

      * **名前**：`fieldLabel`
      * **種類**：string
      * **値**：アカウント ID

      * **名前**：`fieldDescription`
      * **型**：`String`
      * **値**：`The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **名前**：`name`
      * **型**：`String`
      * **値**：`./accountID`
      * **名前**：`validateOnBlur`
      * **型**：`String`
      * **値**：`true`
      * **名前**：`xtype`
      * **型**：`String`
      * **値**：`textfield`

1. `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` を `/apps/acs/analytics/components/googleanalyticspage/body.jsp` にコピーして、34 行目の `libs` を `apps` に変更し、79 行目のスクリプト参照を完全修飾パスにします。
1. 「`/apps/acs/analytics/templates/`」の下に新しいテンプレートを次のように作成します。

   * **Resource Type** = `acs/analytics/components/googleanalyticspage`
   * **Label** = `googleanalytics`
   * **Title**= `Google Analytics Configuration`
   * **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage`（jcr:content ノードではなくテンプレートノード）
   * **cq:designPath** = `/etc/designs/cloudservices/googleanalytics`（jcr:content）

1. 新しいコンポーネントを作成します： `/apps/acs/analytics/components/googleanalytics`。

   次の内容を `googleanalytics.jsp` に追加します。

   ```xml
   <%@page import="org.apache.sling.api.resource.Resource,
                   org.apache.sling.api.resource.ValueMap,
                   org.apache.sling.api.resource.ResourceUtil,
                   com.day.cq.wcm.webservicesupport.Configuration,
                   com.day.cq.wcm.webservicesupport.ConfigurationManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   
   String[] services = pageProperties.getInherited("cq:cloudserviceconfigs", new String[]{});
   ConfigurationManager cfgMgr = resource.getResourceResolver().adaptTo(ConfigurationManager.class);
   if(cfgMgr != null) {
       String accountID = null;
       Configuration cfg = cfgMgr.getConfiguration("googleanalytics", services);
       if(cfg != null) {
           accountID = cfg.get("accountID", null);
       }
   
       if(accountID != null) {
       %>
   <script type="text/javascript">
   
     var _gaq = _gaq || [];
     _gaq.push(['_setAccount', '<%= accountID %>']);
     _gaq.push(['_trackPageview']);
   
     (function() {
       var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
       ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
       var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
     })();
   
   </script><%
       }
   }
   %>
   ```

   これによって、設定プロパティに基づいたカスタムマークアップが出力されます。

1. `http://localhost:4502/miscadmin#/etc/cloudservices` に移動して、新しいページを作成します。

   * **タイトル**：`Google Analytics`
   * **名前**：`googleanalytics`

   CRXDE Lite に戻り、`/etc/cloudservices/googleanalytics` の下で、次のプロパティを `jcr:content` に追加します。

   * **名前**：`componentReference`
   * **型**：`String`
   * **値**：`acs/analytics/components/googleanalytics`


1. 新規作成したサービスページ（`http://localhost:4502/etc/cloudservices/googleanalytics.html`）に移動し、「**+**」をクリックして新しい設定を作成します。

   * **親設定**：`/etc/cloudservices/googleanalytics`
   * **タイトル：**  `My First GA Config`

   「**Google Analytics 設定**」を選択し、「**作成**」をクリックします。

1. **アカウント ID**（例：`AA-11111111-1`）を入力します。「**OK**」をクリックします。
1. ページに移動し、「**クラウドサービス**」タブで、新たに作成された設定をページプロパティに追加します。
1. このページにカスタムマークアップが追加されます。
