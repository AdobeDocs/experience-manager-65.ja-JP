---
title: 早期導入機能とプレリリース機能を統合するために、機能切替スイッチを有効にする
description: 機能切替スイッチは、管理者がランタイム環境で新機能を有効にできる AEM の機能です。
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
exl-id: 08815c2b-23b3-4545-a3ab-ba47ba1c3c55
source-git-commit: 0915f8a65b1a9697eaca95be3ef9a786a1071fe5
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 90%

---

# Adobe Experience Manager（AEM）6.5 の機能切替スイッチ{#enable-feature-toggle-aem-forms-65}

機能切替スイッチは、管理者が特定の機能を動的に有効または無効にできる AEM の機能です。この機能は、大規模なデプロイメントやコードベースの変更を必要とせずに、**早期導入機能**&#x200B;や&#x200B;**プレリリース機能**&#x200B;を管理する場合に特に役立ちます。これにより、AEM 環境でアクセスできる機能に対する柔軟性と制御が確保されます。

## AEM 6.5 設定で機能切替スイッチを使用する理由

AEM 6.5 設定で作業する場合、機能切替スイッチは次の点で役立ちます。

* 実験的な機能を安全にテストする。

* 新しいコンポーネントを段階的にロールアウトする。

* 複数の環境で単一のコードベースを維持する。

* デプロイメントとアップグレードの際のリスクを軽減する。

## 考慮事項

AEM 6.5 SP23 以降では、[com.adobe.granite.toggle.impl.dev](http://com.adobe.granite.toggle.impl.dev/) バンドルがForms アドオンと共にインストールされているので、前提条件の手順を実行する必要はありません。

## 前提条件

AEM 6.5 設定で機能切替スイッチを有効にする前に、次を確認します。

* ユーザーが `forms-users` グループのメンバーである。

* `http://<author-instance-url>:portnumber/system/console/bundles` に移動し、**（com.adobe.granite.toggle.impl.dev-1.1.8.jar）** バンドルが存在するかどうかを確認します。 存在しない場合は、[リンクからバンドルをダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fcom.adobe.granite.toggle.impl.dev-1.1.8.jar)します。

![機能切替スイッチ](/help/forms/using/assets/feature-toggle-1.1.8.png)

## 機能切替スイッチの有効化 {#enable-feature-toggle-65}

早期導入用の機能切替スイッチや新機能は、次の手順に従って、**AEM web コンソール**&#x200B;を通じて設定できます。

1. AEM Forms インスタンスにログインします。
2. `http://<author-instance-url>:portnumber/system/console/configMgr` に移動します。
3. Configuration Manager で **Adobe Granite Dynamic Toggle Provider** を検索します。
4. アイコン ![鉛筆アイコン](assets/illustratorcc_penciltool_cur_edit_2_17.png) をクリックします。
5. 「[!UICONTROL 有効な切替スイッチ]」セクションで、![鉛筆アイコン](assets/aem6forms_add.png) をクリックします。
6. 以下の画像に示すように、機能の機能切替スイッチ ID を追加します。
   ![機能切替スイッチの追加](assets/add_toggle_number_forms.png)

   >[!NOTE]
   >
   >機能切替スイッチ ID は、早期導入機能に固有のドキュメントで確認できます。

7. 「保存」をクリックします。

## 機能切替スイッチの無効化 {#disable-feature-toggle-65}

切替スイッチが有効になっている機能の機能切替スイッチを無効にするには、次の手順に従います。

1. AEM Forms インスタンスにログインします。
2. `http://<author-instance-url>:portnumber/system/console/configMgr` に移動します。
3. Configuration Manager で **Adobe Granite Dynamic Toggle Provider** を検索します。
4. アイコン ![鉛筆アイコン](assets/illustratorcc_penciltool_cur_edit_2_17.png) をクリックします。
5. 「[!UICONTROL 無効な切替スイッチ]」セクションで、![鉛筆アイコン](assets/aem6forms_add.png) をクリックします。
6. 無効にする機能の切替スイッチ番号を追加します。
   ![切替スイッチの削除](assets/remove_toggle_feature_forms.png)
7. 「保存」をクリックします。

## 技術的な考慮事項

機能切替スイッチは環境に固有で、実行時に管理されるので、サーバーの再起動は必要ありません。 ただし、一部の機能では、変更を反映するために、関連するページを更新したり、キャッシュを消去したりする必要がある可能性があります。
`http://<author-instance-url>:4502/etc.clientlibs/toggles.json` 経由で、環境の機能切替スイッチを通じて有効になっている機能のリストにアクセスできます。
