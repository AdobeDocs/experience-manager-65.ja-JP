---
title: AEM Forms JEE パッチインストーラー
description: AEM Forms JEE パッチインストーラー
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 51%

---

# AEM Forms JEE パッチインストーラー {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[サポートに連絡](https://www.adobe.com/account/sign-in.supportportal.html) を参照してください。

## パッチインストーラーについて {#about-the-patch-installer}

AEM 6.5 Forms JEE パッチインストーラーには、このパッチのリリースまで、AEM 6.5 Forms JEE のすべてのコンポーネントに関する修正済みの問題がすべて含まれています。 最新の  [Service Pack リリースノート](release-notes.md) 修正された問題の完全なリストを参照してください。

## パッチをインストールするための前提条件 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## パッチのインストールと設定 {#installing-and-configuring-the-patch}

1. &lt;*AEM_forms_root*>/deploy フォルダーのバックアップを作成します。Quick Fix をアンインストールする場合は必須です。
1. アプリケーションサーバーを停止します。
1. パッチインストーラーアーカイブファイルをハードディスクに展開します。
1. 使用しているオペレーティングシステムに従って名前が付けられたディレクトリで、次の操作を実行します。

   * **Windows**
インストーラーをコピーしたハードディスク上のインストールメディアまたはフォルダーの適切なディレクトリに移動し、 aemforms65_cfp_install.exe ファイルをダブルクリックします。

      * (Windows 32 ビット) `Windows\Disk1\InstData\VM`
      * (Windows 64 ビット) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**
適切なディレクトリに移動し、コマンドプロンプトで次のように入力します。 
`./aem65_cfp_install.bin`

      * (Linux) `Linux/Disk1/InstData/NoVM`

   インストールの手順を示すインストールウィザードが起動します。

1. 概要パネルで「**[!UICONTROL 次へ]**」をクリックします。
1. インストールフォルダーを選択画面で、表示されるデフォルトの場所が既存のインストール場所であることを確認するか、または「**[!UICONTROL 参照]**」をクリックして AEM Forms がインストールされている別のフォルダーを選択してから、「**[!UICONTROL 次へ]**」をクリックします。
1. Quick Fix パッチの概要の情報を読み、「**[!UICONTROL 次へ]**」をクリックします。
1. プリインストールの概要情報を読み、「**[!UICONTROL インストール]**」をクリックします。
1. インストールが完了したら、「**[!UICONTROL 次へ]**」をクリックして、インストールされたファイルに対して Quick Fix アップデートを適用します。

1. 「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。を使用して Configuration Manager を実行する前に **ConfigurationManager.exe** または **ConfigurationManager_IPv6.exe**&#x200B;に移動します。 *&lt;aemforms_install_dir>\configurationManager\bin* ディレクトリと更新 `ConfigurationManager.lax` および `ConfigurationManager_IPv6.lax` 次の名前変更操作を含むファイル：

   * `axis.jar`コピー先：`axis-1.4.1.1.jar`
   * `serializer-2.7.1.jar`コピー先：`serializer-2.7.2.jar`
   * `xalan-2.7.1.jar`コピー先：`xalan-2.7.2.jar`
   * `xercesImpl-2.9.1.jar`コピー先：`xercesImpl-2.12.0.jar`
   * `xml-apis-2.7.1.jar`コピー先：`xml-apis-2.7.2.jar`

1. 「 Configuration Manager を起動」チェックボックスはデフォルトで選択されています。 「**[!UICONTROL 完了]**」をクリックして Configuration Manager を実行します。

1. Configuration Manager を後で実行するには、「完了」をクリックする前に、「Configuration Manager を起動」オプションの選択を解除します。Configuration Manager は、後で `[AEM_forms_root]/configurationManager/bin` ディレクトリ。

1. アプリケーションサーバーに応じて、以下のいずれかのドキュメントを選択し、「*AEM Forms の設定とデプロイ*」節の指示に従ってください。

   * [AEM Forms のインストールおよびデプロイ（JBoss 版）](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [AEM Forms のインストールおよびデプロイ（WebSphere 版）](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. （JBoss のみ）パッチをインストールしてサーバーを設定した後、JBoss Application Server の tmp および work ディレクトリを削除します。

## デプロイ後の設定 {#post-deployment-configurations}

### SAML 設定 {#saml-configurations}

SAML 認証を設定済みで、大きな IDP メタデータに関する問題が発生する場合は、パッチをインストールした後に以下の手順を実行します。

1. アプリケーションサーバーで次のシステムプロパティを設定します。\
   `um.saml.enable.large.xml=true`
1. サーバーを再起動します。
1. 既存の SAML 認証プロバイダーを削除し、SAML 設定の説明に従って、既存のドメインに対して再度追加します。

## 影響を受けるモジュール {#impacted-modules}

* ドキュメントサービス
* Document Security
* Foundation JEE

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
