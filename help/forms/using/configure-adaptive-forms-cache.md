---
title: アダプティブフォームのキャッシュの設定
seo-title: アダプティブフォームのキャッシュの設定
description: 'アダプティブフォームのキャッシュは、アダプティブフォームおよびアダプティブドキュメント向けに設計されています。これは、クライアント側のアダプティブフォームまたはドキュメントのレンダリングの時間を短縮する目的で、アダプティブフォームとアダプティブドキュメントをキャッシュします。 '
seo-description: 'アダプティブフォームのキャッシュは、アダプティブフォームおよびアダプティブドキュメント向けに設計されています。これは、クライアント側のアダプティブフォームまたはドキュメントのレンダリングの時間を短縮する目的で、アダプティブフォームとアダプティブドキュメントをキャッシュします。 '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# アダプティブフォームのキャッシュの設定{#configure-adaptive-forms-cache}

キャッシュは、データへのアクセスにかかる時間を短縮し、遅延を削減して I/O 速度を改善するメカニズムです。アダプティブフォームのキャッシュは、アダプティブフォームの HTML コンテンツと JSON の構造のみを保存し、事前入力されたデータは保存しません。これにより、クライアント側のアダプティブフォームまたはドキュメントのレンダリングの時間を短縮します。キャッシュは、アダプティブフォーム向けに設定されており、アダプティブドキュメントもサポートします。 

>[!NOTE]
>
>アダプティブフォームのキャッシュを使用するときは、AEM Dispatcher を使用してアダプティブフォームまたはアダプティブドキュメントのクライアントライブラリ（CSS および JavaScript）をキャッシュします。

>[!NOTE]
>
>カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。

## キャッシュの設定 {#configure-the-cache}

次の手順を実行して、アダプティブフォームのキャッシュを設定します。

1. Go to AEM web console configuration manager at https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. 「**アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定**」をクリックして、設定値を編集します。
1. In the edit configuration values dialog, specify the maximum number of forms or documents an instance of the AEM Forms server can cache in the **Number of Adaptive Forms** field. デフォルト値は 100 です。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュの設定を無効にしたり変更したりすると、ドキュメントがリセットされ、すべてのフォームとキャッシュがキャッシュから削除されます。

   ![アダプティブフォームの HTML キャッシュの設定ダイアログ](assets/cache-configuration-edit.png)

1. 「**Save**」をクリックして、 設定を保存します。

