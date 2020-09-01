---
title: AEM FormsJEEパッチインストーラー
description: 'null'
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
translation-type: tm+mt
source-git-commit: c1af919d4c0fd984249e1a7009274c63b8ce9adb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 45%

---


# AEM FormsJEEパッチインストーラー {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[詳細やパッチの入手方法については、サポート](https://www.adobe.com/jp/account/sign-in.supportportal.html) にお問い合わせください。

## パッチインストーラについて {#about-the-patch-installer}

AEM 6.5FormsJEEパッチインストーラーには、このパッチのリリースまで使用可能なAEM 6.5FormsJEEのすべてのコンポーネントに関するすべての修正済みの問題が含まれています。 修正された問題の完全なリストについては、最新の [Service Packリリースノート](sp-release-notes.md) を参照してください。

## パッチのインストールに必要な前提条件 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## パッチのインストールと設定 {#installing-and-configuring-the-patch}

1. &lt;*AEM_forms_root*>/deploy フォルダーのバックアップを作成します。Quick Fix をアンインストールする場合は必須です。
1. アプリケーションサーバーを停止します。
1. パッチインストーラーのアーカイブファイルをハードドライブに展開します。
1. 使用しているオペレーティングシステムに従って名前が付けられたディレクトリで、次の操作を実行します。

   * **Windows**&#x200B;インストールメディアまたはハードディスク上のインストーラーのコピー先フォルダーにある適切なディレクトリに移動し、aemforms65_cfp_install.exeファイルを重複クリックします。

      * (Windows 32-bit) `Windows\Disk1\InstData\VM`
      * (Windows 64-bit) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**&#x200B;適切なディレクトリに移動し、コマンドプロンプトで次のように入力します。 
`./aem65_cfp_install.bin`。

      * (Linux) `Linux/Disk1/InstData/NoVM`

   インストールの手順を示すインストールウィザードが起動します。

1. 概要パネルで「**[!UICONTROL 次へ]**」をクリックします。
1. インストールフォルダーを選択画面で、表示されるデフォルトの場所が既存のインストール場所であることを確認するか、または「**[!UICONTROL 参照]**」をクリックして AEM Forms がインストールされている別のフォルダーを選択してから、「**[!UICONTROL 次へ]**」をクリックします。
1. Quick Fix パッチの概要の情報を読み、「**[!UICONTROL 次へ]**」をクリックします。
1. プリインストールの概要情報を読み、「**[!UICONTROL インストール]**」をクリックします。
1. インストールが完了したら、「**[!UICONTROL 次へ]**」をクリックして、インストールされたファイルに対して Quick Fix アップデートを適用します。

1. 「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。ConfigurationManager.exe **またはConfigurationManager_IPv6.exeを使用してConfiguration Manager** を実行する前に **、**&lt;AEMForms_Install_Dir \configurationManager\bin ********** directoryに移動し、&lt;AEMForms_Install_Dir>dirディレクトリに移動し、.1.jarを更新してください。

   * ConfigurationManager.lax
   * ConfigurationManager_IPv6.lax

1. 「開始設定マネージャー」(Configuration Manager)チェックボックスはデフォルトで選択されています。 「**[!UICONTROL 完了]**」をクリックして Configuration Manager を実行します。

1. Configuration Manager を後で実行するには、「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。You can start Configuration Manager later using the appropriate script in the `[AEM_forms_root]/configurationManager/bin` directory.

1. アプリケーションサーバーに応じて、以下のいずれかのドキュメントを選択し、「*AEM Forms の設定とデプロイ*」節の指示に従ってください。

   * [AEM Forms のインストールおよびデプロイ（JBoss 版）](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [AEM Forms のインストールおよびデプロイ（WebSphere 版）](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. （JBossのみ）パッチをインストールしてサーバーを設定した後、JBoss Application Serverのtmpおよびworkディレクトリを削除します。

## Post-deployment configurations {#post-deployment-configurations}

### SAML設定 {#saml-configurations}

SAML認証を設定済みで、大きいIDPメタデータに関する問題が発生する場合は、パッチのインストール後に次の手順を実行します。

1. アプリケーションサーバーで次のシステムプロパティを設定します。\
   `um.saml.enable.large.xml=true`
1. サーバーを再起動します。
1. SAML設定の説明に従って、既存のSAML認証プロバイダーを削除し、既存のドメインに対して再度追加します。

## 影響を受けたモジュール {#impacted-modules}

* ドキュメントサービス
* ドキュメントのセキュリティ
* Foundation JEE

[サポートへのお問い合わせ](https://www.adobe.com/jp/account/sign-in.supportportal.html)
