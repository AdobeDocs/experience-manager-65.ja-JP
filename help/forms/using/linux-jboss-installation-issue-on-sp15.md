---
title: JBoss® Linux®環境でのAEM Forms JEE 6.5.15.0 サービスパックのインストールの問題
description: AEM Forms JEE 6.5.15.0 サービスパックがJBoss® Linux®環境に適切にインストールされていない場合、アプリケーションサーバーにパッチ変更が適用されません。 XML ディレクトリに「RUP_BOM.xml」ファイルを追加します。
SEO Description: AEM Forms JEE 6.5.15.0 service pack  is not installed properly on the JBoss Linux environment.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 45%
---
# JBoss®環境でのAEM Forms 6.5.15.0 JEE サービスパックのインストールに関する問題 {#aem-forms-installation-issue-environment}

## 問題 {#issue}

AEM Forms JEE 6.5.15.0 サービスパックがJBoss® Linux®環境に正しくインストールされていません。 `PatchInstallerProcessing[1-9*].log` ファイルにログエントリ `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing` が記録されます。 このエントリは、AEM Forms JEE 6.5.15.0 サービスパックのインストールが成功しなかったことを示しています。

## 適用先 {#applies-to}

このソリューションは次の場合に適用されます。
* JBoss® Linux® 環境

>[!NOTE]
>
> [RUP_BOM.xml ファイルをXML ディレクトリ &#x200B;](#solution-solution)に追加する手順を実行する前に、AEM Forms JEE 6.5.15.0 サービスパックが少なくとも1回アプリケーションサーバーにインストールされていることを確認してください。

## 解決策 {#solution}

AEM Forms JEE 6.5.15.0 サービスパックのインストールに関する問題を修正するには、`RUP_BOM.xml` ファイルをXML ディレクトリに追加します。
1. パッチ `AEMForms-6.5.0-0057_jboss_linux.tar.gz` を抽出したフォルダーに移動します。
1. `/CDROM_Installers/Linux/Disk1/InstData` の場所に移動し、`Resource1.zip` ファイルを見つけます。
1. 抽出されたフォルダー以外の場所に `Resource1.zip` ファイルをコピーし、`Resource1.zip` ファイルを解凍します。
1. `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` に移動して、`RUP_BOM.xml` ファイルをコピーします。
1. RUP_BOM.xml ファイルを `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml` に貼り付けます。
1. [AEM Forms JEE 6.5.15.0 サービスパック &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)を再インストールします。
