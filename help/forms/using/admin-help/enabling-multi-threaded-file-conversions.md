---
title: マルチスレッドファイル変換の有効化
seo-title: マルチスレッドファイル変換の有効化
description: マルチスレッドファイル変換を有効化する方法について説明します。
seo-description: マルチスレッドファイル変換を有効化する方法について説明します。
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 100%

---


# マルチスレッドファイル変換の有効化 {#enabling-multi-threaded-file-conversions}

PDF Generator では、特定のファイルの種類に対して、マルチスレッドファイル変換を有効にできます。マルチスレッドファイル変換では、同時に複数の変換を実行できるので、PDF Generator のパフォーマンスが向上します。

## OpenOffice、Word および PowerPoint ドキュメントでのマルチスレッドファイル変換の有効化 {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

PDF Generator では、一度に 1 つの OpenOffice、Microsoft Word または PowerPoint ドキュメントのみをデフォルトで変換できます。マルチスレッド変換を有効にすると、PDF Generator は複数のドキュメントを同時に変換できます。PDF Generator から OpenOffice または PDFMaker の複数のインスタンスが起動します（これらのインスタンスは Word 変換および PowerPoint 変換に使用されます）。

>[!NOTE]
>
>マルチスレッドファイル変換は、Microsoft Word 2003 および PowerPoint 2003 ではサポートされていません。マルチスレッドファイル変換を有効にするには、Microsoft Word 2007 および PowerPoint 2007、または Microsoft Word 2010 および PowerPoint 2010 にアップグレードします。

>[!NOTE]
>
>マルチスレッドファイル変換は、Microsoft Excel、Microsoft Visio、Microsoft Project または Microsoft Publisher ではサポートされていません。

OpenOffice または PDFMaker の各インスタンスは、それぞれ別のユーザーアカウントを使用して起動されます。追加する各ユーザーアカウントは、forms サーバーコンピューター上での管理者権限を持つ有効なユーザーである必要があります。クラスター環境では、同じユーザーセットがクラスターのすべてのノードで有効である必要があります。

管理コンソールのユーザーアカウントページで、マルチスレッドファイル変換で使用するユーザーアカウントを指定できます。アカウントの追加と削除またはアカウントのパスワードの変更を行うことができます。Windows Server 2003 または Windows Server 2008 で PDF Generator を実行している場合は、管理者権限を持つユーザーアカウントを少なくとも 3 つ追加します。

Windows Server 2003 または 2008 での OpenOffice、Microsoft Word または Microsoft PowerPoint のユーザー、あるいは Linux または Sun™ Solaris™ での OpenOffice のユーザーを追加する場合、すべてのユーザーに対して最初に表示されるアクティベート用のダイアログを閉じます。

### プロセスレベルトークンを置き換えるための権限の追加 {#add-the-right-to-replace-the-process-level-token}

Windows オペレーティングシステムでは、PDF 変換で使用される管理者ユーザーアカウント（PDFG ユーザー）に、プロセスレベルトークンの置き換え権限が必要です。この権限は、グループポリシーエディターを使用して追加できます。

1. Windows のスタートメニューで「ファイル名を指定して実行」をクリックし、「gpedit.msc」と入力します。
1. ローカルコンピューターポリシー／コンピューターの構成／Windows の設定／セキュリティの設定／ローカルポリシー／ユーザー権利の割り当てをクリックします。次に、Administrators グループが含まれるように「*プロセスレベルトークンの置き換え*」ポリシーを編集します。
1. 「プロセスレベルトークンの置き換え」エントリにユーザーを追加します。

### Windows Server 2008 での OpenOffice、Microsoft Word および Microsoft PowerPoint に必要な追加設定 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Windows Server 2008 で OpenOffice、Microsoft Word または Microsoft PowerPoint を実行する場合は、追加する各ユーザーの UAC を無効にします。

1. コントロールパネル／ユーザーアカウント／ユーザーアカウント制御の有効化または無効化をクリックします。
1. 「ユーザーアカウント制御（UAC）を使ってコンピューターの保護に役立たせる」の選択を解除し、「OK」をクリックします。
1. コンピューターを再起動して設定を有効にします。

### Linux または Solaris での OpenOffice に必要な追加設定 {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. ユーザーアカウントを追加します（[ユーザーアカウントの追加](enabling-multi-threaded-file-conversions.md#add-a-user-account)を参照）。
1. 次に、/etc/sudoers ファイルに変更を加えます。このファイルの権限はデフォルトで 440 が設定されています。このファイルの権限を書き込み可能に変更します。
1. /etc/sudoers ファイルで、追加のユーザー（forms サーバーを実行する管理者以外）のエントリを追加します。例えば、ユーザーを lcadm、サーバーを myhost として AEM Forms を実行している場合、user1 および user2 として動作させるには、/etc/sudoers に次のエントリを追加します。

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   この設定により、lcadm は、ホスト myhost において user1 または user2 として、パスワードの入力を求められることなくすべてのコマンドを実行できるようになります。

   >[!NOTE]
   >
   >システムユーザーロールと PDFG ユーザーロールを user1 と user2 に割り当てたことを確認してください。PDFG ロールをユーザーに割り当てるには、[ユーザーアカウントの追加](enabling-multi-threaded-file-conversions.md#add-a-user-account)を参照してください。

1. また、/etc/sudoers ファイルで、この行を見つけて、行の先頭に番号記号（#）を追加してコメントアウトします。

   ```shell
   Defaults requiretty
   ```

   これで、Linux ユーザーを追加できます。

1. /etc/sudoers ファイルの権限を 440 に再度変更します。
1. [ユーザーアカウントの追加](enabling-multi-threaded-file-conversions.md#add-a-user-account)で追加したすべてのユーザーが forms サーバーに接続できるようにします。例えば、user1 というローカルユーザーに forms サーバーに接続する権限を許可するには、次のコマンドを使用します。

   `xhost +local:user1@`

   詳しくは、xhost コマンドのドキュメントを参照してください。

1. サーバーを再起動します。

>[!NOTE]
>
>OpenOffice は、すべての PDFG ユーザーがアクセスできるディレクトリにインストールする必要があります。アクセスを検証するには、PDFG ユーザーとしてログインし、OpenOffice を問題なく実行できるかどうかを確認します。

### ユーザーアカウントの追加 {#add-a-user-account}

1. 管理コンソールで、サービス／PDF Generator／ユーザーアカウントをクリックします。
1. 「追加」をクリックし、forms サーバー上での管理者権限を持つユーザーのユーザー名とパスワードを入力します。OpenOffice のユーザーを設定する場合は、最初に表示される OpenOffice のアクティベート用のダイアログを閉じます。

   >[!NOTE]
   >
   >OpenOffice のユーザーを設定する場合、OpenOffice のインスタンス数を、この手順で指定したユーザーアカウント数よりも大きくすることはできません。

1. forms サーバーを再起動します。

### マルチスレッドファイル変換用リストからのユーザーの削除 {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. 管理コンソールで、サービス／PDF Generator／ユーザーアカウントをクリックします。
1. 削除するユーザーの横のチェックボックスをクリックし、「削除」をクリックします。
1. 確認ページで、「削除」をクリックします。
1. forms サーバーを再起動します。

### アカウントのパスワードの変更 {#change-the-password-for-an-account}

1. 管理コンソールで、サービス／PDF Generator／ユーザーアカウントをクリックします。
1. ユーザー名をクリックし、新しいパスワードを入力して確認します。このパスワードは、ユーザーのシステムパスワードと同じものである必要があります。

