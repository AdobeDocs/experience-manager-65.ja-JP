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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 59%

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

1. On the connected server, navigate to **Adobe Experience Manager > Tools > Operations > Web Console**.
1. 「**Adaptive Form 設定サービス**」を検索してクリックします。
1. Adaptive Form 設定サービスダイアログで、「**ファイル名を一意にする**」を有効にします。

   If **Make File Names Unique** setting is disabled, users experience data loss if they try to submit adaptive forms with multiple attachments.

1. 「**保存**」をクリックします。

## Workspace ユーザーによって送信された HTML5 フォームドラフトがポータルに表示されない {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

For HTML5 forms enabled in AEM Forms app with **Save as Draft** HTML Render Profile, the saved drafts are not visible to workspace users. Workspaceユーザーが送信したHTML5フォームのドラフトをポータル上に表示保存するには、次の手順を実行します。

1. CRXDE を開いて管理者の資格情報でログインします。

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. CRXDE のルートパスにある「アクセス制御」の「アクセス制御リスト」で、**+** をクリックします。
1. **新しいエントリを追加**&#x200B;ダイアログで、「プリンシパル」フィールドのグループ検索ボタンをクリックします。
1. In the Name field of the Select Principal dialog, type `PERM_WORKSPACE_USER` and click **Search**.
1. Select `PERM_WORKSPACE_USER` group in the Select Principal dialog and click **OK**.
1. 新しいエントリを追加ダイアログの「プリンシパル」フィールドで、`PERM_WORKSPACE_USER` グループが選択された状態になります。

   Enable `jcr:read` privileges for the user group.

1. 「**OK**」をクリックします。

## キャッシュされていない HTML5 フォームを AEM Forms アプリケーションに読み込むことができない {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

AEM Forms アプリケーションが古いバージョンの AEM Forms サーバーに接続している場合、キャッシュされていない HTML5 フォームを AEM Forms アプリケーションに読み込むことができません。

問題を解決するには、次の手順を実行してください。

1. In author instance, navigate to **Adobe Experience Manager > Tools > Configure Workspace App Offline Service > Configure Now**.
1. In **Workspace App Offline Service** page, click **Manual Resource Cache**.

   URL：https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. In the **Manual Resource Cache** tab, click the **+** button to add a CRX path.
1. In the **Add a New Resource** field, type: /etc.clientlibs/fd/xfaforms/I18N/en_US.js and click **Add**.
1. 「**保存**」をクリックします。

## AEM Forms が Windows で同期されない {#aem-forms-do-not-sync-on-windows}

Windows の AEM Forms アプリケーションでは、フォームまたはそのリソースのいずれかへのパスが 256 文字以上の場合、フォームは接続されたサーバーと同期されません。

フォームとそのリソースへのパスを変更して、文字数を 256 文字よりも少なくしてください。

## Gradle のサポートされていないバージョン {#unsupported-version-of-gradle}

**エラーメッセージ：** プロジェクトでサポートされていないバージョンのGradleが使用されています。

Android Studio で AEM Forms アプリケーションを構築すると、エラーメッセージが表示されます。この問題は、システムでサポートされる Gradle のサポート対象でないバージョンにより発生します。

**解像度：** 「 **Fix Gradleラッパー」をクリックし、プロジェクトを再度インポートして** 、問題を解決します。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle と Android Gradle プラグインの互換性の問題 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**エラーメッセージ：** Android GradleプラグインとGradleのバージョンに互換性がありません。

The error message is displayed when you select **Build APK** option from the **Build** menu on the Android Studio user interface.

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**解像度：** Gradle Scripts **/** gradle-wrapper.properties **ファイルを開き、** distributionUrl **** プロパティを編集します。

For example, the Android Studio console recommends downgrading the Gradle version to 3.5. Edit the version in **distributionUrl** of **gradle-wrapper.properties** file.

Select **Build** > **Build APK** again to resolve the error and generate the .apk file.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

