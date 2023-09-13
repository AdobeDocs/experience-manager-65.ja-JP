---
title: 資格情報をAcrobat Reader DC Extensions で使用するための設定
description: 資格情報をAcrobat Reader DC Extensions で使用するための設定方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 5%

---

# 資格情報をAcrobat Reader DC Extensions で使用するための設定{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

使用権限をPDFドキュメントに適用するには、Acrobat Reader DC Extensions 用の有効な資格情報を使用してAEM forms を設定します。 秘密鍵証明書は、AEM forms のインストール中に設定されている可能性があります。 Configuration Manager の実行中にAcrobat Reader DC Extensions 証明書を設定していない場合、または新しい証明書や置き換え用の証明書を読み込む必要がある場合は、Trust Store の管理ページを使用して設定できます。

評価用資格情報を使用している場合は、実稼動環境に移行する際に、実稼動用資格情報に置き換えます。 期限切れの資格情報または評価用の資格情報を更新するには、まず古いAcrobat Reader DC Extensions 資格情報を削除します。

秘密鍵証明書の取得について詳しくは、 [AEM forms のインストールの準備（シングルサーバー）](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

Trust Store には、複数のAcrobat Reader DC Extensions 証明書を含めることができます。 これらの資格情報の 1 つを、デフォルトのReader拡張資格情報として指定します。 デフォルトの資格情報は、Workbench ユーザーがプロセスの作成中に使用する資格情報を特定できない場合に使用されます。 以下のルールはデフォルトの資格情報に適用されます。

* Acrobat Reader DC Extensions 証明書を読み込んでも、Trust Store に他のAcrobat Reader DC Extensions 資格情報が含まれていない場合、その資格情報がデフォルトとして設定されます。
* 「デフォルト」オプションを選択してAcrobat Reader DC Extensions 証明書を読み込むと、デフォルトの種類は既存のデフォルトの資格情報から削除されます。 読み込まれた証明書がデフォルトになります。
* デフォルトのAcrobat Reader DC Extensions 証明書は削除できません。 デフォルトの秘密鍵証明書を削除するには、まず別の秘密鍵証明書をデフォルトとして設定します。 ただし、このルールの例外は、1 つの秘密鍵証明書しかない場合、デフォルトの秘密鍵証明書でも削除できるという点です。
* デフォルトのAcrobat Reader DC Extensions 証明書は更新できません。

>[!NOTE]
>
>また、プログラムを使用して秘密鍵証明書を読み込んだり、削除したりすることもできます。 ( 詳しくは、 [AEM forms によるプログラミング](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja).)

## Acrobat Reader DC Extensions 証明書の読み込み {#import-a-acrobat-reader-dc-extensions-credential}

1. 管理コンソールで、設定/Trust Store の管理/ローカル秘密鍵証明書をクリックします。
1. 「読み込み」をクリックし、「Trust Store の種類」で「 Acrobat Reader DC Extensions 証明書」を選択します。
1. （オプション）この資格情報がAcrobat Reader DC Extensions で使用するデフォルトの資格情報であることを示すには、「デフォルト」を選択します。
1. 「エイリアス」ボックスに、秘密鍵証明書の識別子を入力します。 この識別子は、Acrobat Reader DC Extensions で秘密鍵証明書の表示名として使用されます。 このエイリアスは、AEM forms SDK を使用してプログラムで秘密鍵証明書にアクセスする場合にも使用されます。

   >[!NOTE]
   >
   >エイリアス名は、表示用に自動的に大文字に変換されます。 エイリアス名をプロセスで参照する際、大文字と小文字は区別されません。

1. 「ファイルを選択」をクリックして証明書を探し、証明書のパスワードを入力して「OK」をクリックします。

   「ファイル形式が正しくないか、パスワードが正しくないため、秘密鍵証明書を読み込めませんでした」というエラーメッセージが表示される場合は、パスワードが有効であることを確認します。

## Acrobat Reader DC Extensions 証明書の削除 {#remove-a-acrobat-reader-dc-extensions-credential}

1. 管理コンソールで、設定/Trust Store の管理/ローカル秘密鍵証明書をクリックします。
1. 秘密鍵証明書を選択し、「削除」をクリックします。

## Acrobat Reader DC Extensions 証明書の置き換え {#replace-a-acrobat-reader-dc-extensions-credential}

1. 管理コンソールで、設定/Trust Store の管理/ローカル秘密鍵証明書をクリックします。
1. 既存の秘密鍵証明書のエイリアスをメモしておき、それを選択して「削除」をクリックします。
1. 同じエイリアス名を使用して新しい秘密鍵証明書を読み込みます。
