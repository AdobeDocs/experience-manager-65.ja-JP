---
title: 設定ファイルの読み込みと書き出し
description: サーバーの環境設定を編集したり、別の AEM Forms 製品のインスタンスを設定したりするために、設定ファイルの読み込みと書き出しを行う方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '252'
ht-degree: 100%

---

# 設定ファイルの読み込みと書き出し {#importing-and-exporting-the-configuration-file}

手動設定ページを使用して、設定のコピーを XML 形式でダウンロードできます。このファイル内の設定で、サーバーのすべての環境設定が制御されます。ダウンロード後にファイルを編集し、サーバーにアップロードできます。また、このファイルを使用して、別の AEM Forms 製品のインスタンスを設定できます。

セキュリティ上の問題を防ぐため、ディレクトリサーバーのバインドパスワード値は、書き出された設定ファイルに含まれません。XML ファイルを新しいシステムに読み込む前に、そのファイル内のパスワードを更新します。

>[!NOTE]
>
>設定ファイルを読み込むと、ファイル内の情報に基づいて AEM Forms が再設定されます。設定ファイルを変更するのに適しているのは、システム管理者または AEM Forms 製品と XML に精通したプロのサービスコンサルタントだけです。設定ファイルを編集する必要があるのは、例えば、破損した設定を再指定する場合です。

**設定情報の書き出し**

1. 管理コンソールで、設定／User Management／設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 「書き出し」をクリックします。Microsoft Internet Explorer を使用している場合は、ファイルの保存場所を指定するように求めるプロンプトが表示されます。Firefox を使用している場合は、ファイルはデスクトップに保存されます。

**設定情報の読み込み**

1. 管理コンソールで、設定／User Management／設定／既存の設定ファイルの読み込みと書き出しをクリックします。
1. 「参照」をクリックして設定ファイルを探し、「読み込み」をクリックして「OK」をクリックします。
