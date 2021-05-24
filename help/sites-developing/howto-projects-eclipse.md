---
title: Eclipse を使用して AEM プロジェクトを開発する方法
seo-title: Eclipse を使用して AEM プロジェクトを開発する方法
description: このガイドでは、Eclipse を使用して AEM ベースのプロジェクトを開発する方法について説明します
seo-description: このガイドでは、Eclipse を使用して AEM ベースのプロジェクトを開発する方法について説明します
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 67%

---

# Eclipse を使用して AEM プロジェクトを開発する方法{#how-to-develop-aem-projects-using-eclipse}

このガイドでは、Eclipse を使用して AEM ベースのプロジェクトを開発する方法について説明します。

>[!NOTE]
>
>アドビでは、Eclipse による AEM ソリューションの開発を支援する [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) を提供しています。

## 概要 {#overview}

Eclipse で AEM の開発を開始するには、次の手順を実行する必要があります。

各手順の詳細については、このページで後述します。

* Eclipse 4.3（Kepler）のインストール
* Maven に基づく AEM プロジェクトの設定
* Maven POM での Eclipse 用の JSP サポートの準備
* Eclipse への Maven プロジェクトの読み込み

>[!NOTE]
>
>このガイドは Eclipse 4.3（Kepler）と AEM 5.6.1 を基に作成されています。

## Eclipse のインストール {#install-eclipse}

[Eclipse のダウンロードページ](https://www.eclipse.org/downloads/)から「Eclipse IDE for Java EE Developers」をダウンロードします。

[インストール手順](https://wiki.eclipse.org/Eclipse/Installation)に従って Eclipse をインストールします。

## Maven に基づく AEM プロジェクトの設定  {#set-up-your-aem-project-based-on-maven}

次に、[Apache Mavenを使用してAEMプロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)の説明に従って、Mavenを使用してプロジェクトをセットアップします。

## Eclipse 用の JSP サポートの準備 {#prepare-jsp-support-for-eclipse}

Eclipse では JSP との連携もサポートされます。サポートされる項目の例を次に示します。

* タグライブラリのオートコンプリート
* &lt;cq:defineObjects /> と &lt;sling:defineObjects /> で定義されたオブジェクトの Eclipse での認識

サポートを有効にするには、次の手順を実行します。

1. [Apache Maven](/help/sites-developing/ht-projects-maven.md)を使用してAEMプロジェクトをビルドする方法の[JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)を使用する方法の手順に従ってください。
1. コンテンツモジュールの POM 内の &lt;build /> セクションに次の項目を追加します。

   Eclipse の Maven サポートプラグインである m2e は maven-jspc-plugin のサポートを提供しません。この設定は、プラグインおよび一時的なコンパイルの結果のクリーンアップの関連タスクを無視するように m2e に通知します。

   これは問題ではありません。[JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)を使用する方法で述べたように、この設定では、maven-jspc-pluginは、ビルドプロセスの一環としてJSPコンパイルを検証する目的でのみ使用されます。EclipseはJSPで既に問題を報告しており、それを行うためにこのMavenプラグインを使用しません。

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### Eclipse への Maven プロジェクトの読み込み {#import-the-maven-project-into-eclipse}

1. Eclipse で、File／Import を選択します。
1. Import ダイアログで、Maven／Existing Maven Projects を選択し、「Next」をクリックします。

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. プロジェクトの最上位のフォルダーのパスを入力して、「Select All」、「Finish」の順にクリックします。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. これで、Eclipse を使用して AEM プロジェクトを開発するための設定（JSP のオートコンプリートを含む）がすべて完了しました。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >`/libs/foundation/global.jsp`または他のJSPを`/libs`に含める場合は、Eclipseがインクルージョンを解決できるように、そのJSPをプロジェクトにコピーする必要があります。 同時に、Mavenによってコンテンツパッケージにバンドルされていないことを確認する必要があります。 これを実現する方法については、[Apache Mavenを使用してAEMプロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)を参照してください。
