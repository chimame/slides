<style type="text/css">
  .reveal h1,
  .reveal h2,
  .reveal h3,
  .reveal h4,
  .reveal h5,
  .reveal h6 {
    text-transform: none;
  }
  .c-hatena-embed{
    display: block;
    overflow: hidden;
    width: 100%;
    max-width: 500px;
    margin: 0 0 1.7rem;
    border: none;
  }
  .reveal code {
    font-family: Consolas, 'Courier New', Courier, Monaco, monospace;
  }
</style>
# RailsプログラマのためのReact + Redux TDD
## shinosaka.rb & nishiwaki.rb & kobe.rb
# Jest編

rito

2017/07/22

---

## 目次
- - -
　
- フロントエンドテスト事情
　
- テストツール
　
- セットアップ
　
- Jestチュートリアル
　
　

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
　
1年くらい前まで（私の周り）のトレンド？は
　
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
　
　
今回は`create-react-app`を使用するので
　
```shell
$ yarn global add create-react-app
$ create-react-app jest_hands_on
$ cd jest_hands_on
```
　
以上です！（素の場合は色々あるけど…）
　
　
---

## セットアップ
- - -
　
`yarn test`でテストが実行できます
　
```shell
$ yarn test
#=>  PASS  src/App.test.js
#=>  ✓ renders without crashing (54ms)
#=>
#=>Test Suites: 1 passed, 1 total
#=>Tests:       1 passed, 1 total
#=>Snapshots:   0 total
#=>Time:        4.628s
#=>Ran all test suites related to changed files.
```
　
　
　
---

## Jestチュートリアル
- - -
　
　
以下のファイルを作成し、軽くテストをしてみます
　
```js
// <root>/src/sample/sample.js
const sample = (i) => {
  return i + 1
}

export default sample
```
　
　
　
---

## Jestチュートリアル
- - -
　
テスト実行ファイルは以下の２パターンです
　
- 「`__tests__`」というフォルダ以下に配置している`"*.js"`ファイルを実行
　
- `"*.spec.js"`もしくは`"*.test.js"`ファイルを実行
　
　
　
　

---

## Jestチュートリアル
- - -
　
functionのテスト例
　
```js
// <root>/src/__tests__/sample.js
import sample from '../sample/sample.js'

describe('sample', () => {
  beforeAll(() => {
    console.log('beforeAll')
  })
  beforeEach(() => {
    console.log('beforeEach')
  })
  test('plus one', () => {
    expect(sample(1)).toBe(2)
  })

  test('not', () => {
    expect(sample(1)).not.toBe(1)
  })
})
```

---

## Jestチュートリアル
- - -
　
モックのテスト例
　
```js
// <root>/src/sample/test/mockSample.test.js
describe('mockSample', () => {
  jest.mock('../sample')
  const sample = require('../sample').default

  sample.mockImplementation(() => 42)

  test('sample', () => {
    expect(sample(1)).toBe(42)
  })
})
```
　
　
---

## Jestチュートリアル
- - -
　
divを出力するコンポーネント
　
```js
// <root>/src/sample/render.js
import React from 'react'

export default () => {
  return (
    <div>test</div>
  )
}
```
　
　
　
　
　
---

## Jestチュートリアル
- - -
　
divコンポーネント構造をテストする
実行すると`__snapshots__`フォルダが作成される
　
```js
// <root>/src/sample/test/render.test.js
import render from '../render.js'

describe('toMatchSnapshot example', () => {
  test('render', () => {
    expect(render()).toMatchSnapshot()
  })
})
```
　
コンポーネント側を変更してから再度テスト動かすと…
差分を見て問題ない場合は`yarn test -- -u`
　
---

## Jestチュートリアル
- - -
　
カバレッジ出力は`--coverage`オプションにて実行
　
```shell
$ yarn test -- --coverage
#---------------------------|----------|----------|----------|----------|----------------|
#File                       |  % Stmts | % Branch |  % Funcs |  % Lines |Uncovered Lines |
#---------------------------|----------|----------|----------|----------|----------------|
#All files                  |     8.16 |        0 |    16.67 |       16 |                |
# src                       |     2.17 |        0 |     6.25 |     4.55 |                |
#  App.js                   |      100 |      100 |      100 |      100 |                |
#  index.js                 |        0 |        0 |        0 |        0 |  1,2,3,4,5,7,8 |
#  registerServiceWorker.js |        0 |        0 |        0 |        0 |... 126,127,128 |
# src/sample                |      100 |      100 |      100 |      100 |                |
#  render.js                |      100 |      100 |      100 |      100 |                |
#  sample.js                |      100 |      100 |      100 |      100 |                |
#---------------------------|----------|----------|----------|----------|----------------|
```
　
　
---

## おわり
- - -
　
ということで本日はこのJestを使用してのTDDからReact+Reduxを勉強しようという会です
　
　
Jestの使用で困れば以下を参考に
<iframe
  class="c-hatena-embed"
  title="Facebook製のJavaScriptテストツール「Jest」の逆引き使用例"
  src="https://hatenablog-parts.com/embed?url=http://qiita.com/chimame/items/e97883fd46b67529d59f"
  frameborder="0"
  scrolling="no">
</iframe>
　
　
　
　
　
