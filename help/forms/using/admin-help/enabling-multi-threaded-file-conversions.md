---
title: マルチスレッドファイル変換の有効化
description: マルチスレッドファイル変換を有効にする方法を説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 100%

---

# マルチスレッドファイル変換の有効化 {#enabling-multi-threaded-file-conversions}

PDF Generator では、特定の種類のファイルに対して、マルチスレッドファイル変換を有効にすることができます。マルチスレッドファイル変換では、同時に複数の変換を実行できるので、PDF Generator のパフォーマンスが向上します。

## OpenOffice、Word および PowerPoint ドキュメントでのマルチスレッドファイル変換の有効化 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

PDF Generator は、デフォルトでは一度に 1 つの OpenOffice、Microsoft® Word または PowerPoint ドキュメントのみを変換できます。マルチスレッド変換を有効にすると、PDF Generator は複数のドキュメントを同時に変換できます。PDF Generator から OpenOffice または PDFMaker の複数のインスタンスが起動します（これらのインスタンスは Word 変換および PowerPoint 変換に使用されます）。

>[!NOTE]
>
>マルチスレッドファイル変換は、Microsoft® Word 2003 および PowerPoint 2003 ではサポートされていません。マルチスレッドファイル変換を有効にするには、Microsoft Word 2007 および PowerPoint 2007 か、Microsoft Word 2010 および PowerPoint 2010 にアップグレードします。

>[!NOTE]
>
>マルチスレッドファイル変換は、Microsoft® Excel、Microsoft® Visio、Microsoft® Project、Microsoft® Publisher ではサポートされていません。

OpenOffice または PDFMaker の各インスタンスは、個別のユーザーアカウントを使用して起動されます。追加する各ユーザーアカウントは、Forms サーバーコンピューター上での管理者権限を持つ有効なユーザーである必要があります。クラスター環境では、同じユーザーセットが、クラスターのすべてのノードで有効である必要があります。

管理コンソールのユーザーアカウントページで、マルチスレッドファイル変換に使用するユーザーアカウントを指定できます。アカウントの追加や削除をしたり、アカウントのパスワードを変更したりすることができます。Windows Server 2003 または Windows Server 2008 で PDF Generator を実行している場合は、管理者権限を持つユーザーアカウントを 3 つ以上追加します。

Windows Server 2003 または 2008 での OpenOffice、Microsoft® Word または Microsoft® PowerPoint のユーザー、あるいは Linux® または Sun™ Solaris™ での OpenOffice のユーザーを追加する場合、すべてのユーザーに対して最初に表示されるアクティベート用のダイアログを閉じます。

### プロセスレベルトークンの置き換え権限を追加 {#add-the-right-to-replace-the-process-level-token}

Windows オペレーティングシステムでは、PDF 変換に使用される管理者ユーザーアカウント（PDFG ユーザー）に、プロセスレベルトークンの置き換え権限が必要です。この権限は、グループポリシーエディターを使用して追加できます。

1. Windows のスタートメニューで「ファイル名を指定して実行」をクリックし、「gpedit.msc」と入力します。
1. ローカルコンピューターポリシー／コンピューターの構成／Windows の設定／セキュリティの設定／ローカルポリシー／ユーザー権利の割り当てをクリックします。*プロセスレベルトークンの置き換え*&#x200B;ポリシーを編集し、管理者グループが含まれるようにします。
1. 「プロセスレベルトークンの置き換え」エントリにユーザーを追加します。

### Windows Server 2008 での OpenOffice、Microsoft® Word および Microsoft® PowerPoint に必要な追加設定 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Windows Server 2008 で OpenOffice、Microsoft® Word または Microsoft® PowerPoint を実行している場合は、追加した各ユーザーの UAC を無効にします。

1. コントロールパネル／ユーザーアカウント／ユーザーアカウント制御の有効化または無効化をクリックします。
1. 「ユーザーアカウント制御（UAC）を使ってコンピューターの保護に役立たせる」の選択を解除し、「OK」をクリックします。
1. コンピューターを再起動して設定を有効にします。

### Linux® または Solaris™ での OpenOffice に必要な追加設定 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. ユーザーアカウントを追加します（[ユーザーアカウントを追加](enabling-multi-threaded-file-conversions.md#add-a-user-account)を参照）。
1. 次に、/etc/sudoers ファイルを変更する必要があります。このファイルのデフォルトの権限は 440 です。このファイルの権限を書き込み可能に変更します。
1. /etc/sudoers ファイルに、追加のユーザー（Forms サーバーを実行する管理者以外）のエントリを追加します。例えば、lcadm というユーザー名と myhost というサーバー名で AEM Forms を実行していて、user1 および user2 という別のユーザーとして実行する場合は、/etc/sudoers に次のエントリを追加します。

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   この設定により、lcadm は、ホスト「myhost」において「user1」または「user2」として、パスワードの入力を求められることなくすべてのコマンドを実行できます。

   >[!NOTE]
   >
   >必ずシステムユーザーと PDFG ユーザーの役割を「user1」と「user2」に割り当ててください。PDFG の役割をユーザーに割り当てるには、[ユーザーアカウントを追加](enabling-multi-threaded-file-conversions.md#add-a-user-account)を参照してください。

1. また、/etc/sudoers ファイルで次の行を見つけて、行の先頭にシャープ記号（#）を追加してコメントアウトします。

   ```shell
   Defaults requiretty
   ```

   これで、Linux® ユーザーを追加できるようになります。

1. /etc/sudoers ファイルの権限を 440 に戻します。
1. [ユーザーアカウントを追加](enabling-multi-threaded-file-conversions.md#add-a-user-account)で追加したすべてのユーザーが Forms サーバーに接続できるようにします。例えば、user1 というローカルユーザーに、Forms サーバーに接続する権限を許可するには、次のコマンドを使用します。

   `xhost +local:user1@`

   詳しくは、xhost コマンドのドキュメントを参照してください。

1. サーバーを再起動します。

>[!NOTE]
>
>OpenOffice は、すべての PDFG ユーザーがアクセスできるディレクトリの場所にインストールする必要があります。これを検証するには、PDFG ユーザーとしてログインし、問題なく OpenOffice を起動できるかどうかを確認します。

### ユーザーアカウントを追加 {#add-a-user-account}

1. 管理コンソールで、サービス／PDF Generator／ユーザーアカウントをクリックします。
1. 「追加」をクリックし、Forms サーバーでの管理者権限を持つユーザーのユーザー名とパスワードを入力します。OpenOffice のユーザーを設定する場合は、最初の OpenOffice アクティベーションダイアログを閉じます。

   >[!NOTE]
   >
   >OpenOffice 用にユーザーを設定する場合、OpenOffice のインスタンス数を、この手順で指定したユーザーアカウント数よりも多くすることはできません。

1. Forms サーバーを再起動します。

### マルチスレッドファイル変換に使用されるリストからユーザーを削除 {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 管理コンソールで、サービス／PDF Generator／ユーザーアカウントをクリックします。
1. 削除するユーザーの横のチェックボックスをクリックし、「削除」をクリックします。
1. 確認ページで、「削除」をクリックします。
1. Forms サーバーを再起動します。

### アカウントのパスワードを変更 {#change-the-password-for-an-account}

1. 管理コンソールで、サービス／PDF Generator／ユーザーアカウントをクリックします。
1. ユーザー名をクリックし、新しいパスワードを入力して確定します。このパスワードは、ユーザーのシステムパスワードと一致させる必要があります。
