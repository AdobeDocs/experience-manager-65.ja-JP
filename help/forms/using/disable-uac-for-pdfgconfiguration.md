---
title: JEE と OSGI の両方に適用可能な PDFG 設定の UAC の無効化
description: PDFG 設定の UAC を無効にする手順
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 63%

---

# Word または Excel ファイルを Windows Server 上のPDFに変換できません {#unable-to-convert-word-excel-files-PDF}

## 問題 {#issue}

ユーザーが Word または Excel ファイルをMicrosoft Windows Server 上のPDFに変換しようとすると、次のエラーが発生します。

*プライマリコンバータからのエラーメッセージ：ALC-PDG-015-003-Theシステムは入力ファイルを開けません。 ファイルを再度送信するか、システム管理者に問い合わせてください。*


## 解決策 {#solution}

問題を解決するには、以下の手順を実行します。
1. システム構成ユーティリティにアクセスするには、**[!UICONTROL スタート／ファイル名を指定して実行]**&#x200B;を選択し、**[!UICONTROL MSCONFIG]** と入力します。
1. 「**[!UICONTROL ツール]**」タブをクリックし、スクロールして「**[!UICONTROL UAC 設定を変更]**」を選択します。「**[!UICONTROL 起動]**」をクリックして新しいウィンドウでコマンドを実行します。
1. スライダーを「通知しない」レベルに設定します。完了したら、コマンドウィンドウを閉じ、システム構成ウィンドウを閉じます。
1. レジストリ設定で UAC が 0（ゼロ）に設定されていることを検証します。検証するには、以下の手順を実行します。

   1. Microsoft® は、レジストリを変更する前にバックアップをとっておくことを推奨しています。詳しい手順については、「[Windows でのレジストリのバックアップと復元方法](https://support.microsoft.com/ja-jp/help/322756)」を参照してください。
   1. Microsoft® Windows のレジストリエディターを開きます。レジストリエディターを開くには、「スタート／ファイル名を指定して実行」に移動し、「regedit」と入力して「OK」をクリックします。
   1. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\` に移動します。EnableLUA の値が 0（ゼロ）に設定されていることを確認します。
   1. **EnableLUA** の値が 0（ゼロ）に設定されていることを確認します。値が 0 に設定されていない場合は、0 に変更します。レジストリエディターを終了します。

1. コンピューターを再起動します。

## 適用先 {#appliesto}

このソリューションは、次の場合に適用されます。
* JEE 上のAEM Forms Server
* AEM Forms on OSGi Server
