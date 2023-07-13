---
title: OSGi バンドル
description: OSGi バンドルの管理に関するヒント
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 33%

---

# OSGi バンドル{#osgi-bundles}

## セマンティックバージョン管理を使用 {#use-semantic-versioning}

セマンティックバージョニング番号付けに関する合意に基づいたベストプラクティスについては、[https://semver.org/](https://semver.org/) を参照してください。

## OSGi バンドルで厳密に必要とされる以上のクラスや jar を埋め込まないでください。 {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

共通のライブラリは、別々のバンドルにファクタリングする必要があります。 これにより、バンドル間で再利用できます。 をラッピングする場合 *JAR* OSGi バンドルで、オンラインソースで、既にこの操作を実行しているかどうかを確認します。 既存のバンドルラッパーを見つける一般的な場所は次のとおりです。Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse バンドルレシピ、および SpringSource Enterprise バンドルリポジトリ。

## 最低限必要なバンドルバージョンに依存 {#depend-on-the-lowest-needed-bundle-versions}

POM ファイルのコンパイル時の依存関係の場合、必要な API を公開する、最も必要なバージョンに常に依存します。 これにより、後方互換性が高くなり、古いリリースへのバックポート修正が容易になります。

## OSGi バンドルから最小限のパッケージセットをエクスポートする {#export-a-minimal-set-of-packages-from-osgi-bundles}

パッケージが書き出されると、他のユーザーが依存する API が作成されます。 エクスポート対象を可能な限り少なくし、エクスポートされているものが API であることを確認してください。以前にエクスポートしたものを取得してプライベートにするよりも、プライベートメソッドまたはクラスを取得してパブリックにする方がはるかに簡単です。

実装は常に別の *impl* パッケージ。 デフォルトでは、 *maven-bundle-plugin* を持たないプロジェクト内のすべてを書き出します *impl* 名前に。

## エクスポートするパッケージごとに、常にセマンティックバージョンを明示的に定義する {#always-explicitly-define-a-semantic-version-for-each-package-exported}

これにより、API の利用者も同時に発展することができます。 定義の際には、必ずセマンティックバージョニングのベストプラクティスに従ってください。これにより、API の利用者は、新しいバージョンで予想される変更の種類を把握できます。

## 公開場所に関するメタタイプ情報を含める {#include-metatype-information-where-exposed}

意味のあるメタタイプ情報を指定することで、Felix コンソールでサービスやコンポーネントを理解しやすくなります。 SCR 注釈および属性のリストについては、[https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html) を参照してください。
