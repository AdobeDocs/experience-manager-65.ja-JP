---
title: AEM Forms アプリケーションのトラブルシューティング
seo-title: AEM Forms アプリケーションのトラブルシューティング
description: AEM Forms アプリケーションの一般的な問題と、そのトラブルシューティングについて説明します。
seo-description: AEM Forms アプリケーションの一般的な問題と、そのトラブルシューティングについて説明します。
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 56%

---

# AEM Forms アプリケーションのトラブルシューティング {#troubleshoot-aem-forms-app}

この記事では、AEM Forms アプリケーションの構築中に表示される可能性のあるエラーメッセージとその解決方法について説明します。

この記事のセクションは次のとおりです。

* [iOS ユーザーの添付ファイルが失われる](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Workspace ユーザーによって送信された HTML5 フォームドラフトがポータルに表示されない](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [キャッシュされていない HTML5 フォームを AEM Forms アプリケーションに読み込むことができない](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms が Windows で同期されない](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Gradle のサポートされていないバージョン](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle と Android Gradle プラグインの互換性の問題](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS ユーザーの添付ファイルが失われる {#attachment-loss-for-ios-users}

OSGi 上の AEM Forms と同期するように設定された iOS 用の AEM Forms アプリケーションは、フィールドレベルの添付ファイルのみをサポートします。すべての添付ファイルには一意の名前が付いている必要があります。複数の添付ファイルに同じ名前が付いている場合、1 つの添付ファイルのみが保持され、同じ名前が付いている他のすべての添付ファイルは失われます。iOS デバイスのユーザーがデータを損失するのを回避するには、次の手順を実行します。

1. 接続されているサーバーで、**Adobe Experience Manager/ツール/運営/Webコンソール**&#x200B;に移動します。
1. 「**[!UICONTROL アダプティブフォームとインタラクティブ通信Webチャネルの設定]**」を探してクリックします。
1. [!UICONTROL アダプティブフォームとインタラクティブ通信Webチャネルの設定]ダイアログで、「**ファイル名を一意にする**」を有効にします。

   「 **ファイル名を一意にする** 」設定が無効になっている場合、複数の添付ファイルを含むアダプティブフォームを送信しようとすると、データが失われます。

1. 「**保存**」をクリックします。

## Workspace ユーザーによって送信された HTML5 フォームドラフトがポータルに表示されない  {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

AEM Formsアプリで&#x200B;**Save as Draft** HTML Render Profileを使用してHTML5フォームを有効にした場合、保存したドラフトはWorkspaceユーザーに表示されません。 Workspaceユーザーによって送信されたHTML5フォームの保存済みドラフトをポータル上に表示するには、次の手順を実行します。

1. CRXDE を開いて管理者の資格情報でログインします。

   URL：`https://<server>:<port>/lc/crx/de/index.jsp`

1. CRXDE のルートパスにある「アクセス制御」の「アクセス制御リスト」で、**+** をクリックします。
1. **新しいエントリを追加**&#x200B;ダイアログで、「プリンシパル」フィールドのグループ検索ボタンをクリックします。
1. プリンシパルを選択ダイアログの「名前」フィールドに`PERM_WORKSPACE_USER`と入力し、「**検索**」をクリックします。
1. プリンシパルを選択ダイアログで`PERM_WORKSPACE_USER`グループを選択し、「**OK**」をクリックします。
1. 新しいエントリを追加ダイアログの「プリンシパル」フィールドで、`PERM_WORKSPACE_USER` グループが選択された状態になります。

   ユーザーグループの`jcr:read`権限を有効にします。

1. 「**OK**」をクリックします。

## キャッシュされていない HTML5 フォームを AEM Forms アプリケーションに読み込むことができない {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

AEM Forms アプリケーションが古いバージョンの AEM Forms サーバーに接続している場合、キャッシュされていない HTML5 フォームを AEM Forms アプリケーションに読み込むことができません。

問題を解決するには、以下の手順を実行します。

1. オーサーインスタンスで、**Adobe Experience Manager/ツール/Workspace App Offline Serviceを設定/今すぐ設定**&#x200B;に移動します。
1. **Workspace App Offline Service**&#x200B;ページで、「**手動のリソースキャッシュ**」をクリックします。

   URL：https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. 「**手動リソースキャッシュ**」タブで、「**+**」ボタンをクリックしてCRXパスを追加します。
1. **Add a New Resource**&#x200B;フィールドに、次のように入力します。/etc.clientlibs/fd/xfaforms/I18N/en_US.jsを開き、「**追加**」をクリックします。
1. 「**保存**」をクリックします。

## AEM Forms が Windows で同期されない  {#aem-forms-do-not-sync-on-windows}

Windows の AEM Forms アプリケーションでは、フォームまたはそのリソースのいずれかへのパスが 256 文字以上の場合、フォームは接続されたサーバーと同期されません。

フォームとそのリソースへのパスを変更して、文字数を 256 文字よりも少なくしてください。

## Gradle のサポートされていないバージョン  {#unsupported-version-of-gradle}

**エラーメッセージ：** プロジェクトはGradleのサポートされていないバージョンを使用しています。

Android Studio で AEM Forms アプリケーションを構築すると、エラーメッセージが表示されます。この問題は、システムでサポートされる Gradle のサポート対象でないバージョンにより発生します。

**解決方法：** 「Fix  **Gradle wrapper」をクリックし、プロジェクトを再インポ** ートして問題を解決します。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle と Android Gradle プラグインの互換性の問題 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**エラーメッセージ：** Android GradleプラグインとGradleのバージョンに互換性がありません。

Android Studioユーザーインターフェイスの&#x200B;**Build**&#x200B;メニューから「**Build APK**」オプションを選択すると、エラーメッセージが表示されます。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**解決方法：**  **Gradle Scripts** / **gradle-wrapper.** propertiesファイルを開き、distributionUrlプロパティを編 **** 集します。

例えば、Android Studioコンソールでは、Gradleのバージョンを3.5にダウングレードすることをお勧めします。**distributionUrl**（**gradle-wrapper.properties**&#x200B;ファイル）でバージョンを編集します。

**Build** > **Build APK**&#x200B;を再度選択してエラーを解決し、.apkファイルを生成します。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
