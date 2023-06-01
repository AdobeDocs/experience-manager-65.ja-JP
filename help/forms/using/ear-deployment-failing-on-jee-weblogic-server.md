---
title: JEE WebLogic Server での EAR デプロイメントの失敗
seo-title: EAR Deployment failing on JEE Weblogic Server
description: JEE WebLogic Server での EAR デプロイメントの失敗を解決する手順
seo-description: Steps to resolve EAR Deployment failing on JEE Weblogic Server
source-git-commit: 45bb54a2666c2c196a8fb52795a7f428aa751e4d
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 10%

---


# JEE WebLogic Server での EAR デプロイメントの失敗 {#ear-deployment-failing-on-jee-weblogic-server}

## 問題 {#issue}

ユーザーが `adobe-livecycle-weblogic.ear`、 `Null Pointer` 例外が発生しました。

## 適用先 {#applies-to}

このソリューションは次の場合に適用されます。

* AEM Forms on WebLogic JEE サーバーバージョン 12.2.1.x

## ソリューション {#solution}

この問題を解決するには、次の手順に従います。

1. 次に移動： `<domain_home>\bin` インストールされている WebLogic JEE サーバーのディレクトリ。

1. を編集します。 `setDomainEnv.cmd` または `setDomainEnv.sh` ファイル、 `applicable`.

1. 最後に出現する `JAVA_OPTS` とを追加します。 `-DANTLR_USE_DIRECT_CLASS_LOADING=true` それに対して 例えば、更新された文字列は次のように表示されます。

       set &#39;JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true&#39;
   
1. 変更を保存します。


