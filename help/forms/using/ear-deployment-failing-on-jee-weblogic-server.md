---
title: JEE WebLogic Server での EAR デプロイメントの失敗
seo-title: EAR Deployment failing on JEE Weblogic Server
description: JEE WebLogic Server での EAR デプロイメントの失敗を解決する手順
exl-id: 109d9182-5e3f-477e-9417-abc83d5ea3bc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
    internal-label: Experience Manager 6.5
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '98'
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

1. 最後に発生した `JAVA_OPTS` を検索し、`-DANTLR_USE_DIRECT_CLASS_LOADING=true` を追加します。 例えば、更新された文字列は次のように表示されます。

       set `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. 変更内容を保存します。
