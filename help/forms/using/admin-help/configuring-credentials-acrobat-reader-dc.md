---
title: 証明書を Acrobat Reader DC Extensions で使用するための設定
seo-title: 証明書を Acrobat Reader DC Extensions で使用するための設定
description: 証明書を Acrobat Reader DC Extensions で使用するための設定方法について説明します。
seo-description: 証明書を Acrobat Reader DC Extensions で使用するための設定方法について説明します。
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 97%

---


# 証明書を Acrobat Reader DC Extensions で使用するための設定{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

PDF ドキュメントに使用権限を適用するには、Acrobat Reader DC Extensions 用の有効な証明書を使用して AEM Forms を設定します。証明書は、AEM Forms をインストールするときに設定されている場合があります。Configuration Manager の実行中に Acrobat Reader DC Extensions の証明書を設定しなかった場合や、新しい証明書を読み込む、または証明書を置き換える必要がある場合は、Trust Store の管理ページを使用して行うことができます。

評価用の証明書を使用している場合は、実稼働環境に移行するときに実稼働環境用の証明書に置き換えます。期限切れの証明書または評価用の証明書を更新するには、最初に、古くなった Acrobat Reader DC Extensions 証明書を削除します。

証明書の取得について詳しくは、「[AEM Forms のインストールの準備（シングルサーバー）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)」を参照してください。

Trust Store には複数の Acrobat Reader DC Extensions 証明書が含まれることがあります。これらの証明書の 1 つを、デフォルトの Reader Extensions 証明書として指定する必要があります。デフォルトの証明書は、Workbench ユーザーがプロセス作成時に、どの証明書を使用するかを判断できない場合に使用されます。デフォルトの証明書には以下の規則が適用されます。

* Acrobat Reader DC Extensions 証明書を読み込んだときに、Trust Store に Acrobat Reader DC Extensions 証明書が 1 つしか含まれていない場合は、その証明書がデフォルトとして設定されます。
* 「デフォルト」オプションを選択して Acrobat Reader DC Extensions 証明書を読み込むと、既存のデフォルトの証明書のデフォルト設定が解除され、読み込まれた証明書がデフォルトになります。
* デフォルトの Acrobat Reader DC Extensions 証明書は削除できません。デフォルトの証明書を削除するには、最初に、他の証明書をデフォルトとして設定します。ただし、証明書が 1 つしかない場合は例外で、デフォルトの証明書でも削除できます。
* デフォルトの Acrobat Reader DC Extensions 証明書は更新できません。

>[!NOTE]
>
>プログラムによって証明書を読み込んだり、削除したりすることもできます（「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63)」を参照してください。）

## Acrobat Reader DC Extensions 証明書の読み込み {#import-a-acrobat-reader-dc-extensions-credential}

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 「読み込み」をクリックし、「Trust Store の種類」で「Acrobat Reader DC Extensions 証明書」を選択します。
1. （オプション）この証明書を Acrobat Reader DC Extensions のデフォルトの証明書として指定するには、「デフォルト」を選択します。
1. 「エイリアス」ボックスに、証明書の ID を入力します。この ID は、Acrobat Reader DC Extensions で証明書の表示名として使用されます。このエイリアスは、AEM Forms SDK を使用してプログラムから証明書にアクセスするときにも使用されます。

   >[!NOTE]
   >
   >エイリアス名は、見やすいように大文字に自動的に変換されます。エイリアス名をプロセスで参照するときは、大文字と小文字は区別されません。

1. 「ファイルを選択」をクリックして証明書を探し、証明書のパスワードを入力して「OK」をクリックします。

   「形式が正しくないか、パスワードが正しくないため、証明書を読み込めませんでした」というエラーメッセージが表示される場合は、パスワードが有効であることを確認してください。

## Acrobat Reader DC Extensions 証明書の削除 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 証明書を選択し、「削除」をクリックします。

## Acrobat Reader DC Extensions 証明書の置換 {#replace-a-acrobat-reader-dc-extensions-credential}

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 既存の証明書のエイリアスをメモしておきます。このエイリアスを選択して「削除」をクリックします。
1. 完全に同一のエイリアス名を使用して、新しい証明書を読み込みます。

