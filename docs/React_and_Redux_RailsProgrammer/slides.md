# RailsプログラマのためのReact + Redux TDD with 西脇.rb & 神戸.rb
## Jest

rito

2017/07/22

---

## 目次
- - -
　
- フロントエンドテスト事情
　
- テストツール
　
- セットアップ
　
　
　
　

---

## フロントエンドテスト事情
- - -
　
皆さんに質問です
　
- テストって書いてますか？
　
- 書いているならどんなテストしてますか？
　
　
　
　
　

---

## フロントエンドテスト事情
- - -
　
JavaScriptでDOMを書き換えるような画面がある場合は
　
どうやってテストしていますか？
　
- E2Eでカバー？

- JavaScript自体のテストを実施？

- 実施しない？
　

---

## フロントエンドテスト事情
- - -
　
数あるフロントエンドのテストフレームワークで
　
 :spades: :hearts: <span style="font-size: 100px;"> Jest </span> :clubs: :diamonds:
　
を紹介します
　
　
　

---

## テストツール
- - -
　
少し前までの（私の周り）トレンド？は
　
- テスト環境：「mocha」
　　　　　　　　＋
- アサート：「chai」 or 「power-assert」
　

の組み合わせで使用
　
　
　
　

---

## テストツール
- - -
　
　
　
　
じゃあJestって何ができるの？
　
　
　
　
　
　
---

## テストツール
- - -
Jestが持っている主な機能
　
- テスト環境
- アサート
- モック、スタブ
- スナップショットテスト
- 変更監視による自動実行（watch）機能
- （カバレッジ等の）レポート機能
　

Jest単体でテストに最低必要な機能は持っています
　

---

## テストツール
- - -
もちろんJest以外のものもあるので一応紹介　※[参照](https://medium.com/powtoon-engineering/a-complete-guide-to-testing-javascript-in-2017-a217b4cd5a2a)
　
- テストの環境を提供する
  Mocha、Jasmine、AVA、<span style='color:red'>Jest</span>、Karma
- テストの構造を提供する
  Mocha、Jasmine、AVA、<span style='color:red'>Jest</span>、Cucumber
- アサーション機能を提供する
  Chai、Jasmine、AVA、<span style='color:red'>Jest</span>、Unexpected
- 生成、表示、テスト結果をウォッチする
  Mocha、Jasmine、AVA、<span style='color:red'>Jest</span>、Karma

---

## テストツール
- - -
- コンポーネント構造のスナップショットを比較する
  AVA、<span style='color:red'>Jest</span>
- モック、スパイ、スタブを提供する
  Sinon、Jasmine、enzyme、 <span style='color:red'>Jest</span>、testdouble
- コードカバレッジのレポートを生成する
  Istanbul、 <span style='color:red'>Jest</span>
- シナリオ実行の管理ができるブラウザ、または疑似ブラウザの環境を提供する
  Protractor、Nightwatch、Phantom、Casper

　
機能だけ見るとJestの対抗はAVAとJasmine
　

---

## セットアップ
- - -
create-react-appを使用する前提でのJestのセットアップを書く
セットアップから簡単なテストを一通り実施するスライドにする
