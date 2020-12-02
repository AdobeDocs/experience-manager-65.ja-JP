---
title: フォントを使用可能にする
seo-title: フォントを使用可能にする
description: フォーム内で使用されているフォントが、AEM Forms をホストする J2EE アプリケーションサーバーで使用できることを確認します。
seo-description: フォーム内で使用されているフォントが、AEM Forms をホストする J2EE アプリケーションサーバーで使用できることを確認します。
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 96%

---


# フォントを使用可能にする {#make-fonts-available}

フォーム内で使用されているフォントが、AEM Forms をホストする J2EE アプリケーションサーバーで使用できることを確認します。例えば、次のようなシナリオが考えられます。フォーム開発者が、Designer で使用するフォントをフォントディレクトリに追加し、そのフォントを使用するフォームを別のコンピューターで作成します。Output サービスでそのフォントを使用するには、カスタマーフォントディレクトリにフォントを配置します。カスタマーフォントディレクトリが存在しない場合は、AEM forms をホストする J2EE アプリケーションサーバー上にディレクトリを作成します。

その他のフォント設定について詳しくは、「[一般的な AEM Forms の設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)」を参照してください。

**カスタマーフォントディレクトリの場所の指定**

1. 管理コンソールで、設定／コアシステム設定／設定をクリックします。
1. 「システムフォントディレクトリの場所」ボックスにカスタマーフォントディレクトリのパスを入力します。複数のディレクトリを追加する場合は、セミコロン&#x200B;**;**&#x200B;で区切ります。
1. 「OK」をクリックします。
1. AEM Forms がインストールされているシステムを再起動します。

>[!NOTE]
>
>フォントは Windows システムのフォントのキャッシュから選択されます。キャッシュを更新するにはシステムを再起動する必要があります。カスタマーフォントディレクトリを指定した後、AEM Forms がインストールされているシステムを再起動します。

