---
title: AEM Forms JEE パッチインストーラー
description: AEM Forms JEE パッチインストーラー
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: 495b9a006f5288ad6579e13aaea82ace6d6f0e91
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 69%

---

# AEM Forms JEE パッチインストーラー {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>詳細情報またはパッチの入手については、[サポートにお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)ください。

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
1. の **フォルダのインストールを選択** 画面を表示し、表示された既定の場所が既存のインストールに対して正しいことを確認するか、 **[!UICONTROL 参照]** AEM forms がインストールされている別のフォルダーを選択し、 **[!UICONTROL 次へ]**.
1. Quick Fix パッチの概要の情報を読み、「**[!UICONTROL 次へ]**」をクリックします。
1. プリインストールの概要情報を読み、「**[!UICONTROL インストール]**」をクリックします。
1. インストールが完了したら、「**[!UICONTROL 次へ]**」をクリックして、インストールされたファイルに対して Quick Fix アップデートを適用します。

1. **[Windows のみ]:** 次のいずれかの手順を実行します。
   * 次のいずれかを選択解除します。 **Configuration Manager を起動します。** オプションを使用して、 **[!UICONTROL 完了]**. 実行 **Configuration Manager** を使用して、 **ConfigurationManager.bat** 次の場所にあるファイル： `[aem-forms root]\configurationManager\bin`.

   * または、 **Configuration Manager を起動します。** オプションを使用して、 **[!UICONTROL 完了]**. 実行前 **Configuration Manager** using **ConfigurationManager.exe** または **ConfigurationManager_IPv6.exe**&#x200B;に移動します。 *`<AEMForms_Install_Dir>\configurationManager\bin`* ディレクトリと置換 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) および [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) ファイル。
   >[!NOTE]
   >使用 **ConfigurationManager.bat** ファイルを使用すると、 .lax ファイルの名前を手動で更新するのを防ぐことができます。

1. **[UNIX ベースの場合のみ]:**

   * この **Configuration Manager を起動します。** デフォルトでは、「 」チェックボックスがオンになっています。 クリック **[!UICONTROL 完了]** Configuration Manager を即座に実行するか、 **Configuration Manager** 後で、選択を解除します。 **Configuration Manager を起動します。** オプションを使用して、 **[!UICONTROL 完了]**. 以下を開始できます。 **Configuration Manager** 後で `[AEM_forms_root]/configurationManager/bin` ディレクトリ。

1. アプリケーションサーバーに応じて、以下のいずれかのドキュメントを選択し、*AEM Forms の設定とデプロイ*&#x200B;節の指示に従ってください。

   * [AEM Forms のインストールおよびデプロイ（JBoss 版）](http://www.adobe.com/go/learn_aemforms_installJBoss_65_jp)
   * [AEM Forms のインストールおよびデプロイ（WebSphere 版）](http://www.adobe.com/go/learn_aemforms_installWebSphere_65_jp)

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
