---
title: AEM Forms JEE パッチインストーラー
description: AEM Forms JEE パッチインストーラー
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: ht
source-wordcount: '522'
ht-degree: 100%

---

# AEM Forms JEE パッチインストーラー {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>詳細情報またはパッチの入手については、[サポートにお問い合わせ](https://www.adobe.com/jp/account/sign-in.supportportal.html)ください。

## パッチインストーラーについて {#about-the-patch-installer}

AEM 6.5 Forms JEE パッチインストーラーには、このパッチのリリースまで使用可能であった、AEM 6.5 Forms JEE のすべてのコンポーネントに関するすべての問題の修正が含まれています。修正された問題の一覧については、最新の[サービスパックリリースノート](release-notes.md)を参照してください。

## パッチをインストールするための前提条件 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## パッチのインストールと設定 {#installing-and-configuring-the-patch}

1. &lt;*AEM_forms_root*>/deploy フォルダーのバックアップを作成します。Quick Fix をアンインストールする場合は必須です。
1. アプリケーションサーバーを停止します。
1. パッチインストーラーアーカイブファイルをハードディスクに展開します。
1. 使用しているオペレーティングシステムに従って名前が付けられたディレクトリで、次の操作を実行します。

   * **Windows**

インストールメディアの適切なディレクトリまたはハードディスク上にあるインストーラーのコピー先フォルダーに移動して、aemforms65_cfp_install.exe ファイルをダブルクリックします。

      * （Windows 32 ビット） `Windows\Disk1\InstData\VM`
      * （Windows 64 ビット） `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**
適切なディレクトリに移動して、コマンドプロンプトで、 
`./aem65_cfp_install.bin` を入力します。

      * （Linux）`Linux/Disk1/InstData/NoVM`

   インストールの手順を示すインストールウィザードが起動します。

1. 概要パネルで「**[!UICONTROL 次へ]**」をクリックします。
1. **インストールフォルダーを選択**&#x200B;画面で、表示されるデフォルトの場所が既存のインストール場所であることを確認するか、または「**[!UICONTROL 参照]**」をクリックして AEM Forms がインストールされている別のフォルダーを選択してから、「**[!UICONTROL 次へ]**」をクリックします。
1. Quick Fix パッチの概要の情報を読み、「**[!UICONTROL 次へ]**」をクリックします。
1. プリインストールの概要情報を読み、「**[!UICONTROL インストール]**」をクリックします。
1. インストールが完了したら、「**[!UICONTROL 次へ]**」をクリックして、インストールされたファイルに対して Quick Fix アップデートを適用します。

1. **[Windows のみ]：** 次のいずれかのステップを実行します。
   * 「**Configuration Manager を起動**」オプションの選択を解除し、「**[!UICONTROL 完了]**」をクリックします。`[aem-forms root]\configurationManager\bin` にある **ConfigurationManager.bat** ファイルを使用して **Configuration Manager** を実行します。

   * または、「**Configuration Manager を起動**」オプションの選択を解除し、「**[!UICONTROL 完了]**」をクリックします。*`<AEMForms_Install_Dir>\configurationManager\bin`* ディレクトリに移動し、[ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) ファイルおよび [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) ファイルを置き換えてから、**ConfigurationManager.exe** または **ConfigurationManager_IPv6.exe** を使用して **Configuration Manager** を実行します。
   >[!NOTE]
   >**ConfigurationManager.bat** ファイルを使用すると、.lax ファイルの名前を手動でアップデートする必要がなくなります。

1. **[UNIX ベースの場合のみ]：**

   * 「**Configuration Manager を起動**」チェックボックスは、デフォルトで選択されています。「**[!UICONTROL 完了]**」をクリックして Configuration Manager をすぐに実行するか、**Configuration Manager** を後で実行するには、「**Configuration Manager を起動**」オプションの選択を解除してから、「**[!UICONTROL 完了]**」をクリックします。`[AEM_forms_root]/configurationManager/bin` ディレクトリ内の適切なスクリプトを使用して、後で **Configuration Manager** を起動することができます。

1. アプリケーションサーバーに応じて、以下のいずれかのドキュメントを選択し、*AEM Forms の設定とデプロイ*&#x200B;節の指示に従ってください。

   * [AEM Forms のインストールおよびデプロイ（JBoss 版）](https://www.adobe.com/go/learn_aemforms_installJBoss_65_jp)
   * [AEM Forms のインストールおよびデプロイ（WebSphere 版）](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_jp)

1. （JBoss のみ）パッチをインストールしてサーバーを設定した後、JBoss Application Server の tmp および work ディレクトリを削除します。

## デプロイメント後の設定 {#post-deployment-configurations}

### SAML の設定 {#saml-configurations}

SAML 認証を設定済みで、大きな IDP メタデータに関する問題が発生した場合は、パッチをインストールした後に次の手順を実行します。

1. アプリケーションサーバーで次のシステムプロパティを設定します。\
   `um.saml.enable.large.xml=true`
1. サーバーを再起動します。
1. 既存の SAML 認証プロバイダーを削除し、SAML 設定の説明に従って、既存のドメインに対してそれらのプロバイダーを再度追加します。

## 影響を受けるモジュール {#impacted-modules}

* Document Services
* Document Security
* Foundation JEE

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
