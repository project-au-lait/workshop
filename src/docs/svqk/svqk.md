---
marp: true
paginate: true
---
# SVQK
## Web Application Development Platform
## using Svelte + Quarkus + Playwright

<style scoped>
section {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
---
# Agenda

- 発表者紹介
- Project Au Laitとは
- SVQKとは
- Demo (1 ~ 7)
- Q&A
- まとめ

---
# 発表者紹介

- [発表者](presenter.html)

---
# Project Au Lait

- ミッション
  - システム開発に役立つツールの開発
  - システム開発に携わるエンジニアの作業を自動化・効率化することで、システムの品質向上に寄与することを目指す
- キャッチフレーズ
  - システム開発のほろ苦さをまろやかに
- ロゴ
  <img src="https://aulait.dev/logo.svg" width="18%"/>

---
# プロダクト紹介

- SVQK
  - Svelte(Frontend) + Quarkus(Backend)でWebアプリケーションを開発するための開発プラットフォーム
- 特徴
  - **自動環境構築**：DB構築やE2Eテストなど、Webアプリケーションを動かしてテストするための環境構築手順を自動化、コマンド1つで実行可能
  - **自動テスト**：ユニットテスト、統合テスト、E2Eテストを自動化、CI上で実行可能
  - **コード自動生成**：データベースのテーブル定義からCRUDページと自動テストコードを生成する機能を具備

---
# Demo

1. プロジェクト作成
2. セットアップ
3. プロジェクト構成
4. 開発環境の使用方法
5. E2Eテスト
6. コード自動生成
7. 開発者向けドキュメント

---
# 1/7  プロジェクト作成

SVQKはMaven Archetypeとして使用
以下のコマンドでプロジェクトを作成

```sh
mvn archetype:generate \
  -DarchetypeGroupId=dev.aulait.svqk \
  -DarchetypeArtifactId=svqk-archetype-refimpl \
  -DarchetypeVersion=0.9.1 \
  -DgroupId=my.group.id  \
  -DartifactId=my-artifactid \
  -Dversion=1.0-SNAPSHOT
```

`archetypeArtifactId`にはsvqk-archetype-refimpl、svqk-archetype-arch、svqk-archetype-skeletonが指定可能
->[Quick Start](https://aulait.dev/#svqk) `archtypeの種類`を参照

---
# 2/7  セットアップ

以下のコマンドでセットアップを実行

```sh
cd my-artifactid
chmod u+x mvnw
# セットアップコマンド
./mvnw install -T 1C -P setup

# [任意] プロジェクト資材の初期状態をコミット
git init && git add . && git commit -m "initial commit"
```

->[Quick Start](https://aulait.dev/#svqk) `セットアップコマンドの処理内容`を参照

---
# 3/7  プロジェクト構成

作成したプロジェクトはSvelteKit、Quarkus、Playwrightの各開発ツールで生成したサブプロジェクトを持つ

```
📁 my-artifactid 
├── 📁 my-artifactid-backend   <--- Quarkus (mvn quarkus:create)
│   └── 📄 pom.xml
├── 📁 my-artifactid-e2etest   <--- Playwright (pnpm create playwright)
│   ├── 📄 package.json
│   └── 📄 pom.xml
├── 📁 my-artifactid-frontend  <--- SvelteKit (npx sv create)
│   ├── 📄 package.json
│   └── 📄 pom.xml
└── 📄 pom.xml
```

->各サブプロジェクトの構成・使用方法は各開発ツールで個別に生成した場合と同様

---
# 4/7  開発環境の使用方法

SVQKのプロジェクトはVSCode Workspaceとして使用可能

```sh
code my-artifactid.code-workspace
```

開発環境の操作はVSCodeから実行可能

- DB参照: VSCode Command Pallet: `SQLTools: Focus on Connections View`
- Backend起動: VSCode Task: `start-backend`
- Frontend起動: VSCode Task: `start-frontend`

->その他の操作やコマンドで実行する方法は[実装ガイド](https://aulait.dev/svqk/0.9.1/ja/impl-guide/index.html#project-usage)を参照

---
# 5/7  E2Eテスト

E2Eテストのプロジェクト構成・周辺ツールの使用方法は従来のPlaywrightのものと同様
- VSCodeからテスト実行
- テストレポート

テストはCIサーバー上で一括実行可能
- テスト実行前後のDB・Frontend・Backendの起動・停止等を含む
- セットアップコマンドに統合

---
# 6/7  コード自動生成

プロジェクトはコード自動生成ツールを同梱(my-artifactid-generator)
テーブルに対するCRUD操作を行うページ・APIと自動テストを生成

- VSCode Task: `generate`
  - `Select components` -> all
  - `Enter tables` -> world

---
# 7/7 開発者向けドキュメント

プロジェクトはアーキテクチャ記述、実装ガイドを同梱(skeleton以外のarchtype)
VSCode Task: `gen-docs` でadocからhtmlを生成

```
📁 my-artifactid
├── 📁 my-artifactid-docs
│   ├── 📄 pom.xml  <-------------  Asciidoctorの設定
│   └── 📁 src/docs/asciidoc/ja
│       ├── 📁 arch-desc  <------  アーキテクチャ記述のadoc
│       │   └── 📄 index.adoc
│       └── 📁 impl-guide  <------  実装ガイドのadoc
│           └── 📄 index.adoc
└── 📁 docs/${project.version}/ja
    ├── 📁 arch-desc
    │   └── 📄 index.html  <------  アーキテクチャ記述(adocから生成)
    └── 📁 impl-guide
        └── 📄 index.html  <------  実装ガイド(adocから生成)
```


---
# Q & A

## Demo

1. プロジェクト作成
2. セットアップ
3. プロジェクト構成
4. 開発環境の使用方法
5. E2Eテスト
6. コード自動生成
7. 開発者向けドキュメント

---
# まとめ

- **Project Au Lait**: システム開発を効率化するツールを提供
  - エンジニアの作業を効率化し、品質向上を目指す
- **SVQK**: Svelte + Quarkusを活用したWebアプリケーション開発プラットフォーム
  - 自動環境構築、テスト自動化、コード自動生成で開発効率を向上
  - 今回のDemoの手順は[Project Au Lait プロジェクトサイト](https://aulait.dev)の`Quick Start`を参照
- **Follow Us**: 
  - [X](https://x.com/prj_au_lait_jp): SVQKのリリース情報やProject Au Laitの活動に関する情報
  - [Blog](https://zenn.dev/prj_au_lait_jp): SVQKやその他Project Au Laitのプロダクトの解説記事
  - [GitHub](https://github.com/project-au-lait/svqk): SVQKのソースコード　応援☆Star募集中

---
# ご清聴ありがとうございました。