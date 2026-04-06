# Linkmux

リンクをクリックしたとき、どのブラウザで開くかを毎回選べる macOS アプリ。

![macOS](https://img.shields.io/badge/macOS-13.0+-000000?logo=apple)
![Swift](https://img.shields.io/badge/Swift-5-FA7343?logo=swift)

## ダウンロード

[Releases](../../releases) ページから最新の成果物をダウンロードしてください。

### インストール手順

1. `Linkmux.zip` を展開する
2. `Linkmux.app` を `/Applications` フォルダに移動する
3. **初回起動時の Gatekeeper 警告を回避する**
   - Finder で `Linkmux.app` を**右クリック → 開く**
   - 「開発元を確認できません」ダイアログで **「開く」** をクリック
   - 2回目以降は通常通りダブルクリックで起動できます
4. システム設定でデフォルトブラウザに設定する（[セットアップ](#セットアップ) 参照）

> **Note**
> Apple Developer 証明書による署名・公証を行っていないため、初回のみ上記の手順が必要です。

---

## 概要

Linkmux をデフォルトブラウザに設定すると、リンクをクリックするたびにブラウザ選択ダイアログが表示されます。用途に応じてブラウザを使い分けたい人向けのユーティリティです。

## 動作環境

- macOS 13 Ventura 以降
- Apple Silicon / Intel

## インストール

```bash
git clone <repository-url>
cd Linkmux
bash build.sh
```

`build.sh` は以下を自動で行います。

1. Swift ソースをコンパイル
2. `/Applications/Linkmux.app` にインストール
3. Launch Services へ登録

## セットアップ

1. アプリを起動する
   ```bash
   open /Applications/Linkmux.app
   ```

2. デフォルトブラウザに設定する
   **システム設定 → デスクトップと Dock → デフォルトの Web ブラウザ → Linkmux**

## 使い方

設定後はリンクをクリックするだけです。ブラウザ選択ダイアログが表示されるので、開きたいブラウザを選択してください。キャンセルは `Esc` キーで行えます。

## 対応ブラウザ

インストールされているブラウザを自動で検出します。

- Safari
- Google Chrome / Chrome Canary
- Firefox
- Microsoft Edge
- Brave
- Opera
- Vivaldi
- Kagi
- DuckDuckGo
- Arc
- Chromium

上記以外のブラウザを追加したい場合は `Sources/BrowserManager.swift` の `knownBundleIDs` に Bundle ID を追記して再ビルドしてください。

## ファイル構成

```
Linkmux/
├── Sources/
│   ├── main.swift               # エントリーポイント
│   ├── AppDelegate.swift        # URL イベントのハンドリング
│   ├── BrowserManager.swift     # ブラウザの検出・起動
│   └── BrowserPickerWindow.swift # ブラウザ選択 UI
├── Info.plist                   # アプリメタデータ・URL スキーム登録
└── build.sh                     # ビルド & インストールスクリプト
```

## リリース手順（開発者向け）

GitHub にリポジトリを作成して push したあと、バージョンタグを付けると GitHub Actions が自動でビルド・リリースを行います。

```bash
# 初回: リモートリポジトリを登録して push
git remote add origin <GitHub の URL>
git push origin main

# リリース: タグを打って push するだけ
git tag v1.0.0
git push origin v1.0.0
```

Actions が自動で以下を実行します：

1. Apple Silicon / Intel のユニバーサルバイナリをビルド
2. `Linkmux.zip` にパッケージング
3. GitHub Release を作成してアップロード

バージョンは [Semantic Versioning](https://semver.org/lang/ja/) に従って付けることを推奨します（例: `v1.0.0`, `v1.1.0`, `v2.0.0`）。

## ライセンス

[MIT](./LICENSE)

## 仕組み

macOS の URL ハンドリング機構を利用しています。

1. `Info.plist` に `http` / `https` の URL スキームハンドラとして登録
2. リンクがクリックされると Apple Events 経由で URL を受信
3. インストール済みブラウザの一覧をダイアログで表示
4. 選択されたブラウザで URL を開く

Linkmux 自体はバックグラウンドで常駐し、Dock には表示されません。
