---
title: JEE WebLogic Server での EAR デプロイメントの失敗
seo-title: EAR Deployment failing on JEE Weblogic Server
description: JEE WebLogic Server での EAR デプロイメントの失敗を解決する手順
seo-description: Steps to resolve EAR Deployment failing on JEE Weblogic Server
exl-id: b87a9eee-ee56-4dca-b4a3-a42c91db0b4f
source-git-commit: 1022e2676297141d5635ebbca49e170aee55367b
workflow-type: ht
source-wordcount: '103'
ht-degree: 100%

---

# JEE WebLogic Server での EAR デプロイメントの失敗 {#ear-deployment-failing-on-jee-weblogic-server}

## 問題 {#issue}

ユーザーが `adobe-livecycle-weblogic.ear` をデプロイしようとすると、`Null Pointer` 例外が発生します。

## 適用先 {#applies-to}

このソリューションは次の場合に適用されます。

* WebLogic 上の AEM forms サーバーバージョン 12.2.1.x

## 解決策 {#solution}

この問題を解決するには、次の手順に従います。

1. インストールされている WebLogic JEE サーバーの `<domain_home>\bin` ディレクトリに移動します。

1. `setDomainEnv.cmd` または `setDomainEnv.sh` ファイルを `applicable` として編集します。

1. 最後に発生した `JAVA_OPTS` を検索し、`-DANTLR_USE_DIRECT_CLASS_LOADING=true` を追加します。例えば、更新された文字列は次のように表示されます。

       set `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. 変更を保存します。
