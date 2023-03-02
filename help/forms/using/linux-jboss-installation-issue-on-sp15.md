---
title: JBoss® Linux®環境でのAEM Forms JEE 6.5.15.0 Service Pack のインストールに関する問題
description: AEM Forms JEE 6.5.15.0 Service Pack が JBoss® Linux®環境に正しくインストールされていない場合、パッチの変更はアプリケーションサーバーに適用されません。 XML ディレクトリに'RUP_BOM.xml'ファイルを追加します。
source-git-commit: 76a3a87408ceb13023737379c20fb44ce5fb180a
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 7%

---


# JBoss®環境でのAEM Forms 6.5.15.0 JEE Service Pack のインストールの問題 {#aem-forms-installation-issue-environment}

## 問題 {#issue}

AEM Forms JEE 6.5.15.0 Service Pack が JBoss® Linux®環境に正しくインストールされていない。 In `PatchInstallerProcessing[1-9*].log` ログエントリをファイルする。 `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component isn't in the installation. Skipping Processing`、がログに記録されます。 このエントリは、AEM Forms JEE 6.5.15.0 Service Pack のインストールが成功しなかったことを示します。

## 適用先 {#applies-to}

このソリューションは次の場合に適用されます。
* JBoss® Linux®環境

>[!NOTE]
>
> 以下の手順を実行する前に、AEM Forms JEE 6.5.15.0 Service Pack がアプリケーションサーバーに少なくとも 1 回インストールされていることを確認してください。 [RUP_BOM.xml ファイルを XML ディレクトリに追加する](#solution-solution).

## ソリューション {#solution}

インストールの問題を修正するには、AEM Forms JEE 6.5.15.0 Service Pack で `RUP_BOM.xml` ファイルを XML ディレクトリに配置します。
1. パッチを抽出したフォルダーに移動します。 `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. に移動します。 `/CDROM_Installers/Linux/Disk1/InstData` 場所と `Resource1.zip` ファイル。
1. を `Resource1.zip` ファイルを展開し、解凍したフォルダーの外の別の場所に保存します。 `Resource1.zip` ファイル。
1. に移動します。 `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` をクリックし、 `RUP_BOM.xml` ファイル。
1. RUP_BOM.xml ファイルを次の場所に貼り付けます。 `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. を再インストールします。 [AEM Forms JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja).