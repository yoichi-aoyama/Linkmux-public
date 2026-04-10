# Linkmux

リンクをクリックしたとき、どのブラウザで開くかを毎回選べる macOS アプリ。

![macOS](https://img.shields.io/badge/macOS-13.0+-000000?logo=apple)

## ダウンロード

[Releases](https://github.com/yoichi-aoyama/Linkmux-public/releases) ページから最新版をダウンロードしてください。

## インストール

### Homebrew（推奨）

```sh
brew tap yoichi-aoyama/linkmux
brew install --cask linkmux
```

### 手動インストール

1. ダウンロードした `.dmg` を開き、`Linkmux.app` を `/Applications` フォルダにドラッグする
2. **システム設定 → デスクトップと Dock → デフォルトの Web ブラウザ → Linkmux** に設定する

## 使い方

設定後はリンクをクリックするだけです。ブラウザ選択ダイアログが表示されるので、開きたいブラウザを選択してください。`Esc` キーでキャンセルできます。

## 動作環境

- macOS 13 Ventura 以降
- Apple Silicon / Intel

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

## Google Chrome プロファイル対応 ※AppStore版は非対応

- ブラウザの一覧にプロファイルが表示されます。

## URL、ドメイン設定

- 特定のURL、ドメインを開くブラウザが決まっている場合は、設定しておくことでブラウザ選択をスキップできます。

<img width="464" height="408" alt="image" src="https://github.com/user-attachments/assets/2978b843-f7de-433d-98ae-f40aa6bc1ebe" />

## デフォルトブラウザ

- URL、ドメイン設定に該当しなかった場合にブラウザ選択ではなく、デフォルトブラウザで開くことができます。

## ライセンス

[MIT](./LICENSE)
