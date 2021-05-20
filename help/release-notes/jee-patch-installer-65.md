---
title: AEM Forms JEEパッチインストーラー
description: AEM Forms JEEパッチインストーラー
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 50%

---

# AEM Forms JEEパッチインストーラー{#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[詳細情報](https://www.adobe.com/account/sign-in.supportportal.html) やパッチの入手方法については、サポートにお問い合わせください。

## パッチインストーラーについて{#about-the-patch-installer}

AEM 6.5 Forms JEEパッチインストーラーには、このパッチのリリースまでに利用可能なAEM 6.5 Forms JEEのすべてのコンポーネントに関する修正済みの問題がすべて含まれています。 修正された問題の完全なリストについては、最新の「[サービスパックリリースノート](sp-release-notes.md)」を参照してください。

## パッチ{#prerequisites-to-installing-the-patch}のインストールの前提条件

* AEM 6.5 Forms

## パッチ{#installing-and-configuring-the-patch}のインストールと設定

1. &lt;*AEM_forms_root*>/deploy フォルダーのバックアップを作成します。Quick Fix をアンインストールする場合は必須です。
1. アプリケーションサーバーを停止します。
1. パッチインストーラーアーカイブファイルをハードディスクに展開します。
1. 使用しているオペレーティングシステムに従って名前が付けられたディレクトリで、次の操作を実行します。

   * **Windows**
インストーラーをコピーしたハードディスク上の適切なディレクトリまたはハードディスク上のフォルダーに移動し、 aemforms65_cfp_install.exeファイルをダブルクリックします。

      * (Windows 32 ビット) `Windows\Disk1\InstData\VM`
      * (Windows 64 ビット) `Windows_64Bit`\ `Disk1\InstData\VM`
   * ****
Linux適切なディレクトリに移動し、コマンドプロンプトで次のように入力します。 
`./aem65_cfp_install.bin`

      * (Linux) `Linux/Disk1/InstData/NoVM`

   インストールの手順を示すインストールウィザードが起動します。

1. 概要パネルで「**[!UICONTROL 次へ]**」をクリックします。
1. インストールフォルダーを選択画面で、表示されるデフォルトの場所が既存のインストール場所であることを確認するか、または「**[!UICONTROL 参照]**」をクリックして AEM Forms がインストールされている別のフォルダーを選択してから、「**[!UICONTROL 次へ]**」をクリックします。
1. Quick Fix パッチの概要の情報を読み、「**[!UICONTROL 次へ]**」をクリックします。
1. プリインストールの概要情報を読み、「**[!UICONTROL インストール]**」をクリックします。
1. インストールが完了したら、「**[!UICONTROL 次へ]**」をクリックして、インストールされたファイルに対して Quick Fix アップデートを適用します。

1. 「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。**ConfigurationManager.exe**&#x200B;または&#x200B;**ConfigurationManager_IPv6.exe**&#x200B;を使用してConfiguration Managerを実行する前に、*&lt;AEMorms_Install_Dir>\configurationManager\bin*&#x200B;ディレクトリに移動し、**axis.jar**&#x200B;を&#x200B;**に更新します —1.4.1.1.jar**（次のファイル）

   * ConfigurationManager.lax
   * ConfigurationManager_IPv6.lax

1. 「 Configuration Managerを起動」チェックボックスはデフォルトで選択されています。 「**[!UICONTROL 完了]**」をクリックして Configuration Manager を実行します。

1. Configuration Manager を後で実行するには、「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。`[AEM_forms_root]/configurationManager/bin`ディレクトリ内の適切なスクリプトを使用して、後でConfiguration Managerを起動できます。

1. アプリケーションサーバーに応じて、以下のいずれかのドキュメントを選択し、「*AEM Forms の設定とデプロイ*」節の指示に従ってください。

   * [AEM Forms のインストールおよびデプロイ（JBoss 版）](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [AEM Forms のインストールおよびデプロイ（WebSphere 版）](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. （JBossのみ）パッチをインストールしてサーバーを設定した後、JBossアプリケーションサーバーのtmpディレクトリとworkディレクトリを削除します。

## デプロイ後の設定{#post-deployment-configurations}

### SAML設定{#saml-configurations}

SAML認証を設定済みで、大きなIDPメタデータに関する問題が発生する場合は、パッチをインストールした後に次の手順を実行します。

1. アプリケーションサーバーで次のシステムプロパティを設定します。\
   `um.saml.enable.large.xml=true`
1. サーバーを再起動します。
1. 既存のSAML認証プロバイダーを削除し、SAML設定の説明に従って、既存のドメインに対して再度追加します。

## 影響を受けたモジュール{#impacted-modules}

* ドキュメントサービス
* Document Security
* Foundation JEE

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
