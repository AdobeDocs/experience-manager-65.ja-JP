---
title: JBoss® Linux® 環境での AEM Forms JEE 6.5.15.0 サービスパックのインストールに関する問題
description: AEM Forms JEE 6.5.15.0 サービスパックが JBoss® Linux® 環境に正しくインストールされず、アプリケーションサーバーにパッチの変更が適用されません。XML ディレクトリに「RUP_BOM.xml」ファイルを追加します。
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '204'
ht-degree: 100%

---

# JBoss® 環境での AEM Forms 6.5.15.0 JEE サービスパックのインストールに関する問題 {#aem-forms-installation-issue-environment}

## 問題 {#issue}

AEM Forms JEE 6.5.15.0 サービスパックが JBoss® Linux® 環境に正しくインストールされません。`PatchInstallerProcessing[1-9*].log` ファイルにログエントリ `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing` が記録されます。このエントリは、AEM Forms JEE 6.5.15.0 サービスパックのインストールが成功しなかったことを示しています。

## 適用先 {#applies-to}

このソリューションは次の場合に適用されます。
* JBoss® Linux® 環境

>[!NOTE]
>
> [RUP_BOM.xml ファイルを XML ディレクトリに追加する](#solution-solution)手順を実行する前に、AEM Forms JEE 6.5.15.0 サービスパックがアプリケーションサーバーに少なくとも 1 回インストールされていることを確認してください。

## ソリューション {#solution}

AEM Forms JEE 6.5.15.0 サービスパックのインストール問題を修正するには、`RUP_BOM.xml` ファイルを XML ディレクトリに追加します。
1. パッチ `AEMForms-6.5.0-0057_jboss_linux.tar.gz` を抽出したフォルダーに移動します。
1. `/CDROM_Installers/Linux/Disk1/InstData` の場所に移動し、`Resource1.zip` ファイルを見つけます。
1. 抽出されたフォルダー以外の場所に `Resource1.zip` ファイルをコピーし、`Resource1.zip` ファイルを解凍します。
1. `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` に移動して、`RUP_BOM.xml` ファイルをコピーします。
1. RUP_BOM.xml ファイルを `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml` に貼り付けます。
1. [AEM Forms JEE 6.5.15.0 サービスパック](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)を再インストールします。
