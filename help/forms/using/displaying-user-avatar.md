---
title: ユーザーアバターの表示
seo-title: ユーザーアバターの表示
description: AEM Forms Workspace をカスタマイズしてログインしたユーザーの画像を表示する方法。
seo-description: AEM Forms Workspace をカスタマイズしてログインしたユーザーの画像を表示する方法。
uuid: 2961dc93-f0d0-4842-80f1-3c239a20e348
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: aec03ea5-17a6-4775-92cb-2ad361895fdf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# ユーザーアバターの表示 {#displaying-the-user-avatar}

ログインユーザーのアバターは、AEM Forms Workspace の右上隅に表示されます。また、組織階層の直接レポートのアバターはマネージャービューに表示されます。AEM Forms Workspaceを設定して、LDAPサーバーなどのデータベースからユーザー画像を選択できます。

>[!NOTE]
>
>サポートされているユーザー画像の縦横比は 1:1 です。

1. 次の手順に記載されている説明を使用して DSC を作成します。For more information, see &#39;Developing Components for AEM Forms&#39; topic in [Programming with AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63) guide.
1. DSC で getCurrentUserImageUrl と getUserImageUrl メソッドを公開する新しい SPI を定義して、AEM Forms ユーザーの画像 URL を取得します。Java™ コードスニペットのサンプルを以下に示します。

   ```as3
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. component.xml ファイルを作成します。spec-id が以下に表示されているコードスニペットと同じであることを確認します。

   以下にサンプルのコードスニペットを示します。特定の要件に合うようにカスタマイズします。

   ```as3
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. Workbench を介して DSC をデプロイします。サービスを `ProcessManagementClientSessionService` 再起動します。
1. ブラウザを更新するか、またはユーザーとログアウトして再度ログインする必要がある場合があります。

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
