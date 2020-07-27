---
title: AEM 6.5 Forms へのアップグレード
seo-title: AEM 6.5 Forms へのアップグレード
description: AEM 6.1 Forms、AEM 6.2 Forms、LiveCycle ES4 SP1 を、AEM 6.3 Forms に直接アップグレードすることができます。
seo-description: AEM 6.1 Forms、AEM 6.2 Forms、LiveCycle ES4 SP1 を、AEM 6.3 Forms に直接アップグレードすることができます。
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 63%

---


# OSGi 上の AEM 6.5 Forms へのアップグレード {#upgrade-to-aem-forms-osgi}

AEM 6.3 Forms と AEM 6.4 Forms の場合、AEM 6.5 Forms へ直接アップグレードすることができます。

**AEM 6.0 Forms、AEM 6.1 Forms**、 **** AEM 6.2 FormsからAEM 6.5 Formsへの直接アップグレードパスは使用できません。 Perform an intermediate [upgrade to AEM 6.2 Forms](https://helpx.adobe.com/jp/experience-manager/6-2/forms/using/upgrade.html), [upgrade to AEM 6.3 Forms](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/upgrade.html), or [upgrade to AEM 6.4 Forms](/help/forms/using/upgrade.md) and then upgrade from AEM 6.3 Forms, or AEM 6.4 Forms to AEM 6.5 Forms.

Do the following to upgrade from AEM 6.3 Forms or AEM 6.4 Forms to AEM 6.5 Forms:

1. 既存の AEM インスタンスを AEM 6.5 にアップグレードします。手順は次のとおりです。

   1. AEM 6.3 Forms または AEM 6.4 Forms の最新のサービスパックおよびパッチをインストールします。詳しくは、 [AEMメンテナンスハブを参照してください](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html)。
   1. アップグレードのソースインスタンスを準備します。詳しくは、「[AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md)」を参照してください。
   1. [AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software) をダウンロードします。
   1. **（Unix/Linux ベースのインストールのみ）** 基盤のオペレーティングシステムとして UNIX または Linux を使用している場合は、ターミナルウィンドウを開いて crx-quickstart が含まれているフォルダーに移動し、次のコマンドを実行します。

      `chmod -R 755 ../crx-quickstart`

   1. Upgrade your AEM instance to AEM 6.3. For step by step instructions, see [Upgrading to AEM 6.5](/help/sites-deploying/upgrade.md).

      次の手順に進む前に、ServiceEvent REGISTERED および ServiceEvent UNREGISTERED メッセージが &lt;crx-repository>/error.log ファイルに出現しなくなるまで待ちます。

      >[!NOTE]
      >
      >サーバーが起動して実行した後、いくつかの AEM Forms バンドルはインストール状態のままです。バンドルの数はインストールごとに異なる可能性があります。これらのバンドルの状態は無視しても問題はありません。The bundles are listed at https://&#39;[server]:[port]&#39;/system/console/.

1. AEM Forms アドオンパッケージのインストール. 手順は次のとおりです。

   1. Open [Software Distribution](https://experience.adobe.com/downloads)（ソフトウェア配布）。 Adobe IDがソフトウェア配布物にログインする必要があります。
   1. ヘッダーメニューで **[!UICONTROL Adobe Experience Manager]** をタップします。
   1. In the **[!UICONTROL Filters]** section:
      1. 「 **[!UICONTROL ソリューション]** 」ドロップダウンリストから「 **[!UICONTROL フォーム]** 」を選択します。
      1. パッケージのバージョンと種類を選択します。 また、「 **[!UICONTROL 検索のダウンロード数]** 」オプションを使用して結果をフィルターすることもできます。
   1. お使いのオペレーティングシステムに対応するパッケージ名をタップし、「EULA条項に **[!UICONTROL 同意します]**」を選択して、「 **[!UICONTROL ダウンロード]**」をタップします。
   1. パッ [ケージマネージャーを開き](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/contentmanagement/package-manager.html) 、「パッケージを **[!UICONTROL アップロード]** 」をクリックしてパッケージをアップロードします。
   1. Select the package and click **[!UICONTROL Install]**.

      「 [AEM Formsリリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) 」記事に一覧表示されている直接リンクを使用して、パッケージをダウンロードすることもできます。

      >[!NOTE]
      >
      >パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**その際、すぐにサーバーを停止しないでください。** AEM Forms サーバーを停止する前に、ServiceEvent REGISTERED メッセージと ServiceEvent UNREGISTERED メッセージが &lt;crx-repository>/error.log ファイルに表示されなくなり、このログファイルが安定した状態になるまで待ちます。また、いくつかのパッケージについては、インストールされたままの状態になる場合があることに注意してください。これらのパッケージは、無視してかまいません。

1. AEM インスタンスを再起動します。

1. インストールの事後処理を実行します。

   * **移行ユーティリティの実行**

      移行ユーティリティにより、以前のバージョンのアダプティブフォームや対応する管理アセットが AEM 6.5 Forms で使用できるようになります。このユーティリティは、AEMソフトウェア配布からダウンロードできます。 移行ユーティリティの詳しい設定方法と使用方法については、[移行ユーティリティ](../../forms/using/migration-utility.md)に関する説明を参照してください。

      [ドラフト統合とコンポーネント送信のサンプル](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)をデータベースで使用して旧バージョンのアップグレードを行う場合は、アップグレードの実行後に、以下の SQL クエリを実行してください。

      ```sql
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```sql
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **（AEM 6.2 Formsまたは以前のバージョンからアップグレードした場合のみ）Adobe Signの再設定**

      Adobe Sign を以前のバージョンの AEM Forms で設定してある場合は、AEM Cloud サービスから Adobe Sign を再設定します。詳細については、「[Adobe Sign を AEM Forms に統合する](../../forms/using/adobe-sign-integration-adaptive-forms.md)」を参照してください。

   * **jQueryのサポート**

      AEM 6.5 Formsでは、jQueryのバージョンが3.2.1に更新され、jQuery UIのバージョンが1.12.1に更新されます。AEM Formsでは **noConflict** モードでJQueryを使用します。 したがって、他のjQueryバージョンを使用している場合、アップグレードの実行中に問題は表示されません。 ただし、AEM 6.5 Formsにアップグレードする場合は、次の手順を実行します。

      * カスタムコンポーネントが存在する場合は、そのコンポーネントが、サポートされているjQueryバージョンと互換性があることを確認します。
      * カスタムコンポーネントからサポートされていないAPIを削除します。 削除されたAPIのリストについては、 [アップグレードガイド](https://jquery.com/upgrade-guide/3.0/) を参照してください。 例えば、load()、.unload()、および.error() APIのサポートは削除されました。 前述のAPIの代わりに.on()メソッドを使用します。 例えば、$(&quot;img&quot;).load(fn)を$(&quot;img&quot;).on(&quot;load&quot;, fn)に変更します。
   * **分析機能とレポートの再設定（バージョン 6.2 以前の AEM Forms をアップグレードする場合のみ）** 

      AEM 6.4 Forms では、ソースのトラフィック変数とインプレッションの成功イベントは利用できません。そのため、バージョン 6.2 以前の AEM Forms をアップグレードすると、AEM Forms から Adobe Analytics サーバーにデータが送信されなくなり、アダプティブフォームの分析レポートが使用できなくなります。また、AEM 6.4 Forms には、フォームバージョン分析用のトラフィック変数と、フィールドの処理時間に関する成功イベントが導入されています。このため、AEM Forms 環境で分析とレポートを再設定してください。詳しい手順については、「[分析とレポートの設定](../../forms/using/configure-analytics-forms-documents.md)」を参照してください。


1. サーバーのアップグレードが成功し、すべてのデータが正常に移行され、問題なく動作することを確認してください。

   * **バンドルのステータスを確認：**&#x200B;すべてのバンドルがアクティブ状態になっていることを確認します。
   * **複製と逆複製を確認：**&#x200B;移行されたフォームをいくつか発行、記入、送信します。送信済みデータも確認します。
   * **管理者および開発者のユーザーインターフェースへのアクセスを確認：**&#x200B;管理者アカウントで AEM インスタンスにログインし、次の URL にアクセスできるか確認します。

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   AEM 6.4 Forms では crx-repository の構造が変更されています。6.3 FormsからAEM 6.5 Formsにアップグレードする場合は、新しく作成するカスタマイズ用に変更したパスを使用します。 変更後のパスの一覧については、「[AEM Forms におけるリポジトリの再構築](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)」を参照してください。

