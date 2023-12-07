---
title: セーフバックアップモードの有効化と無効化
description: バックアップ設定ページでは、AEM forms をセーフバックアップモードで操作して、データベースとグローバルドキュメントストレージ (GDS) ディレクトリを確実にバックアップできます。 セーフバックアップモードを有効または無効にする方法を説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 6%

---

# セーフバックアップモードの有効化と無効化 {#enabling-and-disabling-safe-backup-mode}

バックアップ設定ページでは、AEM forms をセーフバックアップモードで操作して、データベースとグローバルドキュメントストレージ (GDS) ディレクトリを確実にバックアップできます。

AEM forms はセーフバックアップモードのときは、GDS ディレクトリからファイルをアクティブに削除しない点を除き、正常に動作します。

>[!NOTE]
>
>このオプションを設定しても、システムはバックアップされません。バックアップ用にシステムが準備されます。

## セーフバックアップモードを有効にする {#enable-safe-backup-mode}

1. 管理コンソールで、設定/コアシステム設定/バックアップ設定をクリックします。
1. [ バックアップ設定 ] ページで、[ セーフバックアップモードで動作 ] を選択し、[OK] をクリックします。

>[!NOTE]
>
>システムが既にセーフバックアップモードで実行されている場合、[OK] をクリックしても新しい予約は作成されません。

## セーフバックアップモードを無効にする {#disable-safe-backup-mode}

1. 管理コンソールで、設定/コアシステム設定/バックアップ設定をクリックします。
1. [ バックアップ設定 ] ページで、[ セーフバックアップモードで動作する ] の選択を解除し、[OK] をクリックします。
