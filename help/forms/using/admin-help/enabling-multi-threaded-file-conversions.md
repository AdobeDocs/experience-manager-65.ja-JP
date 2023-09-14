---
title: マルチスレッドファイル変換の有効化
description: マルチスレッドファイル変換を有効にする方法を説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
source-git-commit: fd8bb7d3d9040e0a7a6b2f65751445f41aeab73e
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 3%

---

# マルチスレッドファイル変換の有効化 {#enabling-multi-threaded-file-conversions}

PDF Generatorを使用すると、特定の種類のファイルに対して、マルチスレッドファイル変換を有効にすることができます。 マルチスレッドファイル変換では、同時に複数のPDF Generatorを実行できるので、変換のパフォーマンスが向上します。

## OpenOffice、Word、PowerPoint ドキュメントのマルチスレッドファイル変換の有効化 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

PDF Generatorでは、デフォルトで一度に 1 つの OpenOffice、Microsoft® Word または PowerPoint ドキュメントのみ変換できます。 マルチスレッド変換を有効にすると、PDF Generatorは複数のドキュメントを同時に変換できます。 PDF Generatorは、OpenOffice または PDFMaker の複数のインスタンスを起動します（Word および PowerPoint の変換を実行するために使用されます）。

>[!NOTE]
>
>Microsoft® Word 2003 および PowerPoint 2003 では、マルチスレッドファイル変換はサポートされていません。 マルチスレッドファイル変換を有効にするには、Microsoft® Word 2007 と PowerPoint 2007、またはMicrosoft® Word 2010 と PowerPoint 2010 にアップグレードします。

>[!NOTE]
>
マルチスレッドファイル変換は、Microsoft® Excel、Microsoft® Visio、Microsoft® Project、Microsoft® Publisher ではサポートされていません。

OpenOffice または PDFMaker の各インスタンスは、別々のユーザーアカウントを使用して起動されます。 追加する各ユーザーアカウントは、Forms Server コンピューター上での管理者権限を持つ有効なユーザーである必要があります。 クラスター環境では、同じユーザーセットがクラスターのすべてのノードで有効である必要があります。

管理コンソールのユーザーアカウントページで、マルチスレッドファイル変換に使用するユーザーアカウントを指定できます。 アカウントの追加、削除、またはアカウントのパスワードの変更を行うことができます。 Windows Server 2003 または Windows Server 2008 でPDF Generatorを実行している場合は、管理者権限を持つユーザーアカウントを 3 つ以上追加します。

OpenOffice、Microsoft® Word、Microsoft® PowerPoint (Windows Server 2003、2008)、または OpenOffice (Linux®、Sun™ Solaris™) のユーザーを追加する場合は、すべてのユーザーの初期アクティベーションダイアログを閉じます。

### プロセスレベルのトークンを置き換える権限を追加 {#add-the-right-to-replace-the-process-level-token}

Windows オペレーティングシステムでは、PDF変換に使用される管理者ユーザーアカウント（PDFG ユーザー）は、プロセスレベルのトークン権限を置き換える必要があります。 この権限は、グループポリシーエディタを使用して追加できます。

1. Windows の [ スタート ] メニューで、[ ファイル名を指定して実行 ] をクリックし、「 gpedit.msc 」と入力します。
1. [ ローカルコンピュータポリシー ] > [ コンピュータの構成 ] > [Windows の設定 ] > [ セキュリティの設定 ] > [ ローカルポリシー ] > [ ユーザー権限の割り当て ] の順にクリックします。 を編集します。 *プロセスレベルトークンの置換* 管理者グループを含めるポリシーです。
1. 「プロセスレベルトークンの置き換え」エントリにユーザーを追加します。

### Windows Server 2008 上の OpenOffice、Microsoft® Word およびMicrosoft® PowerPoint に必要な追加設定 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Windows Server 2008 で OpenOffice、Microsoft® Word またはMicrosoft® PowerPoint を実行している場合は、追加した各ユーザーの UAC を無効にします。

1. 「Campaign コントロールパネル」>「ユーザーアカウント」>「ユーザーアカウント制御を有効にする」をクリックします。
1. 「ユーザーアカウント制御（UAC）を使ってコンピューターの保護に役立たせる」の選択を解除し、「OK」をクリックします。
1. 設定を有効にするには、コンピューターを再起動します。

### Linux®または Solaris™上の OpenOffice に必要な追加設定 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. ユーザーアカウントを追加します。 ( 詳しくは、 [ユーザーアカウントの追加](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. 次に、/etc/sudoers ファイルを変更する必要があります。 このファイルのデフォルトの権限は 440 です。 このファイルの権限を書き込み可能に変更します。
1. /etc/sudoers ファイルに、追加のユーザー (Forms Server を実行する管理者以外 ) のエントリを追加します。 例えば、lcadm というユーザーおよび myhost という名前のサーバーとしてAEM forms を実行していて、user1 および user2 として動作させる場合は、/etc/sudoers に次のエントリを追加します。

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   この設定により、lcadm は、パスワードの入力を求めることなく、ホスト「myhost」に対して「user1」または「user2」として任意のコマンドを実行できます。

   >[!NOTE]
   >
   システムユーザーと PDFG ユーザーの役割を「user1」と「user2」に割り当てていることを確認します。 PDFG ロールをユーザーに割り当てるには、 [ユーザーアカウントの追加](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. また、/etc/sudoers ファイルで、行の先頭に番号記号 (#) を付けて、この行を見つけてコメントアウトします。

   ```shell
   Defaults requiretty
   ```

   これにより、Linux®ユーザを追加できます。

1. etc/sudoers ファイルの権限を 440 に変更します。
1. 経由で追加したすべてのユーザーを許可 [ユーザーアカウントの追加](enabling-multi-threaded-file-conversions.md#add-a-user-account) をクリックして、Forms Server に接続します。 例えば、user1 という名前のローカルユーザーに対し、Forms Server への接続権限を許可するには、次のコマンドを使用します。

   `xhost +local:user1@`

   詳しくは、 xhost コマンドのドキュメントを参照してください。

1. サーバーを再起動します。

>[!NOTE]
>
OpenOffice は、すべての PDFG ユーザーがアクセスできるディレクトリの場所にインストールする必要があります。 これを確認するには、PDFG ユーザーとしてログインし、問題なく OpenOffice を起動できるかどうかを確認します。

### ユーザーアカウントの追加 {#add-a-user-account}

1. 管理コンソールで、サービス/PDF Generator/ユーザーアカウントをクリックします。
1. 「追加」をクリックし、Forms Server での管理者権限を持つユーザーのユーザー名とパスワードを入力します。 OpenOffice のユーザーを設定する場合は、最初の OpenOffice アクティベーションダイアログを閉じます。

   >[!NOTE]
   >
   OpenOffice 用にユーザーを設定する場合、OpenOffice のインスタンス数を、この手順で指定したユーザーアカウント数より多くすることはできません。

1. Formsサーバーを再起動します。

### マルチスレッドファイル変換に使用されるリストからユーザーを削除する {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 管理コンソールで、サービス/PDF Generator/ユーザーアカウントをクリックします。
1. 削除するユーザーの横のチェックボックスをクリックし、「削除」をクリックします。
1. 確認ページで、「削除」をクリックします。
1. Formsサーバーを再起動します。

### アカウントのパスワードの変更 {#change-the-password-for-an-account}

1. 管理コンソールで、サービス/PDF Generator/ユーザーアカウントをクリックします。
1. ユーザー名をクリックし、新しいパスワードを入力して確定します。 このパスワードは、ユーザーのシステムパスワードと一致する必要があります。
